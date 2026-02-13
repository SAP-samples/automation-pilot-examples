# Check Cloud Foundry Application Certificates

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Schedule Regular Execution](#schedule-regular-execution)
* [Expected Result](#expected-result)

## Description

This example helps you monitor X.509 certificate expiration in Cloud Foundry service bindings. Expired certificates can cause application failures and service disruptions. By proactively checking certificate expiration dates, you can renew certificates before they expire and avoid downtime.

The example provides three commands:

* **CheckAppCertificates** - Checks certificate expiration for all service bindings of a single Cloud Foundry application. Returns a list of certificates expiring within the configured threshold.

* **CheckSpaceCertificates** - Checks certificate expiration for all applications in a Cloud Foundry space. Iterates through all applications in the space and aggregates the results. Optionally sends a summary notification via SAP Alert Notification service.

* **GetCfServiceBindingDetails** - Helper command that retrieves credentials for a specific service binding. Used internally by the other commands.

The automation works by:

1. Retrieving all service bindings for the target application(s).
2. Fetching the credentials for each binding.
3. Extracting X.509 certificates from common credential locations (`credentials.certificate`, `credentials.uaa.certificate`, `credentials.x509.certificate`).
4. Checking each certificate's expiration date against the configured threshold.
5. Reporting certificates that will expire within the threshold period.
6. Optionally sending a summary notification to SAP Alert Notification service (CheckSpaceCertificates only).

## Requirements

To use this example you'll need the following:

* SAP Automation Pilot tenant
* Cloud Foundry user with **Space Developer** role in the target space
* (Optional) SAP Alert Notification service instance for receiving notifications

Check out the following resources for more information:

* [SAP Automation Pilot Documentation](https://help.sap.com/docs/automation-pilot)
* [SAP Alert Notification service](https://help.sap.com/docs/alert-notification)
* [Cloud Foundry User Roles](https://help.sap.com/docs/btp/sap-business-technology-platform/about-roles-in-cloud-foundry-environment)

## How to use

1. **Import the Example**:
   * Copy the content of the `catalog.json` file.
   * Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
   * Click on `Import` and paste the catalog content.

2. **Trigger the Command**:
   * For a single application: Navigate to `CheckAppCertificates` and click `Trigger`.
   * For all applications in a space: Navigate to `CheckSpaceCertificates` and click `Trigger`.

### Input Parameters for CheckAppCertificates

| Parameter | Required | Default | Description |
| --------- | -------- | ------- | ----------- |
| region | Yes | - | Cloud Foundry region (e.g., cf-eu10, cf-eu20) |
| org | Yes | - | Cloud Foundry organization name or ID |
| space | Yes | - | Cloud Foundry space name or ID |
| app | Yes | - | Cloud Foundry application name or ID |
| user | Yes | - | UserID/Email for the Cloud Foundry user |
| password | Yes | - | Password for the Cloud Foundry user |
| identityProvider | No | sap.ids | Identity provider origin key |
| expirationThreshold | No | 30 | Report certificates expiring within this many days (1-365) |

### Input Parameters for CheckSpaceCertificates

| Parameter | Required | Default | Description |
| --------- | -------- | ------- | ----------- |
| region | Yes | - | Cloud Foundry region (e.g., cf-eu10, cf-eu20) |
| org | Yes | - | Cloud Foundry organization name or ID |
| space | Yes | - | Cloud Foundry space name or ID |
| user | Yes | - | UserID/Email for the Cloud Foundry user |
| password | Yes | - | Password for the Cloud Foundry user |
| identityProvider | No | sap.ids | Identity provider origin key |
| expirationThreshold | No | 30 | Report certificates expiring within this many days (1-365) |
| ansServiceKey | No | - | SAP Alert Notification Service credentials. If provided, sends a summary notification after the check completes. |

## Schedule Regular Execution

Certificate expiration monitoring is most effective when run on a regular schedule. This ensures you receive timely warnings before certificates expire.

SAP Automation Pilot allows executions to be automatically triggered on regular intervals - hourly, daily, weekly, monthly, or yearly. For certificate monitoring, a daily or weekly schedule is recommended depending on your `expirationThreshold` setting.

Steps to schedule:

1. Open `Scheduled Executions` in the Automation Pilot UI.
2. Click `Schedule` to create a new schedule.
3. Select the `CheckSpaceCertificates` command.
4. Fill in all required parameters.
5. Choose your preferred schedule (e.g., daily).
6. Confirm to activate the schedule.

For more details, see the [Scheduled Execution documentation](https://help.sap.com/docs/automation-pilot/automation-pilot/scheduled-execution).

## Expected Result

### CheckAppCertificates Output

The command returns:
* `app` - The application name that was checked
* `certificates` - An array of certificates expiring within the threshold, each containing:
  * `id` - The service binding ID
  * `instanceName` - The service instance name
  * `daysLeft` - Number of days until the certificate expires

### CheckSpaceCertificates Output

The command returns:
* `space` - The space name that was checked
* `results` - An array of results per application (same format as CheckAppCertificates output)
* `ansEventId` - The Alert Notification event ID if a notification was sent

### Alert Notification

When `ansServiceKey` is provided to CheckSpaceCertificates and expiring certificates are found, a WARNING event is sent to SAP Alert Notification service with:
* **Subject**: Certificate Expiration Check - Space: {space name}
* **Body**: Summary of all certificates expiring within the threshold, grouped by application
* **Event Type**: CertificateExpirationCheck
* **Category**: ALERT

You can configure subscriptions in SAP Alert Notification service to receive these alerts via email, Slack, webhook, or other channels.
