# Check HANA Cloud Database Audit Log Entries

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)

## Description

Auditing allows you to monitor and record selected actions performed in the SAP HANA Cloud database. It can help you achieve better security in the following ways:

* Uncover security vulnerabilities
* Show attempts to breach security

This example commands performs an SQL query to find any audit log entries that might be considered suspicious. It does so by pulling data from the [AUDIT_LOG system view](https://help.sap.com/docs/HANA_SERVICE_CF/7c78579ce9b14a669c1f3295b0d8ca16/d1fe1244d29510148f69be8b0e060dcc.html). If there is at least one such audit log entry, the execution fails with an error message:

![Screenshot](assets/audit-logs-error-message.png)

:information_source: SQL query should be modified to fit the user's needs and to better detect audit log entries which should be treated as suspicious.

## Requirements

To use this example you'll need the following:

* SAP HANA Cloud database
* User with database access
* Users with a AUDIT ADMIN, AUDIT OPERATOR, or AUDIT READ system privilege
* Allow connections from Automation Pilot to your HANA Cloud database. Use [this procedure](https://help.sap.com/docs/HANA_SERVICE_CF/cc53ad464a57404b8d453bbadbc81ceb/71eb651f84274a0cb2f2b4380df91724.html) to add the NAT IPs of the [relevant Automation Pilot region](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/4536e41c57aa442095ccbac977965f26.html)

Check out the following resources for more information:

* [Deploy SAP HANA Cloud](https://developers.sap.com/tutorials/hana-cloud-deploying.html)
* [Create Users and Manage Roles and Privileges](https://developers.sap.com/tutorials/hana-cloud-mission-trial-4.html)

## How to use

Import the content of [examples catalog](catalog.json) in your Automation Pilot tenant. Navigate to the *CheckHanaCloudAuditLogs* command and trigger it.

You'll need to provide values for the following input keys:

* *connectionUrl* - JDBC connection URL for the database
* *user* - Name of a database user
* *password* - Password for the specified database user

This command is most useful when executed every day. Automation Pilot allows executions to be automatically triggered on regular intervals - hourly, daily, weekly, monthly or yearly. You can find more details in the [documentation](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/96863a2380d24ba4bab0145bbd78e411.html).

Another important aspect is alerting. It's important to receive notifications (in the form of email, slack message, Jira ticket or other) whenever the *CheckHanaCloudAuditLogs* command finds suspicious audit log entries. This could be easily achieved with the help of SAP Alert Notification. More information can be found [here](https://help.sap.com/docs/AUTOMATION_PILOT/de3900c419f5492a8802274c17e07049/e75533639c6d4193aa8a7e7420c25f8c.html).
