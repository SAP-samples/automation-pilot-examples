# Check Cloud Foundry Application Certificates

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Schedule Regular Execution](#schedule-regular-execution)
* [Expected Result](#expected-result)

## Description

This example helps you monitor certificate expiration in Cloud Foundry service bindings. It supports both standard X.509 certificates and PKCS7/CMS certificate bundles. Expired certificates can cause application failures and service disruptions. By proactively checking certificate expiration dates, you can renew certificates before they expire and avoid downtime.

### Built-in ANS Certificate Events

SAP Alert Notification service provides built-in certificate expiration events for specific services:

* [Alert Notification service](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/credential-expiration) - Monitors its own service binding credentials
* [Credential Store](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/expired-credentials) - Monitors credentials stored in the service
* [Destination Service](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/sap-btp-destination-service-expiring-certificate-notification) - Monitors destination certificates (not bindings)

This example complements those built-in events by covering **all other services** with X.509 certificate bindings that don't have native ANS integration.

The example provides three commands:

* **CheckAppCertificates** - Checks certificate expiration for all service bindings of a single Cloud Foundry application. Returns a list of certificates expiring within the configured threshold.

* **CheckSpaceCertificates** - Checks certificate expiration for all applications in a Cloud Foundry space. Iterates through all applications in the space and aggregates the results. Sends a summary notification via SAP Alert Notification service.

* **GetCfServiceBindingDetails** - Helper command that retrieves credentials for a specific service binding. Used internally by the other commands.

The automation works by:

1. Retrieving all service bindings for the target application(s).
2. Fetching the credentials for each binding.
3. Extracting certificates from common credential locations.
4. Checking each certificate's expiration date against the configured threshold.
5. Reporting certificates that will expire within the threshold period.
6. Sending a summary notification to SAP Alert Notification service (CheckSpaceCertificates only).

> [!NOTE]
> **Extending Certificate Detection**: Different SAP BTP services may store certificates in custom credential paths not covered by this example. If your service binding uses a different structure, you can extend the extraction logic by modifying the `extractCertificates` executor in the `CheckAppCertificates` command.
>
> To add a new path, edit the expression and append your custom path using the alternative operator (`//`):
> ```
> .credentials.certificate // .credentials.clientcert // ... // .credentials.YOUR_CUSTOM_PATH
> ```

## Requirements

To use this example you'll need the following:

* SAP Automation Pilot tenant
* Cloud Foundry user with **Space Developer** role in the target space
* SAP Alert Notification service instance for receiving notifications

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

When CheckSpaceCertificates finds expiring certificates, a WARNING event is sent to SAP Alert Notification service with:
* **Subject**: Certificate Expiration Check - Space: {space name}
* **Body**: Summary message with details about each application and expiring certificates (see example below)
* **Event Type**: CertificateExpirationCheck
* **Category**: ALERT
* **Severity**: WARNING
* **Resource Type**: space
* **Resource Name**: {space name}
* **Details Link**: Link to the Automation Pilot execution

Example event body:

```
Certificate check completed for space 'dev'. Found 3 certificate(s) expiring within 30 days.

App: my-app-1
- xsuaa-instance (15 days left)
- destination-instance (7 days left)

App: my-app-2
- connectivity-instance (25 days left)
```

You can configure subscriptions in SAP Alert Notification service to receive these alerts via email, Slack, webhook, or other channels.
