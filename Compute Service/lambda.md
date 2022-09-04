# AWS Lambda

> AWS Lambda lets you run code as functions without provisioning or managing servers.

#### Features
1. Run *on-demand* and limited by time - *short execution*
2. Lambda-based applications are composed of functions triggered by *events*.
3. Scaling is automated.
4. You specify the configuration information like, ammount of memory, exeecution timeout, programming language etc. when you create the function but cannot log in to the compute instances that run Lambda functions or customize the operating system or language runtime.
5. AWS Lambda allocates *CPU power proportional to the memory* you specify using the same ratio as a general purpose EC2 instance type.

#### Lambda Invocations
Lambda functions can be *invoked directly* with the Lambda console, the Lambda API, the AWS SDK, the AWS CLI, AWS toolkits and other AWS services.
Lambda can be also configured to *read from* a stream or queue to invoke the function.

1. **Synchronous Invocation** - 
You wait for the function to process the event and return a response. Error handling must happen client side (retries, exponential backoff, etc…)

	 **User Invoked**:
• Elastic Load Balancing (Application Load Balancer)
• Amazon API Gateway
• Amazon CloudFront (Lambda@Edge)
• Amazon S3 Batch
	 **Service Invoked**:
• Amazon Cognito
• AWS Step Functions
	 **Other Services**:
• Amazon Lex
• Amazon Alexa
• Amazon Kinesis Data Firehose

2. **Asynchronous Invocation**:
you do not wait for a response from the function code. Lambda attempts to retry on errors.

	Lambda first places the event in a queue called "**Event Queue**" and returns a success response without additional information,  then a separate process reads events from the queue and sends them to your function. In case of failures *lambda function retries 3 times in total, 1 minute wait after 1st , then 2 minutes wait*. you will see duplicate logs entries in CloudWatch Logs in such cases.

	• Amazon Simple Storage Service (S3)
• Amazon Simple Notification Service (SNS)
• Amazon CloudWatch Events / EventBridge
• AWS CodeCommit (CodeCommitTrigger: new branch, new tag, new push)
• AWS CodePipeline (invoke a Lambda function during the pipeline, Lambda must callback)
• Amazon CloudWatch Logs (log processing)
• Amazon Simple Email Service
• AWS CloudFormation
• AWS Config
• AWS IoT
• AWS IoT Events

