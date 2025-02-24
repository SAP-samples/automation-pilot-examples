# Run HANA Cloud Stored Procedure

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

This example demonstrates how to trigger a stored procedure in HANA Cloud asynchronously and continuously monitor its status until completion using SAP Automation Pilot. This approach is useful for efficiently managing long-running processes without interrupting the execution flow.

To start the HANA Cloud stored procedure asynchronously, the example uses the following SQL statement: `CALL "sleep"(10) ASYNC`. The result of this query is the `ASYNC_CALL_ID`, which can be used to check the status of the procedure from the `M_PROCEDURE_ASYNC_EXECUTIONS` system view. You can find more details about this approach in the [HANA Cloud documentation](https://help.sap.com/docs/hana-cloud-database/sap-hana-cloud-sap-hana-database-sql-reference-guide/call-statement-procedural).

This example can be easily adapted to run your own productive stored procedure by modifying the SQL statement and the procedure parameters as needed.

## Requirements

To use this example you'll need the following:

* **SAP Automation Pilot Tenant**: Ensure you have access to an SAP Automation Pilot tenant.
* **HANA Cloud Database**: A HANA Cloud database instance where the stored procedure will be executed.
* **Stored Procedure**: The procedure used in this example is a simple sleep procedure to simulate a long-running process. You must create it manually first, for example from the HANA Cloud SQL Console.

  ```sql
  CREATE PROCEDURE "sleep" (IN sleep_duration INT)
  LANGUAGE SQLSCRIPT
  SQL SECURITY INVOKER READS SQL DATA AS
  BEGIN
      USING SQLSCRIPT_SYNC as SyncLib;
      CALL SyncLib:SLEEP_SECONDS(sleep_duration);
  END
  ```

* **Database User Credentials**: Credentials for a database user with the necessary permissions to execute the stored procedure.

## How to use

1. **Import the Example**:

* Copy the content of the [catalog.json](./catalog.json) file.
* Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
* Click on `Import` in the upper right corner.
* Paste the catalog's content and import it.

2. **Trigger the Command Manually**:

* Navigate to the `RunHanaCloudStoredProcedure` command in your SAP Automation Pilot tenant.
* Click on the *Trigger* button after getting familiar with the command.
* Provide values for the following input keys:
  * `connectionUrl`: Connection URL for access to the HANA Cloud database
  * `user`: Name of the database user
  * `password`: Password for the database user
  * `procedureDuration`: Duration of the procedure in seconds (default is 30)
* Confirm and start the automation.

## Expected result

After successfully executing the example, the stored procedure will be triggered asynchronously, and the status will be continuously polled until completion. The output will include the following details:

* **id**: The unique identifier of the procedure execution.
* **startTime**: The start time of the procedure.
* **endTime**: The end time of the procedure.
* **errorText**: The error message in case the procedure execution has failed.
* **errorCode**: The error code in case the procedure execution has failed.

These output keys provide comprehensive information about the execution status and any potential issues that occurred during the process.
