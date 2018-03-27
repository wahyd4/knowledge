# Incident Management

## Incident dealing

It's important for a company to have a formal process about how do people dealing with those scenarios. There should some places to list all the common issues and its' solutions.
During the process, we should records the steps we have, so we can learn from this after the incident.
Company should have a on call rotation rules to have every engineers on the list and well rotated.

### Some tools

* Pagerduty - on call scheduling and incident resolution
* Datadog - metrics
* Stackdriver - logging

## Incident Training

### The purpose for doing this

* It's better to have some training before people get on call
* We can learn something from the incident training, so we can find some potential issues in production
* It's a good opportunities to have people from different teams work together to solve the issue
* Customer first. We should let customer know what happened if the issue has some impact to the customers.

### How to organise an incident training

* Have some check lists for people prepared before training
* Have a almost production like environment to do this
* Organiser triggers a issue, then ask trainees to fix the issue and investigate the root clause
* Let customers knows what happened. The other way round, the customer can give us some more information and also give us some complaint about his loss due to the incident.
* The on-call team should solve the issue as well as write down some notes to record how to deal with this.
* Escalate the severity if necessary to involve more people to help to solve this
* Give enough information to the next people when you are going to hand over it to.

## After incident

* Run a post incident review
* Write down the incident events timeline
* Provide a problem statement
* List the root cause
* List the ways of how do we prevent this happen again