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

## Devops — CICD Pipeline: Unit Test with Code Build

Build phases

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/53b24539-c9b7-4f06-8915-c14c14f654e0)

I will use buildspec.yml file

## CodeCommit Repo created

let's create a CodeCommit repository first called codepipeline-lambda-demo and push our code from Cloud9 IDE.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/802323ca-7154-4340-9907-587719e89065)

Clone the repo in Cloud9 and upload files.

I use git commands (git clone, git add -A,  git commit -m "Add sample application file", git push)

![image](https://github.com/felixdagnon/Devops-CICD-Pipeline-Automate-Unit-Testing-in-CodePipeline/assets/91665833/69c4d54d-19ad-4928-a703-bcd00af99769)

Code files pushed in CodeCommit repo

Ok there are three files:

Buildspec.yml is for the CodeBuild

template.yml is the CloudFormation SAM template that will create resources like API Gateway, and Lambda. Attach the API gateway with Lambda and deploy the code into the Lambda function. 

lambda_funtion.py is the file of code that will be deployed into lambda. 

lambda_payloads.json is the file of payload that will be deployed into lambda. 

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/b0f0d02d-195b-48cc-9bf5-fda79473b1c5)

### buildspec.yml

This will be used in Codebuild and artifact wil save in a s3 bucket name “codepipeline-lambda-bucket-demo”. Create s3 bucket according to the buildspec.yml.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/130be1c5-5cf7-49f5-9ce0-52e319729fab)

### lambda_function.py

This is just a “Hello World” Python code deploying on lambda.

whenever I will create something to deploy in lambda I always need to do it using a “handler” function.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/8e057892-83f6-44f0-84b6-ccf8c541bbbb)

### template.yml

This is the template.yml file which will create a lambda function and a API Gateway(with only GET method) and deploy the code into the lambda function.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/cdc82ad6-7435-4b2b-b99d-43b0c4bac920)

### lambda_payloads.json

This is the file of payload that will be deployed into lambda. 







## 1. Download the codes in Cloud9 IDE repository and explore the buildspec.yml file.



Git add: git add *
Git commit: git commit -m "added codebuild buildspec for unittests"
Git push: git push origin dev
Note When prompted for a user name and password, enter the Git credentials you noted in the part 3 of our series.

EXPLANATION

To add the buildspec.yml file to your local Git repository, run the command below.

Check the status of your local Git repository by running the command below.

Commit the buildspec.yml file to your local Git repository by running the command below.

Push the buildspec.yml file to the my-Deploying CodeCommit repository by running the command below. When prompted for the user name and password, enter the Git credentials you noted in the second exercise.

Sign in to the AWS Management Console as the myDeployingUser IAM user.

In the console, click Services, then click CodeCommit to open the CodeCommit dashboard.

Make sure you are in the same region as you have been using since the beginning of this series .

Click the my-Deploying repository.

In the left side navigation menu, click Commits. You should see your latest commit in which you pushed the buildspec.yml file to the repository.

To view the buildspec.yml file in the CodeCommit repository, click the commit ID link as shown in the screenshot below.


3. Create an Amazon S3 bucket to store build artifacts.
we will create an Amazon S3 bucket to store the temporary build artifacts that are created during the CodeBuild build. If you are familiar with Amazon S3, you may want to attempt this section by using the properties below, before reading the step-by-step instructions.

Region: US West (Oregon)
Bucket name: REPLACE_WITH_YOUR_INITIALS-tempartifacts
Note Replace REPLACE_WITH_YOUR_INITIALS in the bucket name above with your initials to make it unique.

Step by step instruction

Sign in to the console as the myDeployingUser IAM user. (see part 1 of this series for how to create this user)
In the console, click Services, then click S3 to open the Amazon S3 dashboard.
Click Create bucket.
For Bucket name, type REPLACE_WITH_YOUR_INITIALS-tempartifacts
For Region, select the same region you have been using — in my case its US West (Oregon).
Click Create.
4. Create a CodeBuild project and run unit tests.
In this section, you will create a CodeBuild project which refers to the buildspec.yml file you pushed in a previous section. CodeBuild will create a build against the latest commit of your CodeCommit repository and then run unit tests and static code analysis against the latest commit. Follow the steps below.

Sign in to the console as the myDeployingUser IAM user.
In the console, click Services, then click CodeBuild to open the CodeBuild dashboard.
Make sure you are in the same region as you were earlier mine is Oregon region.
Click Create build project.
For Project name, type UnitTests
For Source provider, select AWS CodeCommit or github if you are using github.
For Repository, select my-Deploying.
For Environment image, click Custom image.
For Environment type, select Linux.
Click Other location.
For Other location, type amazonlinux:2017.09
Scroll down, to the Buildspec section.
For Buildspec name, type BuildSpecs/unittest-buildspec.yml
In the Artifacts section, for Type, select Amazon S3.
For Bucket name, select the bucket you created in the previous section with the bucket name YOUR_INITIALS-tempartifacts.
Scroll down, leave the rest of the default settings, and click Create build project.
On the UnitTest build project page, click Start build.
Scroll down, to the Source section.
You should see the dev branch is selected.
Scroll down and click Start build. You should see that the build is in progress.
Scroll down to the Build logs section, after a few seconds you will see log messages for the build as shown in the screenshot below. CodeBuild will finish building and running the unit tests in a few minutes.
You can also see the pylint static analysis and the unit tests results in the logs details as shown in the screenshot below.


To view the output from the build, open the Amazon S3 dashboard and click the Amazon S3 bucket with bucket name similar toREPLACE_WITH_YOUR_INITIALS-tempartifacts. Drill down into the folders and you will see the code coverage report and the other output files from the build.






