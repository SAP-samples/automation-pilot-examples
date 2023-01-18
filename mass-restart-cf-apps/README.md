# Mass Restart Cloud Foundry Apps

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

The command detects all Cloud Foundry applications in a given space and restarts them one by one. For simplicity the command performs stop-start restart which might cause downtime for your applications. However, this could be easily changed to a rolling restart.

## Requirements

To use this example you'll need the following:

* Cloud Foundry space with at least one application
* Technical user with **Space Developer** role

Check out the [documentation](https://help.sap.com/docs/btp/sap-business-technology-platform/administration-and-operations-in-cloud-foundry-environment) for more information.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *MassRestartCfApp* command and trigger it.

You'll need to provide values for the following input keys:

* *region* - Technical name of your SAP BTP region, e.g. cf-eu10, cf-us20
* *subAccount* - Name of your Cloud Foundry organization
* *resourceGroup* - Name of your Cloud Foundry space
* *user* - Email or ID of your technical user
* *password* - Password of your technical user
* *identityProvider* - Optional: origin key of your identity provider. Defaults to sap.ids
