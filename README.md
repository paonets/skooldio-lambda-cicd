Welcome to the AWS Lambda Workshop by Skooldio
==============================================

## Getting Started
This repository is a modified version of CodeStar Express.js Lambda project which includes PreTraffic hook. Just copy following files to your AWS CodeStar project.
```shell
preTrafficHook.js
template.yml
```
Once you push the code, it should automatically get built and deployed by AWS CodePipeline.

You might run into issue when deploying new code since your CloudFormation does not have permission to perform some operations. You will need to add proper permission to CloudFormation's IAM role. You can find the name of CloudFormation's IAM role in *Stack info* tab in AWS CloudFormation console. Go to that IAM Role and attach following policies:
* ```IAMFullAccess```
* ```AWSCodeDeployFullAccess```

## Simulating Deployment Failure

The PreTraffic hook checks that ```GET / ``` returns 200. You can simulate failure by modifying your ```app.js``` to return 500 instead.
```javascript
res.status(500).send('Something broke!')
```
The deployment should fail due to validation by PreTraffic hook.

## Trying Linear or Canary deployment
Once the deployment succeeded, you can try other types of deployment preference. In ```template.yml```, you can see other types which got commented out. Try one of those types and see the result in [CodeDeploy](https://ap-southeast-1.console.aws.amazon.com/codesuite/codedeploy/deployments?region=ap-southeast-1) console.