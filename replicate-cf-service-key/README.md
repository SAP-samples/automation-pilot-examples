# Replicate a Cloud Foundry Service Key Across Regions

Table of Contents

* [Description](#description)
* [Commands](#commands)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Scheduling](#scheduling)
* [Expected result](#expected-result)

## Description

This example demonstrates how to automate the replication and rotation of service credentials from a source Cloud Foundry (CF) region into one or more target CF regions, with the goal of preventing certificate expiration and avoiding manual user error.

A common pattern is to have a **single service instance** in one CF region whose credentials - obtained from a **service key** - are also needed in several other regions. In each of those regions a **user-provided service (UPS)** holds a copy of the credentials, because the consuming setup (for example, Multi-Target Application deployments) works with CF representations of the service. Keeping those copies in sync by hand is error-prone, and service keys backed by **certificates** eventually expire, which leads to outages if the renewal is missed.

This automation keeps a consistently named user-provided service up to date across every landscape and rotates the underlying service key before its certificate expires - without downtime for consumers that are still using the previous credentials.

To keep the setup universal, the **source subaccount is treated as just another target**: a UPS with the same name is created in every listed landscape, including the source. This avoids special-casing the source region, so consumers everywhere reference one stable service name.

The zero-downtime guarantee comes from the ordering: a new key is created and replicated into every landscape **first**, and only **then** are the older keys deleted. Deployments that still reference the previous credentials keep working until the old keys are removed.

Authentication to every landscape is done with a single CF user (ID/email and password) over an identity provider (SAP ID Service by default). The same user must have permissions in the source and in all target landscapes.

## Commands

In normal use you only trigger or schedule these two commands:

| Command | Purpose |
|---------|---------|
| `CheckAndRotateServiceKey` | The main command. Reads the current service key's certificate and performs a zero-downtime rotation **only** when it expires within a configurable threshold (default 30 days), when no key exists yet, or when the key is already expired. Schedule it to run periodically. |
| `CleanupExpiredServiceKeys` | Optional safety net. Prunes old keys sharing a prefix, keeping the newest and deleting the others once they are older than a grace period (default 1 day). |

## Requirements

To use this example you'll need the following:

* **SAP Automation Pilot Tenant**: Ensure you have access to an SAP Automation Pilot tenant.
* **A source service instance**: A Cloud Foundry service instance that issues a service key - for example an [SAP Cloud Logging](https://help.sap.com/docs/cloud-logging) instance, whose key contains the mTLS client certificate used by consumers.
* **One or more target landscapes**: A Cloud Foundry org and space in each region where the credentials should be replicated. The source landscape is also listed as a target.
* **A CF user with access everywhere**: A single Cloud Foundry user (ID/email and password) that has permissions in the source and in all target landscapes (for example, Space Developer in each space). Storing these credentials as a reusable [Input](https://help.sap.com/docs/automation-pilot/automation-pilot/managing-inputs?locale=en-US) is recommended.

## How to use

1. **Import the Example**:

* Copy the content of the [catalog.json](./catalog.json) file.
* Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
* Click on `Import` in the upper right corner.
* Paste the catalog's content and import it.

2. **Trigger the Command Manually**:

* Navigate to the `CheckAndRotateServiceKey` command.
* Click on the *Trigger* button after getting familiar with the command.
* Provide values for the following input keys:
  * `sourceRegion`: Technical name of the source CF region, e.g. `cf-eu10`.
  * `sourceOrg`: Name or ID of the source CF organization.
  * `sourceSpace`: Name or ID of the source CF space.
  * `sourceServiceInstance`: Name or ID of the source service instance that issues the key.
  * `serviceKeyPrefix`: Name prefix shared by the rotating keys, e.g. `mta-exporter-sk`. A new key is named `<serviceKeyPrefix>-<timestamp>`.
  * `upsName`: The consistent user-provided service name created/updated in every landscape, e.g. `mta-exporter-ups`.
  * `targets`: Array of target landscapes, each with `region`, `org` and `space`. Include the source landscape to keep the setup homogeneous. Example:
    ```json
    [
      { "region": "cf-eu10", "org": "my-source-org", "space": "dev" },
      { "region": "cf-us10", "org": "my-us-org", "space": "dev" },
      { "region": "cf-ap10", "org": "my-ap-org", "space": "dev" }
    ]
    ```
  * `expirationThreshold`: Rotate when the certificate expires within this many days (optional, default `30`).
  * `user`: CF user ID/email with access to all landscapes.
  * `password`: Password for the user.
  * `identityProvider`: Identity provider origin key (optional, default `sap.ids`).
* Confirm and start the automation.

## Scheduling

Because `CheckAndRotateServiceKey` only rotates when the certificate is actually close to expiring, it is safe to [schedule](https://help.sap.com/docs/automation-pilot/automation-pilot/managing-schedules?locale=en-US) it to run regularly - for example once a day. On most runs it will simply report the remaining days and do nothing; when the threshold is reached it performs the zero-downtime rotation automatically.

Optionally, schedule `CleanupExpiredServiceKeys` (for example weekly) as a safety net to prune superseded keys that are older than the configured grace period.

## Expected result

When you run `CheckAndRotateServiceKey`:

* **Certificate still healthy** - the command reports `rotated: false` and `daysLeft` set to the number of days until the certificate expires, and makes no changes.
* **Certificate near expiry, missing, or expired** - the command reports `rotated: true` and `newServiceKeyName` set to the freshly created `<serviceKeyPrefix>-<timestamp>` key. A new key is created, a user-provided service with the configured `upsName` is created or updated in place in every listed landscape (including the source), and the older keys sharing the prefix are deleted afterwards.

> :information_source: **Certificate parsing note:** different services expose the client certificate under different credential field names. `CheckAndRotateServiceKey` looks for the certificate under the common names (`certificate`, `clientcert`, `sslcert`, `uaa.certificate`, `x509.certificate`) as well as SAP Cloud Logging's `ingest-mtls-cert`. If your service stores its certificate under a different key, add that key to the `parseCert` extraction expression in the command; otherwise the certificate cannot be inspected and the command will rotate on every run as a safe fallback.
