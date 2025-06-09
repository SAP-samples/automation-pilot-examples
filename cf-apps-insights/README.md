# :sparkles: Cloud Foundry Apps Insights

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

Effortlessly identify the state of your Cloud Foundry applications using **CloudFoundryAppsInsights** example command, enhanced by the power of Gen AI.

Gain valuable insights into the health and performance of each of your CF applications. Verify their state and receive short summary, empowering you to take proactive measures and maintain optimal functionality.


Leveraging the capabilities of `gpt4o`, this command provides insights and useful suggestions for critical actions such as application restarts, instances increase, quota adjustments and e.g.

Here are example Cloud Foundry Apps Insights:


> 1. red-app:
> - There are 3 instances running. 
> - The states of the instances are: RUNNING, RUNNING, RUNNING. 
> - The CPU usage for the instances are: 1.78%, 1.91%, 1.61% respectively. 
> - The memory usage for the instances are: 131.4MB (0.13GB), 134.7MB (0.13GB), 129.6MB (0.13GB) respectively. 
> - The applications have been up for 50894 seconds (841.57 minutes, 14.03 hours), 55215 seconds (920.25 minutes, 15.34 hours), > 7589 seconds (126.48 minutes, 2.11 hours) respectively.
> - Suggestions: No action needed.
> 
> 2. blue-app: 
> - There is 1 instance running. 
> - The state of the instance is: RUNNING. 
> - The CPU usage is: 1.91%. 
> - The memory usage is: 133.8MB (0.13GB). 
> - The application has been up for 49579 seconds (826.32 minutes, 13.77 hours).
> - Suggestions: Consider increasing the number of instances.
> 
> 3. green-app: 
> - There are 2 instances running. 
> - The states of the instances are: RUNNING, RUNNING. 
> - The CPU usage for the instances are: 1.60%, 1.96% respectively. 
> - The memory usage for the instances are: 129.4MB (0.12GB), 126.0MB (0.12GB) respectively. 
> - The applications have been up for 49554 seconds (825.9 minutes, 13.76 hours), 59444 seconds (990.73 minutes, 16.51 hours) > respectively.
> - Suggestions: No action needed.
> 
> 4. yellow-app: 
> - There is 1 instance and it is not running. 
> - The state of the application is: DOWN. 
> - The CPU and memory usage are not available as the application is not running. 
> - The application has not been alive (uptime is 0).
> - Suggestions: The application is down, please restart the application. Also, consider increasing the number of instances.

## Requirements

To use this example you'll need the following:
* Cloud Foundry space with at least one application
* Technical user with *Space Developer* role
* Ai Core service instance with service key for authentication 
* SAP AI Launchpad application 
* Deployment for `gpt4o`

Check out the following resources for more information:
* [SAP AI Core Initial Setup](https://help.sap.com/docs/sap-ai-core/sap-ai-core-service-guide/initial-setup?locale=en-US)
* [SAP AI Core Documentation](https://help.sap.com/docs/sap-ai-core?locale=en-US)
* [Tutorial for AI Core](https://developers.sap.com/tutorials/ai-core-generative-ai.html)


## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the **CloudFoundryAppsInsights** command and trigger it.

You'll need to provide values for the following input keys:

* *deploymentId* - ID of the deployment for gpt4о which will execute the query
* *serviceKey* - Service key for the SAP AI Core service
* *region* - Technical name of your SAP BTP region, e.g. cf-eu10, cf-us20
* *subAccount* - Name of your Cloud Foundry organization
* *resourceGroup* - Name of your Cloud Foundry space
* *user* - Email or ID of your technical user
* *password* - Password of your technical user
* *identityProvider* -  Identity provider to be used

:information_source: Some of the needed information is available in your subaccount's *Overview* page under *Cloud Foundry Environment*.

:information_source:  **CloudFoundryAppsInsights** example uses model `gpt4o` and with small changes the insights can be modified in the prompt. 

:warning: Using a subaccount with fewer applications and instances enhances the accuracy of GPT model responses.