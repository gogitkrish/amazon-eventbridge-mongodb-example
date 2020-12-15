# Amazon EventBridge - Partner Event integration example

This example application creates an Amazon EventBridge event bus, an associated event rule, and a Lambda function. The SAM template accepts the external partner event source name as a parameter and creates these components. When the partner event source receives an event from a linked MongoDB database trigger, it triggers the rule and invokes a Lambda function that logs the payload into Amazon CloudWatch.

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

```bash
.
├── README.MD                   <-- This instructions file
├── myeventfunction             <-- Source code for a lambda function
│   └── index.js                <-- Main Lambda handler
├── samtemplate.yaml               <-- SAM template
```

## Requirements

* AWS CLI already configured with Administrator permission
* [NodeJS 12.x installed](https://nodejs.org/en/download/)

## Installation Instructions

1. [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and login.

1. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [install the AWS Serverless Application Model CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) on your local machine.

1. Create a new directory, navigate to that directory in a terminal and enter ```https://github.com/aws-samples/amazon-eventbridge-producer-consumer-example```.

1. From the command line, run:
```
cd ./amazon-eventbridge-partnerevent-example
sam deploy --guided
```
Choose a stack name, select the desired AWS Region, and allow SAM to create roles with the required permissions. Once you have run guided mode once, you can use `sam deploy` in future to use these defaults.

## How it works

* Use the AWS CLI or AWS Lambda Console to invoke the Producer function. This places the events in `events.js` onto the default event bus in EventBridge.
* The EventBridge rule specified in `template.yaml` filters the events based upon the criteria in the `EventPattern` section.
* When the rule validates an event, it is routed to the Consumer function. This logs out the event, which you can see in CloudWatch Logs.

==============================================

Copyright 2020 Amazon.com, Inc. or its affiliates. All Rights Reserved.

SPDX-License-Identifier: MIT-0
