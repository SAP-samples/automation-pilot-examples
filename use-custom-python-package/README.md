# Use Custom Python Package

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

SAP Automation Pilot has the functionality to run scripts in an isolated Linux environment which provides a large array of useful tools and runtimes including Python. It's often necessary to install custom packages from the [Python Package Index (PyPi)](https://pypi.org/) for functionalities that are not available in the standard Python library.

This examples show how to install a custom package such as [requests](https://pypi.org/) and how to use it to send a simple HTTP request. The actual script can easily be modified to fit an actual productive scenario.

Please refer to the [documentation](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/6584da7c47bb4b12834e73eb68767ce0.html) for more details about the Execute Script functionality in Automation Pilot.

## Requirements

There are no mandatory requirements.

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *UseCustomPythonPackage* command and check the configuration of the *PythonScript* executor. You can also trigger the command to see it in action


## Method 2
The following method can also be used for installing additional packages from the python script runtime.

```sh
#!/usr/bin/env python3
import sys
import subprocess
subprocess.call('pip install requests --no-warn-script-location', shell=True, stdout=subprocess.PIPE)  # Install the required package
result = subprocess.check_output("pip show requests | grep Location | cut -d ' ' -f 2-", shell=True) # Fetches the path for the installed package (to avoid hardcoding)
location = result.decode("utf-8").strip()  # Convert bytes to string and remove leading/trailing spaces
sys.path.append('{}'.format(location)) # Adds the package path to the PATH variable
import requests # Now you can import the package in the same script
.. the rest of your code ..
```


