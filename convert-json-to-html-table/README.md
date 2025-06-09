# Convert JSON to HTML Table

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Examples](#examples)

## Description

This example demonstrates how to convert a JSON array of objects into an HTML table. The command processes the JSON data and generates an HTML table string that can be used in web pages, embedded in emails, or other HTML-supported environments.

You can use the following approaches to send the HTML table via email:

* Create an [Email Action](https://help.sap.com/docs/alert-notification/sap-alert-notification-for-sap-btp/email-action-type?locale=en-US) with a custom template in the SAP Alert Notification service, and then send the HTML table using the [SendAnsEvent command](https://help.sap.com/docs/automation-pilot/automation-pilot/sendansevent?locale=en-US).
* Directly send the HTML table using the [SendEmail command](https://help.sap.com/docs/automation-pilot/automation-pilot/sendemail-command?locale=en-US) with HTML formatting enabled.

## Requirements

There are no specific requirements to use this example, other than having a JSON array of objects as input data.

## How to use

Import the content of the [examples catalog](catalog.json) into your Automation Pilot tenant. Navigate to the *ConvertJsonToHtmlTable* command and trigger it.

## Examples

### Basic Example

*JSON Array Input*

```json
[
  {
    "name": "John",
    "age": 30,
    "city": "New York",
    "state": "NY"
  },
  {
    "name": "Jane",
    "age": 25,
    "city": "Los Angeles",
    "state": "CA"
  },
  {
    "name": "Tom",
    "age": 35,
    "city": "Chicago",
    "state": "IL"
  },
  {
    "name": "Sue",
    "age": 40,
    "city": "Houston",
    "state": "TX"
  }
]
```

*HTML Table Result*

<table> <tr> <th>age</th><th>city</th><th>name</th><th>state</th> </tr> <tr><td>30</td><td>New York</td><td>John</td><td>NY</td></tr><tr><td>25</td><td>Los Angeles</td><td>Jane</td><td>CA</td></tr><tr><td>35</td><td>Chicago</td><td>Tom</td><td>IL</td></tr><tr><td>40</td><td>Houston</td><td>Sue</td><td>TX</td></tr> </table>

### Advanced Example

*JSON Array Input*

```json
[
  {
    "name": "OS Memory Usage",
    "state": "Ok",
    "value": 42,
    "unit": "%",
    "timestamp": 1732608880000,
    "output": "OK: MemoryValue: 42 (W> 98, C> 98) "
  },
  {
    "name": "Disk I/O",
    "state": "Ok",
    "value": 65327,
    "unit": "B/s",
    "timestamp": 1732608880000,
    "output": "OK: DiskRead: 0 B/s (W> 10000000, C> 15000000) DiskWrite: 65327 B/s (W> 10000000, C> 15000000)"
  },
  {
    "name": "Average Response Time",
    "state": "Ok",
    "value": 0,
    "unit": "ms",
    "timestamp": 1732608880000,
    "output": "JMX OK - AverageResponseTimeMin = 0ms "
  },
  {
    "name": "Certificate Validity",
    "state": "Ok",
    "value": 729,
    "unit": "days to expiration",
    "timestamp": 1732608881000,
    "output": "JMX OK - Alias = ajddef09eq; Thumbprint = BDD430E9BF9C12896C801848B5E834840B28F25C; ValidUntil = 2026-11-26T00:50:56Z; Expires in 729 days (W < 14 days, C < 7 days) "
  },
  {
    "name": "Heap Memory Usage",
    "state": "Ok",
    "value": 12,
    "unit": "%",
    "timestamp": 1732608880000,
    "output": "HeapMemoryUsage.used = 151 of 1183 MB "
  },
  {
    "name": "Busy Threads",
    "state": "Ok",
    "value": 0,
    "unit": "threads",
    "timestamp": 1732608880000,
    "output": "JMX OK - currentThreadsBusy = 0 (W > 150, C > 180) "
  },
  {
    "name": "Requests per Minute",
    "state": "Ok",
    "value": 1,
    "unit": "requests",
    "timestamp": 1732608880000,
    "output": "JMX OK - RequestsCountMin = 1 "
  },
  {
    "name": "CPU Load",
    "state": "Ok",
    "value": 11,
    "unit": "%",
    "timestamp": 1732608880000,
    "output": "OK CPUValue: 11 (W> 80, C> 90) "
  },
  {
    "name": "Used Disc Space",
    "state": "Ok",
    "value": 22,
    "unit": "%",
    "timestamp": 1732608879000,
    "output": "DISK OK - free space: / 8709 MB (76% inode=90%); /var 7152 MB (93% inode=99%); /tmp 3846 MB (99% inode=99%); /usr/sap 8705 MB (92% inode=99%);"
  }
]
```

*HTML Table Result*

<table> <tr> <th>name</th><th>output</th><th>state</th><th>timestamp</th><th>unit</th><th>value</th> </tr> <tr><td>OS Memory Usage</td><td>OK: MemoryValue: 42 (W> 98, C> 98) </td><td>Ok</td><td>1732608880000</td><td>%</td><td>42</td></tr><tr><td>Disk I/O</td><td>OK: DiskRead: 0 B/s (W> 10000000, C> 15000000) DiskWrite: 65327 B/s (W> 10000000, C> 15000000)</td><td>Ok</td><td>1732608880000</td><td>B/s</td><td>65327</td></tr><tr><td>Average Response Time</td><td>JMX OK - AverageResponseTimeMin = 0ms </td><td>Ok</td><td>1732608880000</td><td>ms</td><td>0</td></tr><tr><td>Certificate Validity</td><td>JMX OK - Alias = ajddef09eq; Thumbprint = BDD430E9BF9C12896C801848B5E834840B28F25C; ValidUntil = 2026-11-26T00:50:56Z; Expires in 729 days (W < 14 days, C < 7 days) </td><td>Ok</td><td>1732608881000</td><td>days to expiration</td><td>729</td></tr><tr><td>Heap Memory Usage</td><td>HeapMemoryUsage.used = 151 of 1183 MB </td><td>Ok</td><td>1732608880000</td><td>%</td><td>12</td></tr><tr><td>Busy Threads</td><td>JMX OK - currentThreadsBusy = 0 (W > 150, C > 180) </td><td>Ok</td><td>1732608880000</td><td>threads</td><td>0</td></tr><tr><td>Requests per Minute</td><td>JMX OK - RequestsCountMin = 1 </td><td>Ok</td><td>1732608880000</td><td>requests</td><td>1</td></tr><tr><td>CPU Load</td><td>OK CPUValue: 11 (W> 80, C> 90) </td><td>Ok</td><td>1732608880000</td><td>%</td><td>11</td></tr><tr><td>Used Disc Space</td><td>DISK OK - free space: / 8709 MB (76% inode=90%); /var 7152 MB (93% inode=99%); /tmp 3846 MB (99% inode=99%); /usr/sap 8705 MB (92% inode=99%);</td><td>Ok</td><td>1732608879000</td><td>%</td><td>22</td></tr> </table>
