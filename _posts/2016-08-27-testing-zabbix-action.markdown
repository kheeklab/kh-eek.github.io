---
published: false
title: testing Zabbix action 
layout: post
---
This post will describe how to configure Zabbix so that you can toggle a trigger on demand from the command line, which will in turn create an event, call an action and then most importantly, send an alert to enable testing with faster feedback.

To achieve this, the following steps detail how to create a dummy text item and a trigger which will fire every time the value of the dummy items changes. Instruction is also provided for creating the required media types and actions, and finally, triggering a notification on demand using ```zabbix_sender```.