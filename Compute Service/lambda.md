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

