# HTTP Request With OAuth Client Credentials

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [Configuring OAuth Setup](#configuring-oauth-setup)
* [Configuring Automatic Retry for OAuth Token Acquisition](#configuring-automatic-retry-for-oauth-token-acquisition)
* [How to use](#how-to-use)

## Description

This example demonstrates how to perform HTTP requests to endpoints that require OAuth 2.0 authentication using the client credentials flow. Two scenarios are covered:

* Using a client secret (standard client credentials flow)
* Using mTLS for enhanced security

Both scenarios target the [SAP Service Manager API](https://api.sap.com/api/APIServiceManager/path/getServiceOfferings), where authentication details are provided via a service key obtained from the SAP BTP cockpit. The service key contains all necessary information: client ID, authentication credentials (client secret or certificate/key), OAuth token URL, and the Service Manager API endpoint.

SAP Automation Pilot's [HttpRequest](https://help.sap.com/docs/automation-pilot/automation-pilot/httprequest-command?locale=en-US) command supports multiple authentication mechanisms, including OAuth 2.0. It can transparently obtain and reuse OAuth tokens throughout the execution as long as they remain valid, and will automatically acquire a new token if the current one is about to expire. It is recommended to always let the `HttpRequest` command handle token acquisition.

## Requirements

To use these examples you'll need the following:

* **SAP Automation Pilot Tenant**: Access to an SAP Automation Pilot tenant.
* **SAP Service Manager Instance**: A Service Manager instance in your SAP BTP subaccount.
* **Service Key**: A service key for the Service Manager instance.

> **Note:**
> Each BTP service might require specific parameters when creating the service key. Additionally, the structure of the service key JSON may differ for each service. You must get familiar with the service you are using and configure the command accordingly.

For example, a service key structure for **client secret** may look like this:

```json
{
  "clientid": "sb-xxxx|service-manager!xxxx",
  "clientsecret": "ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890",
  "url": "https://my-subdomain.authentication.eu10.hana.ondemand.com",
  "sm_url": "https://service-manager.cfapps.eu10.hana.ondemand.com"
}
```

For **mTLS**:

```json
{
  "clientid": "sb-xxxx|service-manager!xxxx",
  "certificate": "-----BEGIN CERTIFICATE-----...-----END CERTIFICATE-----",
  "key": "-----BEGIN PRIVATE KEY-----...-----END PRIVATE KEY-----",
  "certurl": "https://my-subdomain.authentication.cert.eu10.hana.ondemand.com",
  "sm_url": "https://service-manager.cfapps.eu10.hana.ondemand.com"
}
```

## Configuring OAuth Setup

To configure the OAuth setup in your Automation Pilot command, you need to extract the required values from the service key using [Dynamic Expressions](https://help.sap.com/docs/automation-pilot/automation-pilot/dynamic-expression?locale=en-US). The screenshot below shows how to map the fields from the service key object to the OAuth configuration in the command input:

![OAuth Setup Example](./assets/oauth-setup-example.png)

## Configuring Automatic Retry for OAuth Token Acquisition

In some scenarios, the request to obtain an OAuth token may fail due to network problems, timeouts, or other transient issues. You can configure your command to automatically retry the OAuth token request if such failures occur.

To ensure that only the OAuth token acquisition is retried (and not the main API request), you should configure the retry condition to match only OAuth-related failures. This can be done by checking if the error message contains specific text, such as:

* `Failed to obtain oAuth 2.0 token` (for general OAuth token acquisition failures)
* `Connectivity timeout issue` (for network or timeout problems)

The screenshot below shows an example of how to set up the autoretry condition:

![Autoretry Setup Example](./assets/autoretry-setup-example.png)

## How to use

1. **Import the Example**:
   * Copy the content of the [catalog.json](./catalog.json) file.
   * Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
   * Click on `Import` in the upper right corner.
   * Paste the catalog's content and import it.

2. **Trigger the Command**:
   * For **client secret** authentication:
     * Use the `HttpOAuthWithSecret` command.
     * Provide the `serviceKey` input (the JSON object from your Service Manager service key with client secret).
   * For **mTLS (certificate + key)** authentication:
     * Use the `HttpOAuthWithMtls` command.
     * Provide the `serviceKey` input (the JSON object from your Service Manager service key with certificate and key).
   * Confirm and start the automation.
