---
published: true
title: testing Zabbix action 
layout: post
---
This post will describe how to configure Zabbix so that you can toggle a trigger on demand from the command line, which will in turn create an event, call an action and then most importantly, send an alert to enable testing with faster feedback.

To achieve this, the following steps detail how to create a dummy text item and a trigger which will fire every time the value of the dummy items changes. Instruction is also provided for creating the required media types and actions, and finally, triggering a notification on demand using ```zabbix_sender```.

#### Create an item
First create a dummy item. Navigate to the desired host or template and select Items > Create Item.

The Zabbix trapper item type enables an agent (or in our case ```zabbix_sender```) to submit an item value to the Zabbix server at any time; without waiting for polling intervals or active check batch sends. We’ll use a simple Text value type for storing an arbitrary timestamp as follows:

* Name: Test timestamp
* Type: Zabbix trapper
*  Key: test.timestamp
* Type of information: Text
* Enabled: checked
* Click Add to save

(image will add later)

#### Create a trigger

Next create a trigger which will fire each time the value of the timestamp item changes. On your host or template, navigate to Triggers > Create trigger.

Use the ```diff()``` trigger function to identify a change in value. Also, ensure Multiple PROBLEM events generation is checked to ensure an event (and subsequent notification) is created every time the item value changes; not just the first time.

* Name: Timestamp changed
* Expression: ``` {[host/template]:test.timestamp.diff()}>0 ``` (replace host/template)
* Multiple PROBLEM events generation: checked
* Severity: Any (except Not classified)
* Click Add to save

(image will add later)

#### Create an action

Navigate to Configuration > Actions > Create action and enter a desirable name, default subject and message for your action. Select the Conditions tab and add a new condition with:

* New condition: ```Trigger = [dummy trigger]```
* Click Add to save the condition

(image will add later)

Select the Operations tab and add a new operation as follows:

* Send to Users:
* Click Add to save to the operation

(image will add later)

Finally, click Add to save the action.

#### Toggle the trigger

To put the trigger into a ```PROBLEM``` state, simply submit a value for your test item using ```zabbix_sender``` that is different to the previous value. The simplest way to generate a new value on each command line call is to embed a timestamp using ```$(date --rfc-3339=ns)```. Send a new value to the Zabbix server with the following (taking care to replace all argument values with the correct values for your environment):

    $ VALUE="$(date --rfc-3339=ns)"; zabbix_sender \
  	    --zabbix-server=127.0.0.1 \
  	    --host="Zabbix server" \
  	    --key="test.timestamp" \
  	    --value="${VALUE}"

To put the trigger back into an ```OK ```state (and cause a ‘Recovery message’ to be sent), simply resubmit the same item value by running the ```zabbix_sender``` command again without making a change to the ```VALUE``` environment variable:

    $ zabbix_sender \
  	    --zabbix-server=127.0.0.1 \
  	    --host="Zabbix server" \
  	    --key="test.timestamp" \
  	    --value="${VALUE}"