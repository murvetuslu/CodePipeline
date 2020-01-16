# Lambda Fucntion automaticly deployment with Codepipeline

## Pre-Requirement

Before the run cloudformations scripts, should be upload hello_word.zip(CodeCommitSource/hello_world.zip) file in the root directory into
your s3 bucket
Because When codecommit is created with cloudformation, codecommit get source from this s3 bucket 

## How to Run

*Firstly*, create a aws cloudformation stack via CodePipeline.json.json
Cloudformation stack have some need parameters.
CI/CD pipeline was created when cloudformation stack create progress is completed.

When the codecommit source changed, codepipeline will be triggered automaticly, then Cloudformation create a chage set with template.yml
for Cloudformation stack where lambda function is created then The cange set will be automaticly executed. 


*Secondly*, create a another cloudformation stack via ALbTarget.json.json
ApplicationLoadBalancer, Target Group and Listener(Rule) was created with dependencies when cloudformation stack is completed.

You can access to Lambda Function with ALB Dns name.

ALB forward to host header. The host header api.example.com
Example code for similation access to lambda function:

curl -H "Host: api.example.com" AlbDnsName

AlbDnsName: CFstackName-Alb-AccountID.region.elb.amazonaws.com

Pipeline is as below picture:

![Image description](https://github.com/murvetuslu/CodePipeline/blob/master/images/pipeline.PNG)
