<!-- This template is the default one for all the example's README files -->

# Trigger Multiple Executions and Collect their Outputs

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

This example contains commands that achieve the following
1. Execute a command with configured input values in batches
2. Collect the created executions' output values
3. Delete the created executions

## Requirements

To use this example you'll need the following:

The user and password of a SAP Automation Pilot service account with Read, Write, and Execute permissions.

## How to use

1. Import the catalog
2. Trigger the `TriggerAndCollectOutputsBatching` command
3. View the output of the execution

## Expected result

By default the command will trigger and delete one execution of the Void command in SAP Automation Pilot.
The output for the default input values will be:
```
[{"message":"Hello"}]
```
