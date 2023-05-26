# Use Custom Python Package

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

SAP Automation Pilot has the functionality to run scripts in an isolated Linux environment which provides a large array of useful tools and runtimes including Python. It's often necessary to install custom packages from the [Python Package Index (PyPi)](https://pypi.org/) for functionalities that are not available in the standard Python library.

This examples show how to install a custom package such as [requests](https://pypi.org/) and how to use it to send a simple HTTP request. The actual script can easily be modified to fit an actual productive scenario.

Please refer to the [documentation](https://help.sap.com/docs/automation-pilot/automation-pilot/executescript-version-2) for more details about the Execute Script functionality in Automation Pilot.

## Requirements

There are no mandatory requirements.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *UseCustomPythonPackage* command and check the configuration of the *PythonScript* executor. You can also trigger the command to see it in action
