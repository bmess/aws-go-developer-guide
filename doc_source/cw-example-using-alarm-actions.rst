.. Copyright 2010-2017 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _examples-cw-alarms:

##############################################
Using Alarms and Alarm Actions in |CW| with Go
##############################################

.. meta::
   :description: Use this code example to learn how to create alarms and alarm actions to change the state of your EC2 instances in Amazon Cloudwatch.
   :keywords: AWS SDK for Go examples, CloudWatch, alarm actions

These Go examples show you how to change the state of your |EC2| instances automatically based
on a |CW| alarm, as follows:

* Creating and enabling actions on an alarm
* Disabling actions on an alarm

You can download complete versions of these example files from the
:doc-examples-go:`aws-doc-sdk-examples <cloudwatch>` repository on GitHub.

.. _cw-create-alarm-actions-scenario:

The Scenario
============

You can use alarm actions to create alarms that automatically stop, terminate, reboot, or
recover your |EC2| instances. You can use the stop or terminate actions when you no
longer need an instance to be running. You can use the reboot and recover actions to
automatically reboot the instance.

In this example, Go code is used to define an alarm action in |CW| that triggers the reboot
of an |EC2| instance. The code uses the |sdk-go| to manage instances by using these methods of
:sdk-go-api-deep:`PutMetricAlarm <service/cloudwatch/#CloudWatch>` type:

* :sdk-go-api-deep:`PutMetricAlarm <service/cloudwatch/#CloudWatch.PutMetricAlarm>`
* :sdk-go-api-deep:`EnableAlarmActions <service/cloudwatch/#CloudWatch.EnableAlarmActions>`
* :sdk-go-api-deep:`DisableAlarmActions <service/cloudwatch/#CloudWatch.DisableAlarmActions>`

.. _cw-create-alarm-actions-prerequisites:

Prerequisites
=============

* You have :doc:`set up <setting-up>` and :doc:`configured <configuring-sdk>` the |sdk-go|.
* You are familiar with |CW| alarm actions. To learn more, see
  :cw-dg:`Create Alarms to Stop, Terminate, Reboot, or Recover an Instance <UsingAlarmActions>`
  in the |CW-ug|.

.. _cw-example-alarm-actions:

Creating and Enabling Actions on an Alarm
=========================================

Create a new Go file named :file:`create_enable_alarms.go`.

You must import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: example_code/cloudwatch/create_enable_alarms.go
   :lines: 15-24

Initialize a session that the SDK will use to load configuration, credentials, and
region information from the shared config file, ~/.aws/config, and create a new |EC2| service client.

.. literalinclude:: example_code/cloudwatch/create_enable_alarms.go
   :lines: 28-35

Create a metric alarm that will reboot an instance if its CPU utilization is greater
than 70 percent.

.. literalinclude:: example_code/cloudwatch/create_enable_alarms.go
   :lines: 39-50

You can use one of the default workflow actions to reboot the instance if the
alarm is triggered.

.. literalinclude:: example_code/cloudwatch/create_enable_alarms.go
   :lines: 54-68

Call ``EnableAlarmActions`` with the new alarm for the instance.

.. literalinclude:: example_code/cloudwatch/create_enable_alarms.go
   :lines: 71-

Disabling Actions on an Alarm
=============================

Create a new Go file named :file:`disable_alarm.go`.

You must import the relevant Go and |sdk-go| packages by adding the following lines.

.. literalinclude:: example_code/cloudwatch/disable_alarm.go
   :lines: 15-23

Initialize a session that the SDK will use to load configuration, credentials, and
region information from the shared config file, ~/.aws/config, and create a new |EC2| service client.

.. literalinclude:: example_code/cloudwatch/disable_alarm.go
   :lines: 27-34

Call the ``DisableAlarmActions`` method to disable the actions for this alarm.

.. literalinclude:: example_code/cloudwatch/disable_alarm.go
   :lines: 37-49
