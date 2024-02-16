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







