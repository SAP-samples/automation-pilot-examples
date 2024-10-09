# Receive notifications about Cloud Foundry resources utilization via SAP Alert Notification service

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [Prerequisites](#prerequisites)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

This command allows you to get insights about the resource utilization in your Cloud Foundry runtime, like memory consumption and service usage in your Cloud Foundry space and its parent Cloud Foundry organization. 
Forward the insights towards your [SAP Alert Notification service](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/what-is-sap-alert-notification-service-for-sap-btp) account where you can subscribe for events regarding your resource consumption.
By using an appropriate configuration you could get informed about detailed resource usage, and you can also be notified when your resource usage is close the quota defined for your space and organization as well.
The event which will be triggered towards your SAP Alert Notification instance is described in the following [documentation](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/resource-quota-utilization-events?locale=en-US#technical-details). On top of that you can get notified about your Cloud Foundry resource consumption on regular intervals (e.g., every hour or day) by using [Scheduled Executions](https://help.sap.com/docs/automation-pilot/automation-pilot/scheduled-execution?locale=en-US). 

## Requirements

* A Cloud Foundry Runtime within SAP BTP.

* An instance of [SAP Alert Notification service instance](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/initial-setup) in the Cloud Foundry space which resource utilization metrics will be pulled.

* A technical user with **Space Auditor** and **Organization Auditor** roles in Cloud Foundry space and the corresponding organization that will be used to access the resource data in the Cloud Foundry space. For further information about user management refer to the following [documentation](https://help.sap.com/docs/btp/sap-business-technology-platform/administration-and-operations-in-cloud-foundry-environment).

## Prerequisites

* Create an instance of SAP Alert Notification service and configure a subscription that will match the [Resource quota utilization event](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/resource-quota-utilization-events?locale=en-US#technical-details).
  You can directly import the following [example Alert Notification service configuration](alert_notification_configuration.json) that will forward the resulting event from the command execution to your email.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *CheckResourceQuotaUtilization* command and trigger it.

You'll need to provide values for the following input keys:

* *ansServiceKey* - A Service key created in your SAP Alert Notification service instance. For further information check the [Credentials management page](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/credential-management)
* *region* - Technical name of your SAP BTP region, e.g. cf-eu10,cf-eu20
* *user* - The email or ID of your technical user.
* *password* - The password of your technical user.
* *spaceId* - The GUID of the Cloud Foundry space which you want to receive events for.
* *identityProvider* - Optional: origin key of your identity provider. Defaults to sap.ids.

## Expected result

We have set up a Cloud Foundry Runtime and a space with 3 instances and running 2 applications with defined memory quota on space level and organization level:

Running applications in the space:

![Running Applications](assets/applications-view.png)

Service instances created in the space:

![Service instances](assets/space-instances-view.png)

Cloud Foundry Organization quota configuration:

![Organization quota](assets/org-quota.png)

Space quota configuration:

![Space quota](assets/space-quota.png)


We have also created an SAP Alert Notification instance which has a subscription that will match events with *type* that *EQUALS* to *ResourceQuotaUtilization*:

![ANS subscription](assets/ans-subscription.png)

Once we trigger the command, it will start analyzing the usage data int the Cloud Foundry space and its corresponding organization as well.

![Command execution](assets/command-execution.png)

In a several minutes after the command has finished its execution the result of the resource utilization analysis could be observed as an email delivered via the SAP Alert Notification service:

![Email notification](assets/ans-email.png)
