# Execution of a SAP Host Agent operation via Automation Pilot and SAP Cloud Connector

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

This example demonstrates how SAP Automation Pilot can perform HTTP requests in order to execute SAP Host Agent Operations via the [SAP Cloud Connector](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/cloud-connector). Any HTTP-based protocol is supported, including OData, REST, and SOAP.

By leveraging the Cloud Connector, Automation Pilot can interact with systems that are not directly accessible from the public Internet, enabling secure automation scenarios across hybrid landscapes.

## Requirements

To use this example you'll need the following:

* **SAP Automation Pilot Tenant**: Access to an SAP Automation Pilot tenant - [help](https://help.sap.com/docs/automation-pilot/automation-pilot/initial-setup).
* **SAP Cloud Connector**: Connected to the same SAP BTP account as your Automation Pilot tenant - [help](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/cloud-connector). [Here](https://help.sap.com/docs/automation-pilot/automation-pilot/what-is-sap-automation-pilot) you can find in which regions SAP Automation Pilot is available.
* **Configured Cloud Connector Mapping**: The internal HTTP endpoint for SAP Host Agent must be exposed via the Cloud Connector and accessible using a virtual hostname and port.

### Cloud Connector Setup Steps

1. **Expose access to the SAP Host Agent through the Cloud Connector**
   Assign a virtual host and port to SAP Host Agent in the Cloud Connector admin console. This virtual host will be used to send requests from BTP (e.g., Automation Pilot) to the agent.
   Standard **Internal HTTPS port** - *1129* and **URL Path** - */saphostagent/services/SAPHostControl*

2. **Verify Cloud Connector connection in BTP**
   Once the Cloud Connector is successfully connected to your BTP subaccount and the system is exposed, you will see the Cloud Connector listed in your BTP subaccount cockpit.

## How to use

1. **Import the Example**:
   * Copy the content of the provided file.
   * Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`.
   * Click on `Import` in the upper right corner.
   * Paste the catalog's content and import it.

2. **Trigger the Command**:
   * Use the `RunOperationViaScc` command.
   * Provide the neccessary values for the input keys:
      * server - the virtual hostname as configured in the Cloud Connector
      * arguments - the arguments that will be passed to the SAP Host Agent operation, in the format *{"argumentName": "argumentValue"}*
      * sensitiveArguments – sensitive arguments that will be passed to the SAP Host Agent operation, in the same format as arguments
      * name - the name of the SAP Host Agent operation
      * user - the user used for authenticating to the system. Most commonly *sapadm*
      * password -  the user's password
      * locationId - the Location ID of the Cloud Connector (or leave empty if not specified)
   * Start the automation.

## Expected result

After execution, the command will trigger the specified SAP Host Agent operation via the Cloud Connector and wait for it to finish. The result from the operation will be returned as output.
