# Remove Inactive Subaccount Users

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

This example demonstrates how to use SAP Automation Pilot to identify and remove inactive users from a subaccount in SAP BTP. The command allows customization of the inactivity grace period and provides options to exclude specific users or remove users who have never logged in.

Inactive users can pose a security risk if they are not monitored or managed properly. Regularly cleaning up inactive users helps maintain compliance with internal and external security standards.

Automating the removal of inactive users offers several advantages over manual processes, such as reducing time and effort, enabling the management of a large number of users across multiple subaccounts, and more.

The command can also be scheduled to run on a weekly, monthly, or custom basis to ensure continuous compliance and security.

### Customization Options

The command provides several customization options to tailor the automation to your needs:

* **Grace Period**: Adjust the number of days since a user's last login after which they are considered inactive by modifying the `grace` input parameter.
* **Remove Users Who Never Logged In**: Enable or disable the removal of users who have never logged in by setting the `removeNeverLogged` input parameter.
* **Exclude Specific Users**: Specify a list of users who should not be removed even if they are inactive by providing their usernames in the `excludeUsers` input parameter.

## Requirements

To use this example you'll need the following:

* **SAP Automation Pilot Tenant**: Ensure you have access to an SAP Automation Pilot tenant.
* **SAP Authorization and Trust Management Service**: A service key (API credentials) to enable programmatic access to the SAP Authorization and Trust Management Service.

To gain API access to **SAP Authorization and Trust Management Service**, follow the steps in the [SAP BTP documentation](https://help.sap.com/docs/btp/sap-business-technology-platform/get-access-to-apis).

You can also use the BTP CLI to create the necessary API credentials for your BTP subaccount with the following command:

```shell
btp --format json create security/api-credential --name autopi-credential --sub-account '<SUBACCOUNT_ID>'
```

## How to use

1. **Import the Example**:

* Copy the content of the [catalog.json](./catalog.json) file.
* Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
* Click on `Import` in the upper right corner.
* Paste the catalog's content and import it.

2. **Trigger the Command Manually**:

* Navigate to the `RemoveInactiveSubaccountUsers` command in your SAP Automation Pilot tenant.
* Click on the *Trigger* button after getting familiar with the command
* Provide values for the following input keys:
  * `serviceKey`: The service key for SAP Authorization and Trust Management Service.
  * `grace`: Number of days since the last login after which a user is considered inactive.
  * `removeNeverLogged`: Boolean flag to enable or disable the removal of users who have never logged in.
  * `excludeUsers`: List of usernames to exclude from removal even if they are inactive.
  * `targetIdentityProvider`: Identity provider of the target users (default is `sap.ids`).
* Confirm and start the automation

:information_source: If you want to test the command without actually removing any users, click on the *Trigger Dry* Run option. This will allow the command to identify which users are inactive without making any changes. Once you have reviewed the list of inactive users, you can run the command again in non-dry run mode to proceed with the removal.

## Expected result

After executing the command, the following results are expected:

* Inactive users, based on the specified grace period, will be identified and removed from the subaccount.
* Users who have never logged in will be removed if the `removeNeverLogged` parameter is set to true.
* Users specified in the `excludeUsers` list will not be removed, even if they are inactive.
* A list of removed inactive users will be provided as output for verification and record-keeping.
