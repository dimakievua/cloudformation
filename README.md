Deployment Steps
Prerequisites
This Quick Start requires a GitHub repository that contains the AWS CloudFormation templates you want to test as part of the CI/CD pipeline. Your GitHub repository must have a specific folder structure:
- A templates folder, which includes your AWS CloudFormation templates. Templatescan be in either JSON or YAML format.
- A ci folder, which includes a TaskCat configuration file named taskcat.yml and aninput parameters file. The configuration file should specifiy the template name thatneeds to be tested, the parameters file, and the tests that TaskCat should run.
For detailed information about these input files, see the TaskCat documentation.

If you want to give TaskCat a trial run, you can download and use any of the AWS CloudFormation templates and configuration files in the Quick Start GitHub organization at https://github.com/aws-quickstart.
Step 1. Prepare Your AWS Account
1. If you don’t already have an AWS account, create one at https://aws.amazon.com by following the on-screen instructions.
2. Use the region selector in the navigation bar to choose the AWS Region where you want to deploy CI/CD pipeline for AWS CloudFormation templates on AWS.
Step 2. Set Up Your GitHub Token and Collect Your Information
1. Log in to your GitHub account.
2. Follow the steps in the GitHub documentation to create a new (OAuth 2) token with the following scopes (permissions): admin:repo_hook and repo. If you already have a token with these permissions, you can use that. You can find a list of all your personal access tokens in https://github.com/settings/tokens.
3. Make a note of the following information:
- GitHub token name.
- GitHub repository name – This repository should have the folder structure and files described earlier in the Prerequisites section.
- Source branch name – This is the branch that CodePipeline should monitor for any changes.
- Release branch name – This is the branch that the source branch will be merged into after a successful test.
You will be prompted for this information when you launch the Quick Start.



aws.cmd cloudformation validate-template --template-body file://parameters.yaml
aws.cmd cloudformation create-stack --stack-name Credentials --template-body file://parameters.yaml --parameters  ParameterKey=GitHubUser,ParameterValue=dimakievua 

aws ssm put-parameter --name GITHUBTOKEN --type SecureString --value "e29e9d1524d76561e3d24b8c5ccbae4a50fda146"


Key	Value	Description	Export 		Name
GitHubUser	dimakievua	GitHub user	Credentials-GitHubUser


  MyIAMUser:
    Type: AWS::IAM::User
    Properties:
      UserName: 'MyUserName'
      LoginProfile:
        Password: '{{resolve:ssm-secure:IAMUserPassword:10}}'


aws.cmd cloudformation validate-template --template-body file://code_pipeline.yaml
aws.cmd cloudformation create-stack --stack-name Infrastructure --template-body file://code_pipeline.yaml --parameters file://test_pipeline.json --capabilities CAPABILITY_IAM
