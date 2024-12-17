# Mass Stop and Start of HANA Cloud Instances

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

This example demonstrates how to automate the mass stopping and starting of HANA Cloud instances. It is particularly useful for managing large-scale environments where multiple HANA Cloud instances need to be controlled simultaneously. Automating these operations helps to reduce manual effort, minimize downtime, and ensure consistency across all instances.

The example includes multiple commands, depending on the BTP subaccount environment.

For *Cloud Foundry Environment*:

* **MassStopHanaCloudDatabasesCF**: Stops all HANA Cloud instances across every Cloud Foundry space in a subaccount.
* **MassStartHanaCloudDatabasesCF**: Starts all HANA Cloud instances across every Cloud Foundry space in a subaccount.

For *Other Environment* (also known as *Multi-Environment* or Subaccount level):

* **MassStopHanaCloudDatabasesOtherEnv**: Stops all HANA Cloud instances within a specified BTP subaccount (service: hana-cloud, plan: hana).
* **MassStartHanaCloudDatabasesOtherEnv**: Starts all HANA Cloud instances within a specified BTP subaccount (service: hana-cloud, plan: hana).

These commands provide flexibility to manage HANA Cloud instances at both the Cloud Foundry space level and the subaccount level, making it easier to handle different deployment scenarios. This example can manage one or multiple HANA instances, ranging from tens to even hundreds.

### Core Benefits

* **Efficiency**: Automates repetitive tasks, saving time and reducing the risk of human error.
* **Scalability**: Easily manage multiple instances across different environments.
* **Consistency**: Ensures that all instances are started or stopped in a uniform manner.
* **Cost Management**: Helps in managing costs by stopping instances when not in use.

### Sample Scenarios

* **Development Environments**: Stop databases during non-working hours to save costs and start them again during working hours.
* **Testing Environments**: Automatically start databases before running test suites and stop them afterward to optimize resource usage.
* **Maintenance Windows**: Schedule stops and starts of databases during maintenance windows to ensure minimal disruption.

## Requirements

For *Cloud Foundry Environment* you'll need the following:

* **SAP Automation Pilot Tenant**: Ensure you have access to an SAP Automation Pilot tenant.
* **HANA Cloud Databases**: HANA Cloud databases in Cloud Foundry.
* **Service Manager Service Key**: A service key for the SAP Service Manager.
* **Cloud Foundry User**: Credentials for a Cloud Foundry user with appropriate permissions (*Space Developer*).

For *Other Environment* you'll need the following:

* **SAP Automation Pilot Tenant**: Ensure you have access to an SAP Automation Pilot tenant.
* **HANA Cloud Databases**: HANA Cloud databases in *Other Environment*.
* **Service Manager Service Key**: A service key for the SAP Service Manager.

## How to use

1. **Import the Example**:

* Copy the content of the [catalog.json](./catalog.json) file.
* Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
* Click on `Import` in the upper right corner.
* Paste the catalog's content and import it.

### Cloud Foundry Environment

If your HANA Cloud database is in the *Cloud Foundry environment*, navigate to the desired command (e.g., `MassStopHanaCloudDatabasesCF`, `MassStartHanaCloudDatabasesCF`) in your SAP Automation Pilot tenant.

You'll need to provide values for the following input keys:

* `serviceKey`: Service key for the SAP Service Manager.
* `user`: UserID/Email of the Cloud Foundry user which will be used for authentication.
* `password`: Cloud Foundry user's password.
* `identityProvider`: Identity provider to be used (optional, default is `sap.ids`).
* `excludedInstances`: Names of HANA Cloud instances which should not be stopped/started. Example: `[ "my-prod-hana" ]` (optional).

### Other Environment

If your HANA Cloud database is in the *Other environment*, navigate to the desired command (e.g., `MassStopHanaCloudDatabasesOtherEnv`, `MassStartHanaCloudDatabasesOtherEnv`) in your SAP Automation Pilot tenant.

You'll need to provide values for the following input keys:

* `serviceKey`: Service key for the SAP Service Manager.
* `deadline`: Number of minutes to wait for the process to complete successfully (optional, default is 60 minutes).
* `excludedInstances`: Names of HANA Cloud instances which should not be stopped/started. Example: `[ "my-prod-hana" ]` (optional).

## Expected result

After executing the mass stop or start commands, you should see the following results:

1. The command will list all HANA Cloud instances in the specified environment.
2. It will exclude any instances specified in the `excludedInstances` input key.
3. The command will initiate the stop/start process for each instance.
4. It will wait for the stop/start process to complete for each instance.
5. The output will list all instances that have been successfully stopped/started.

You can verify the status of the instances in the SAP HANA Cloud Central or by checking the output values in the Automation Pilot execution logs.
