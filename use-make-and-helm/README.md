# Use Make and Helm

Table of Contents

- [Use Make and Helm](#use-make-and-helm)
  - [Description](#description)
  - [Requirements](#requirements)
  - [How to use](#how-to-use)
  - [Cleaning up](#cleaning-up)

## Description

SAP Automation Pilot has the functionality to run scripts in an isolated Linux environment which provides a large array of useful tools and runtimes including **kubectl**, **make** and **helm**. It migth be useful to pull a git repo, containing a helm chart project, build it and deploy it to a kubernetes cluster.

This examples show how to configure your access to git and kubernetes cluster. Clone a repository containing helm project that builds with make. Build a make target and deploy a helm chart to kubernetes cluster.

The example helm chart deploys a simple busy box deployment with a single replica to the default namespace.

DISCLAIMER: the **make** tool is restricted to the current user and all security restrictions apply to any task that **make** tries to execute, so only **make** targets that do not require more privileges than the provided user can be leveraged in that way.

DISCLAIMER: the script execution time is limited, so any long running jobs will not be able to finish.

Please refer to the [documentation](https://help.sap.com/docs/automation-pilot/automation-pilot/executescript-version-2) for more details about the Execute Script functionality in Automation Pilot.

## Requirements

Base64 encoded kubeconfig with access to a kubernetes cluster.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. 
- Navigate to the **Kubeconfig** input and put your base64 encoded kubeconfig as the **kubeconfig** value.
- Navigate to the **HelmExample** command and trigger it to see it in action.
  
**OPTIONAL**: 
- If you wish to use a different GIT repository than the provided one you can navigate to the **GitAccess** input and
  - put an [access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) with read permissions as the **token** value
  - put the address of the repository to use without the protocol
- You can then go to the **HelmExample** command and modify
  - **helmProjectPath** input key to point to the root directory of your helm project after cloning
  - **makeTarget** to use your desired **make** target

## Cleaning up
To clean up the example resources on your kubernetes cluster you can trigger the **HelmExample** command with **uninstall_app** as the **makeTarget** input, or alternatively a cleanup target of your custom repository if you have configured one.
