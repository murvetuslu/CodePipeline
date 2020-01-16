# Lambda Fucntion automatically deployment with Codepipeline

## Pre-Requirement

Before running the cloudformation scripts, it should be uploaded to hello_word.zip(CodeCommitSource/hello_world.zip) file into your s3 Bucket in the root directory. The reason behind this upload is; when codecommit is created with cloudformation, codecommit gets the source from this s3 Bucket.

## Running Cloudformation Scripts

**Firstly**, create an AWS Cloudplatform stack via **CodePipeline.json** because Cloudformation stack will need some parameters to work properly. CI/CD Pipeline will be created after Cloudformation Stack Creating process is completed. 
When the codecommit source changed, codepipeline will trigger automatically and Cloudformation will create a change set with template.yml after that. For Cloudformation stack where lambda function is created, the change set will automatically execute.

**Secondly**, create another cloudformation stack via **ALbTarget.json** ApplicationLoadBalancer. Target Group and Listener(Rule) will be created with dependencies after cloudformation stack completes. You can access successfully to Lambda Function with ALB Dns name after tracking this process.

You can access to Lambda Function with ALB Dns name.

ListenerRule in ALB forward to host header. The host header is api.example.com
Example code for similation access to lambda function:

```
curl -H "Host: api.example.com" AlbDnsName
```

AlbDnsName: CFstackName-Alb-AccountID.region.elb.amazonaws.com

Pipeline is as below picture:

![Image description](https://github.com/murvetuslu/CodePipeline/blob/master/images/pipeline.PNG)
