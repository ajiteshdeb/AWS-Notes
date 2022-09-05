![AWS Lambda](https://digitalcloud.training/wp-content/uploads/2022/01/AWS-Lambda.jpg "AWS Lambda")

> AWS Lambda lets you run code as functions without provisioning or managing servers.

## Features
1. Run *on-demand* and limited by time - *short execution*
2. Lambda-based applications are composed of functions triggered by *events*.
3. Scaling is automated.
4. You specify the configuration information like, ammount of memory, exeecution timeout, programming language etc. when you create the function but cannot log in to the compute instances that run Lambda functions or customize the operating system or language runtime.
5. AWS Lambda allocates *CPU power proportional to the memory* you specify using the same ratio as a general purpose EC2 instance type.

## Lambda Invocations
Lambda functions can be *invoked directly* with the Lambda console, the Lambda API, the AWS SDK, the AWS CLI, AWS toolkits and other AWS services.
Lambda can be also configured to *read from* a stream or queue to invoke the function.

#### a) Direct Invocation -
	
1. **Synchronous Invocation** - 
You wait for the function to process the event and return a response. Error handling must happen client side (retries, exponential backoff, etc…).

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

#### b)  Event source mapping  (polled/read from the source) -
An event source is an AWS service or developer-created application that produces events that trigger an AWS Lambda function to run. You can *use event source mappings to process items from a stream or queue in services that don’t invoke Lambda functions directly.*

	

AWS services that Lambda reads events from -
- Kinesis Data Streams
- SQS & SQS FIFO queue
- DynamoDB Streams

> The configuration of the event source mapping for stream-based services (DynamoDB, Kinesis), and Amazon SQS, is made on the Lambda side and it's a synchronous invocation.
And for other services such as Amazon S3 and SNS, the function is invoked asynchronously, and the configuration is made on the source (S3/SNS) rather than Lambda.

## Lambda versions
When we’re ready to publish a Lambda function, we create a  version with an unique ARN (Amazon Resource Name).
- versions are numbered and starts with 1 and subsequent versions are incremented by 1.
- versions are immutable.
- version composes with function code and lambda configuration (environment variables, settings etc.).
- we work on $LATEST version and it's mutable.

> Because different versions have unique ARNs this allows us to effectively manage them for different environments like Production, Staging or Development. 
