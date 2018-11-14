How to deploy my project in CLI

aws.cmd cloudformation validate-template --template-body file://my_eks_setup.yaml     

aws.cmd cloudformation  create-stack --stack-name test-kuber --template-body file://my_eks_setup.yaml --parameters ParameterKey=KeyName,ParameterValue=k8spair --capabilities CAPABILITY_IAM

aws.cmd cloudformation create-change-set --stack-name test-kuber --change-set-name SampleChangeSet --use-previous-template --parameters ParameterKey=KeyName,ParameterValue=k8spair --capabilities CAPABILITY_IAM

aws.cmd cloudformation delete-stack --stack-name test-kuber





aws.cmd cloudformation create-stack --stack-name test-kuber --template-body file://kubernetes-cluster-with-new-vpc.yaml --parameters ParameterKey=KeyName,ParameterValue=k8spair ParameterKey=AvailabilityZone,ParameterValue=eu-west-1b ParameterKey=AdminIngressLocation,ParameterValue=0.0.0.0/0 --capabilities CAPABILITY_IAM