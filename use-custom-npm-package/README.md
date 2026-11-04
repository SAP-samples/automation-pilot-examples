# Use Custom NPM Package

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

SAP Automation Pilot has the functionality to run scripts in an isolated Linux environment which provides a large array of useful tools and runtimes including NodeJS. It's often necessary to install custom packges from the [npm registry](https://www.npmjs.com/) for functionalities that are not available in the standard NodeJS library.

This examples show how to install a custom package such as [uuid](https://www.npmjs.com/package/uuid) and how to use it to generate UUIDs. The actual script can easily be modified to fit an actual productive scenario.

Please refer to the [documentation](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/6584da7c47bb4b12834e73eb68767ce0.html) for more details about the Execute Script functionality in Automation Pilot.

## Requirements

There are no mandatory requirements.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *UseCustomNpmPackage* command and check the configuration of the *PythonScript* executor. You can also trigger the command to see it in action.
