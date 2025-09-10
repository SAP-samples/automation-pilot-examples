# SAP Automation Pilot Examples

![Logo](assets/autopi.svg)

[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/automation-pilot-examples)](https://api.reuse.software/info/github.com/SAP-samples/automation-pilot-examples)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)
[![Activity](https://img.shields.io/github/commit-activity/m/SAP-samples/automation-pilot-examples)](https://github.com/SAP-samples/automation-pilot-examples/pulse)

Table of Contents

* [About SAP Automation Pilot](#about-sap-automation-pilot)
* [About This Repository](#about-this-repository)
* [Getting Started](#getting-started)
* [Examples](#examples)
  * [HANA Cloud](#hana-cloud)
  * [BTP Management](#btp-management)
  * [Cloud Foundry](#cloud-foundry)
  * [Kubernetes](#kubernetes)
  * [Neo](#neo)
  * [HTTP](#http)
  * [Scripting](#scripting)
  * [Utility Commands](#utility-commands)
  * [Availability Check](#availability-check)
* [Resources](#resources)
* [Known Issues](#known-issues)
* [How to obtain support](#how-to-obtain-support)
* [Contributing](#contributing)
* [License](#license)

## About SAP Automation Pilot

SAP Automation Pilot is a low-code/no-code automation service that's part of the SAP Business Technology Platform (BTP). As a cloud-native automation engine, it empowers customers to independently automate various scenarios, reducing manual effort and operational complexity across their SAP landscape.

SAP Automation Pilot is designed to:

* Automate complex manual processes with an intuitive, visual interface
* Minimize the time and resources needed to manage cloud solutions
* Allow customers to create and customize automation workflows themselves
* Provide consistent, repeatable execution of critical operational tasks
* Connect with various SAP and third-party services for comprehensive automation scenarios
* Deliver **over 300 built-in automations** supported by SAP for HANA Cloud, Cloud Foundry, cTMS, BTP management, and more
* Enable serverless execution of HTTP requests, SQL statements, and custom scripts (Python, Node.js, Shell)

## About This Repository

This repository contains a curated collection of example Automation Pilot commands that demonstrate the automation of various real-world scenarios relevant to SAP customers, including:

* Remediation & maintenance procedures
* Health checking and monitoring
* Root cause analysis
* Mass operations and bulk management
* Integration scenarios
* And many more operational use cases

These examples serve as starting points and learning resources for customers looking to implement automation in their own environments. They showcase best practices and common patterns while demonstrating the versatility and power of SAP Automation Pilot.

### Important Disclaimer

**Please note**: The examples provided in this repository are for **illustrative purposes** and are designed to help you understand the capabilities of SAP Automation Pilot. While these examples can be used in productive environments, it is the user's responsibility to:

* **Review and validate** each automation thoroughly before using it
* **Enhance and customize** the examples to fit your specific environment and requirements
* **Test extensively** in non-productive environments before applying to production systems

These examples are provided **as-is**. Support is available through the community for questions, additional functionalities, and bug fixes. Users should exercise due diligence when implementing these automations in their production environments.

## Learning Resources

To use the examples in this repository, you'll need access to SAP Automation Pilot. Here are the different ways to get started:

* [Tutorial: Get a Free Account on SAP BTP Trial](https://developers.sap.com/tutorials/hcp-create-trial-account.html)
* [Tutorial: Setup Automation Pilot in SAP BTP](https://blogs.sap.com/2023/01/09/setup-configuration-of-automation-pilot-in-btp-cockpit/)
* [Official Documentation](https://help.sap.com/docs/AUTOMATION_PILOT?locale=en-US)
* [Discovery Center Overview](https://discovery-center.cloud.sap/serviceCatalog/automation-pilot)
* [API Reference](https://api.sap.com/package/SAPCloudPlatformAutomationPilot/overview)
* [Interactive Tutorials](https://developers.sap.com/tutorial-navigator.html?tag=software-product%3Atechnology-platform%2Fsap-business-technology-platform%2Fsap-automation-pilot)
* [YouTube: Automation Pilot Overview](https://www.youtube.com/live/SpitmcdQVGU)
* [YouTube: HANA Cloud Automation](https://www.youtube.com/watch?v=JD16pX1-kzc)
* [YouTube: Technical Ops Automations](https://www.youtube.com/watch?v=dDoU2oVBgg0)
* [Community Blog Posts](https://blogs.sap.com/tags/73554900100800002433/)

## Getting Started

### Importing Examples into SAP Automation Pilot

Each example in this repository is packaged as a `catalog.json` file that contains all the necessary automation commands and configurations. Follow these steps to import and use any example:

#### Step 1: Choose Your Example

Browse through the [Examples](#examples) section below and select the automation scenario that fits your needs.

#### Step 2: Import the Catalog

1. Navigate to the example folder and copy the entire content of the `catalog.json` file
2. Open your Automation Pilot service
3. In the Automation Pilot interface, go to the `My Catalogs` section
4. Import the catalog:
   * Click on `Import` in the upper right corner
   * Paste the copied catalog content into the import dialog
   * Click `Import` to add the catalog to your tenant

#### Step 3: Access Your Imported Examples

After successful import, you'll see a new catalog tile labeled **"Automation Pilot Examples"** in your catalogs overview.

### Additional Resources

* [Official documentation on importing catalogs](https://help.sap.com/docs/automation-pilot/automation-pilot/managing-catalogs?locale=en-US)
* [Learn how to execute commands](https://help.sap.com/docs/automation-pilot/automation-pilot/managing-commands?locale=en-US)

:information_source: **Note**: All examples in this repository are part of the **"Automation Pilot Examples"** catalog. You only need to import each example's `catalog.json` once to access all its commands.

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
| [Run HANA Cloud Stored Procedure](run-hana-cloud-stored-procedure) | Trigger a stored procedure in HANA Cloud asynchronously and then continuously poll its status until completion |

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

### HTTP

| Example | Description |
|---------|-------------|
| [HTTP Request With OAuth Client Credentials](http-oauth-client-credentials) | Perform HTTP requests to endpoints requiring OAuth 2.0 authentication using client credentials |
| [HTTP Request via SAP Cloud Connector](http-cloud-connector) | Perform HTTP requests to internal endpoints via SAP Cloud Connector |
| [Execute a SAP Host Agent Operation via SAP Cloud Connector](sap-host-agent-via-cloud-connector) | Execute a SAP Host Agent Operation in an internal environment via SAP Cloud Connector |

### Scripting

| Example | Description |
|---------|-------------|
| [HTTP Request via Script](script-http-request) | Perform HTTP requests with large timeouts by utilizing the ExecuteScript command |
| [Use Custom Python Package](use-custom-python-package) | Install and use custom Python package in a script |
| [Use Custom NPM Package](use-custom-npm-package) | Install and use custom NPM package in a NodeJS script |
| [Use make and helm](use-make-and-helm) | Pull git repo and use make and helm to deploy the helm chart to kubernetes cluster |
| [Terraform with BTP Provider](terraform-with-btp-provider) | Use Terraform with the BTP Provider |

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

## How to obtain support

[Create an issue](https://github.com/SAP-samples/automation-pilot-examples/issues) in this repository if you find a bug or have questions about the content.

For additional support, [ask a question in SAP Community](https://answers.sap.com/questions/ask.html).

## Contributing

If you wish to contribute code, offer fixes or improvements, please send a pull request. Due to legal reasons, contributors will be asked to accept a DCO when they create the first pull request to this project. This happens in an automated fashion during the submission process. SAP uses [the standard DCO text of the Linux Foundation](https://developercertificate.org/).

## License

Copyright (c) 2023 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSE) file.
