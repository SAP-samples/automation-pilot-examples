# Auto Scale Neo Application

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

BTP Neo this does not provide a full-fledged and flexible autoscaling option. This example shows how to achieve such functionality. The command monitores your application and scales it up or down automatically, based on predefined rules.

Furthermore, with the help of SAP Alert Notification this command can be automatically triggered whenever the CPU load metric of your application instance reaches a critical level.

This example is described in further details by this blog post: [Application autoscaling with Automation Pilot and Alert Notification](https://community.sap.com/t5/technology-blog-posts-by-sap/application-autoscaling-with-automation-pilot-and-alert-notification-in-sap/ba-p/13520281)

## Requirements

To use this example you'll need the following:

* SAP BTP Neo subaccount with at least one Java application
* At least one quota which is necessary for the application upscaling
* OAuth client credentials with sufficient scope for application management and access to monitoring data

Check out the following resources for more information:

* [Deploying and Updating Java Applications](https://help.sap.com/docs/btp/sap-btp-neo-environment/deploying-and-updating-java-applications)
* [Using Platform APIs](https://help.sap.com/docs/BTP/ea72206b834e4ace9cd834feed6c0e09/using-platform-apis-84c881e4e30e43848b9b2f8401368020)

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *AutoScaleNeoApp* command and trigger it.

You'll need to provide values for the following input keys:

* *region* - Technical name of your SAP BTP region, e.g. neo-eu1, neo-us2
* *subAccount* - Name of your SAP BTP subaccount
* *resourceName* - Name of your Java application
* *clientId* - Neo Platform API client id
* *clientSecret* - Neo Platform API client secret
* *scaleUpThreshold* - Optional: CPU load threshold in percentage for scaling up an instance. Defaults to 70
* *scaleDownThreshold* - Optional: CPU load threshold in percentage for scaling down an instance. Defaults to 30
