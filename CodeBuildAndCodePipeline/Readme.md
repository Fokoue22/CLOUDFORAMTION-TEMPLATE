# Deploying CodeBuild and CodePipeline with CloudFormation

Managing the AWS developer tools with cloud formation helps speed up initial environment and deployment setup processes. This example deploys a CodeCommit Repository, two CodeBuild jobs, and then creates a CodePipeline which uses continuous integration to run any time changes are pushed to the code commit repository. The templates provided can be expanded to create multiple CodeBuild jobs or add additional environments to the CodePipeline stages. Using these CloudFormation templates will be considerably faster than working through the required menus to deploy the jobs and pipelines through the AWS console.

## Cloud Formation Templates

This example contains two CloudFormation templates.

### codebuild-template.yml

This template must be deployed first as the cloudformation-codepipeline-template has dependencies on the output of this template. This template deploys the following resources

 - An S3 storage account for holding build artifacts
 - App-build CodeBuild project for running scripts and commands to build the application
 - App-deploy CodeBuild Project for running scripts and commands to deploy the application
 - Required IAM roles for the codebuild to create logs in cloudwatch and s3, create objects in s3, and create reports

## fullcd-codepipeline-template.yml

This template deploys the pipeline which is triggered on a commit to main. It has 3 stages

1. app-build stage - executes the app-build CodeBuild job
2. Manual approval stage - requires manual approval
3. app-deploy stage - executes the app-deploy CodeBuild job

