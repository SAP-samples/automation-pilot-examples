# SAP Automation Pilot Examples

![Logo](assets/autopi.svg)

[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/automation-pilot-examples)](https://api.reuse.software/info/github.com/SAP-samples/automation-pilot-examples)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)
[![Activity](https://img.shields.io/github/commit-activity/m/SAP-samples/automation-pilot-examples)](https://github.com/SAP-samples/automation-pilot-examples/pulse)

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Examples](#examples)
  * [HANA Cloud](#hana-cloud)
  * [BTP Management](#btp-management)
  * [Cloud Foundry](#cloud-foundry)
  * [Kubernetes](#kubernetes)
  * [Neo](#neo)
  * [Scripting](#scripting)
  * [Utility Commands](#utility-commands)
  * [Availability Check](#availability-check)
* [Resources](#resources)
* [Known Issues](#known-issues)
* [How to obtain support](#how-to-obtain-support)
* [Contributing](#contributing)
* [License](#license)

## Description

SAP Automation Pilot is a low-code/no-code automation engine that's part of the SAP Business Technology Platform. It's goal is to simplify and automate complex manual processes in order to minimize the operational effort behind any cloud solution in the SAP BTP.

This repository contains example Automation Pilot commands which demonstrate the automation of various scenarios such as:

* Remediation & maintenance procedures
* Health checking
* Root cause analysis
* Mass operations
* And many more...

These examples can be used with little to no changes or they can be modified to better fit the user's scenarios.

:clapper: SAP Automation Pilot - Introduction

[![Introduction Video](https://img.youtube.com/vi/BIS_OK1ZNXI/hqdefault.jpg)](https://www.youtube.com/watch?v=BIS_OK1ZNXI)

## Requirements

To use the examples in this repository, you'll need SAP Automation Pilot tenant. The easiest way to get one is with SAP BTP trial:

* [Tutorial: Get a Free Account on SAP BTP Trial](https://developers.sap.com/tutorials/hcp-create-trial-account.html)
* [Tutorial: Setup Automation Pilot in SAP BTP](https://blogs.sap.com/2023/01/09/setup-configuration-of-automation-pilot-in-btp-cockpit/)
* [Automation Pilot Initial Setup Documentation](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/76e77c4563d042b2b46f6c622be3a091.html)

:information_source: Each example might have additional requirements. They will described in details in the example's README.

## How to use

Each example consists of a `catalog.json` file. To get started, you'll need to import the contents of this file in your SAP Automation Pilot tenant by performing the following steps:

* Copy the content of the `catalog.json` file for the example that you want to use
* Go to your SAP Automation Pilot tenant and navigate to `My Catalogs`
* Click on `Import` in the upper right corner
* Paste the catalog's content and import it

More information on how to import a catalog can be found in the [documentation](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/48ee09640e094bcb9601d845f316f773.html).

After importing, you'll see a new catalog tile - **Automation Pilot Examples**. From there, you can navigate to all commands and inputs which are part of the catalog.

:information_source: All examples in this repository are part of the **Automation Pilot Examples** catalog.

## Examples

### HANA Cloud

| Example | Description |
|---------|-------------|
| [Update HANA Cloud](update-hana-cloud) | Automatically update the HANA Cloud database to the latest patch version, to the next or most recent QRC version |
| [Mass Stop/Start HANA Cloud](mass-stop-start-hana-cloud) | Stop or start all HANA Cloud databases across your entire BTP account |
| [Check HANA Cloud Backup](check-hana-cloud-backup) | Check regularly whether there was a recent backup of a SAP HANA Cloud database |
| [Check HANA Cloud Audit Logs](check-hana-cloud-audit-logs) | Check regularly for any suspicious audit log entries in a SAP HANA Cloud database |
| [Check HANA Cloud Availability](check-hana-cloud-availability) | Check regularly whether the HANA Cloud database is currently available |
| [Rotate HANA Cloud Database Credentials](rotate-hana-cloud-db-credentials) | Automate the rotation of credentials for a HANA Cloud database |

### BTP Management

| Example | Description |
|---------|-------------|
| [Create and Configure BTP Subaccount](prepare-btp-subaccount) | Create a new BTP subaccount, configure entitlements and setup essential service instances |
| [Setup Cloud Foundry BTP Environment](prepare-btp-environment) | Enable the Cloud Foundry environment, create a space and setup a service instance |
| [Grant Privileges](grant-privileges) | Grant privileges to users on subaccount, organization and space level |
| [Reassign Identity Provider](reassign-identity-provider) | Migrate all users on BTP subaccount level from one identity provider to another |
| [Remove Inactive Subaccount Users](remove-inactive-subaccount-users) | Identify and remove inactive users from a BTP subaccount |

### Cloud Foundry

| Example | Description |
|---------|-------------|
| [:sparkles: Cloud Foundry Apps Insights](cf-apps-insights) | Effortlessly identify the state of your Cloud Foundry applications powered by Gen AI |
| [Mass Restart CF Apps](mass-restart-cf-apps) | Restart all applications in a given Cloud Foundry space |
| [Mass Stop/Start CF Apps](mass-stop-start-cf-apps) | Stop or start all Cloud Foundry applications across your entire BTP account |
| [CF resource quota notifications](check-cf-space-quota-utilization) | Get insights about Cloud Foundry resource usage via Alert Notification service |

### Kubernetes

| Example | Description |
|---------|-------------|
| [Execute Script Via Kubernetes Job](execute-script-via-k8s-job) | Execute a custom script within a Kubernetes Job in a customer-owned Kubernetes cluster |

### Neo

| Example | Description |
|---------|-------------|
| [Auto Scale Neo App](auto-scale-neo-app) | Automatically scales up a Neo application and monitors it over time, potentially scaling it back down |

### Scripting

| Example | Description |
|---------|-------------|
| [HTTP Request via Script](script-http-request) | Perform HTTP requests with large timeouts by utilizing the ExecuteScript command |
| [Use Custom Python Package](use-custom-python-package) | Install and use custom Python package in a script |
| [Use Custom NPM Package](use-custom-npm-package) | Install and use custom NPM package in a NodeJS script |
| [Use make and helm](use-make-and-helm) | Pull git repo and use make and helm to deploy the helm chart to kubernetes cluster |

### Utility Commands

| Example | Description |
|---------|-------------|
| [Transform Data](transform-data) | Transform Data between different formats - JSON, XML, YAML, and CSV |
| [Convert JSON to HTML Table](convert-json-to-html-table) | Convert JSON array of objects to HTML table |
| [Trigger and Collect Outputs Batching](trigger-and-collect-outputs-batching) | Trigger Multiple Executions in Batches and Collect their Outputs |
| [Pretty Print XML](pretty-print-xml) | Pretty Print XML Data |

### Availability Check

| Example | Description |
|---------|-------------|
| [Advanced Availability Check](advanced-availability-check) | Enables comprehensive monitoring, tracking of Service Level Agreements (SLAs) and data visualization within the Dynatrace platform. |

## Resources

Check out the following resources if you want to get familiar with Automation Pilot:

* [Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/automation-pilot)
* [Official Documentation](https://help.sap.com/docs/AUTOMATION_PILOT)
* [API Business Hub](https://api.sap.com/package/SAPCloudPlatformAutomationPilot/overview)
* [Blog Posts](https://blogs.sap.com/tags/73554900100800002433/)
* [Tutorials](https://developers.sap.com/tutorial-navigator.html?search=automation+pilot)

## Known Issues

No known issues.

## How to obtain support

[Create an issue](https://github.com/SAP-samples/automation-pilot-examples/issues) in this repository if you find a bug or have questions about the content.

For additional support, [ask a question in SAP Community](https://answers.sap.com/questions/ask.html).

## Contributing

If you wish to contribute code, offer fixes or improvements, please send a pull request. Due to legal reasons, contributors will be asked to accept a DCO when they create the first pull request to this project. This happens in an automated fashion during the submission process. SAP uses [the standard DCO text of the Linux Foundation](https://developercertificate.org/).

## License

Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSE) file.
