# Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline
Devops — CICD Pipeline: Automate Continuous integration with AWS CodePipeline (Build and Test)


![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/92f71cd6-388e-4585-8726-1e52b41ca32e)

I take example from pipeline I created

on the automation of steps we need to release our software.

# Stages pipeline

Source, Build, Test, and Deploy.

## Source:
Could be AWS CodeCommit, Github, Bitbucket — for this demonstration i will be making use of AWS CodeCommit

## Build:
A build action this could be CodeBuild building my Buildspec.yml code or any third party integration like Jenkins

## Test:
A Test action this again could be CodeBuild running some unit tests against my code or a third party integration and then the code is ready for Deployment.

## Deploy:
For our Deploy action, we have chosen AWS CloudFormation. We could use other AWS services like, Elastic Beanstalk, AWS CodeDeploy, or third parties.

# What we will do in this part

I created a continuous integration (CI) pipeline and automate the build and now I will automate unit testing process using AWS CodePipeline.

I will also be able to set up a CI/CD pipeline that builds, tests my code every time there is a code change.

Preliously, I created I am role for CodeBuid and CodeDeploy. I created also s3 bucket to store build artifacts.

## Devops — CICD Pipeline: Unit Test with Code Build

Build phases

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/53b24539-c9b7-4f06-8915-c14c14f654e0)

I will use buildspec.yml file


## 1. CodeCommit Repo created

CodeCommit repository first called codepipeline-lambda-demo and push our code from Cloud9 IDE.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/802323ca-7154-4340-9907-587719e89065)

## 2. Download the codes files in Cloud9 IDE repository

Clone the repo in Cloud9 and upload files.

I use git commands (git clone, git add -A,  git commit -m "Add sample application file", git push)

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/69c4d54d-19ad-4928-a703-bcd00af99769)

Code files pushed in CodeCommit repo

Ok there are five files.

test_handler.py is the file of unit test code. 

Buildspec.yml is for the CodeBuild

template.yml is the CloudFormation SAM template that will create resources like API Gateway, and Lambda. Attach the API gateway with Lambda and deploy the code into the Lambda function. 

lambda_funtion.py is the file of code that will be deployed into lambda. 

lambda_payloads.json is the file of payload that will be deployed into lambda. 

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/7fd47ef7-9944-4b84-92e1-968e2d85c403)

### test_handler.py

This is the file of unit test code. 

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/d5b7e730-3e5e-4264-a0f7-7e2bc33827d9)

### buildspec.yml

This will be used in Codebuild and artifact wil save in a s3 bucket name “codepipeline-lambda-bucket-demo”. Create s3 bucket according to the buildspec.yml.

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/4b704f28-dfae-4a49-9e4c-a6528d390360)

### lambda_function.py

This is just a “Hello World” Python code deploying on lambda.

whenever I will create something to deploy in lambda I always need to do it using a “handler” function.

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/9ae74235-1a1b-4e67-86fd-8722cc33e307)

### lambda_payloads.json

This is the file of payload that will be deployed into lambda. 

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/c8fb3bbd-76ee-4292-9a18-0ecd88264833)

### template.yml

This is the template.yml file which will create a lambda function and a API Gateway(with only GET method) and deploy the code into the lambda function.

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/370f6195-96cd-4ee6-a995-58df61848517)

## 3. Run unit tests.

### Test1
In this section, I create test event in lambda console

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/157059ba-9d10-4e35-9797-f17090c3b5da)

After running the test, for the designated country, the output is correct. The output extract the field country from the imput event

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/50e5e8b3-b0bb-46cf-87eb-2b90d65b48c2)

### Test2

Suppose, I did not code it

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/09388d17-36e7-4593-9ef2-64196cda856f)

After deployement in the Build console of pipeline the test is KO

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/1ca60177-8252-430d-874d-9d3e637c7d61)

### Test3: Running the test using test_handler.py and Buildspec.yml

lambda_function.py

I code the name of the country

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/bc5ca70e-38e6-43e6-9a58-98540ca1c29e)

 Buildspec.yml

- python -m unittest discover tests: go to the tests folder to discover the test
  
 ![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/5fd7f273-cbe0-4a97-b975-79ac4e62fb08)

test_handler.py 

I add more test

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/48bcd593-9c29-4bb8-bfb4-2ec842dacac3)

 













