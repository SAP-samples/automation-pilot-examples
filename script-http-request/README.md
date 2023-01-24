# HTTP Request via Script

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

Automation Pilot provides the [*HttpRequest*](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/6ce1e04b7812411db04b80ea769ef46e.html) command which allows customers to perform arbitrary HTTP request to any public endpoint. Its flexibility and simplicity provides a way to use and automate most modern HTTP APIs.

To ensure scalability and optimal performance for all Automation Pilot customers, the *HttpRequest* command has a strict limit on the maximum time that each request can take, as well as limit on the response size.

However, some customer scenarios require working with synchronous HTTP APIs. Request to such APIs might take minutes to complete. Similar requirements could also apply to the response size.

Automation Pilot enables such scenarios with the [*ExecuteScript*](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/d0854dbb80d84946bb57791db94b7e20.html) command. It can be used to run scripts in a fully isolated environment. These scripts can run for up to 5 minutes with limited set of computing, memory and storage resources.

The supported runtimes include bash, python, node.js and provides access to popular CLI tools including curl, jq, and git.

This example command has very similar contract to the original *HttpRequest*. However, its implementation is base entirely on *ExecuteScript* by utilizing [curl](https://curl.se/) and [jq](https://stedolan.github.io/jq/). It could be used to send requests to slow synchronous APIs and to work with larger response bodies.

:warning: *ExecuteScript* has [some limitations](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/d0854dbb80d84946bb57791db94b7e20.html) described in the documentation. They also apply to this example command.

## Requirements

There are no mandatory requirements. This command can perform HTTP requests to any public endpoint.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *ScriptHttpRequest* command and trigger it.

You'll need to provide values for the following input keys:

* *method* - Request method to use
* *url* - URL to which to send the request
* *body* - Optional: Request body to send with the request
* *headers* - Optional: Request headers to send with the request
* *timeout* - Optional: Maximum time that the request can take. Defauls to 60 seconds. Maximum allowed value is 240 seconds.
* *user* - Optional: User name to use for server authentication
* *password* - Optional: Password to use for server authentication
* *authorizationHeader* - Optional: Explicit value for the HTTP authorization header. Overwrites all other forms of authentication
* *responseBodyTransformer* - Optional: JQ expression to transform the response body with. The format must follow the one described in https://github.com/stedolan/jq
