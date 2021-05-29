# myawslambda


## Start lambda
ubuntu:~/environment/myawslambda (main) $ sam init
Which template source would you like to use?
        1 - AWS Quick Start Templates
        2 - Custom Template Location
Choice: 1
What package type would you like to use?
        1 - Zip (artifact is a zip uploaded to S3)
        2 - Image (artifact is an image uploaded to an ECR image repository)
Package type: 2

Which base image would you like to use?
        1 - amazon/nodejs14.x-base
        2 - amazon/nodejs12.x-base
        3 - amazon/nodejs10.x-base
        4 - amazon/python3.8-base
        5 - amazon/python3.7-base
        6 - amazon/python3.6-base
        7 - amazon/python2.7-base
        8 - amazon/ruby2.7-base
        9 - amazon/ruby2.5-base
        10 - amazon/go1.x-base
        11 - amazon/java11-base
        12 - amazon/java8.al2-base
        13 - amazon/java8-base
        14 - amazon/dotnet5.0-base
        15 - amazon/dotnetcore3.1-base
        16 - amazon/dotnetcore2.1-base
Base image: 4

Project name [sam-app]: MyHelloWorldLambda                                                      

Cloning app templates from https://github.com/aws/aws-sam-cli-app-templates

AWS quick start application templates:
        1 - Hello World Lambda Image Example
        2 - PyTorch Machine Learning Inference API
        3 - Scikit-learn Machine Learning Inference API
        4 - Tensorflow Machine Learning Inference API
        5 - XGBoost Machine Learning Inference API
Template selection: 1

    -----------------------
    Generating application:
    -----------------------
    Name: MyHelloWorldLambda
    Base Image: amazon/python3.8-base
    Dependency Manager: pip
    Output Directory: .

    Next steps can be found in the README file at ./MyHelloWorldLambda/README.md
    

ubuntu:~/environment/myawslambda (main) $ cd MyHelloWorldLambda/
ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ ls
README.md  __init__.py  events  hello_world  template.yaml  tests
ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ sam build
Building codeuri: . runtime: None metadata: {'Dockerfile': 'Dockerfile', 'DockerContext': './hello_world', 'DockerTag': 'python3.8-v1'} functions: ['HelloWorldFunction']
Building image for HelloWorldFunction function
Setting DockerBuildArgs: {} for HelloWorldFunction function
Step 1/4 : FROM public.ecr.aws/lambda/python:3.8
 ---> b1aec550dac9
Step 2/4 : COPY app.py requirements.txt ./
 ---> 7b16f4bc98a9
Step 3/4 : RUN python3.8 -m pip install -r requirements.txt -t .
 ---> Running in 61c9c530c90f
Collecting requests
  Downloading requests-2.25.1-py2.py3-none-any.whl (61 kB)
Collecting chardet<5,>=3.0.2
  Downloading chardet-4.0.0-py2.py3-none-any.whl (178 kB)
Collecting idna<3,>=2.5
  Downloading idna-2.10-py2.py3-none-any.whl (58 kB)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.5-py2.py3-none-any.whl (138 kB)
Collecting certifi>=2017.4.17
  Downloading certifi-2020.12.5-py2.py3-none-any.whl (147 kB)
Installing collected packages: urllib3, idna, chardet, certifi, requests
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.5
WARNING: Running pip as root will break packages and permissions. You should install packages reliably by using venv: https://pip.pypa.io/warnings/venv
WARNING: You are using pip version 21.1.1; however, version 21.1.2 is available.
You should consider upgrading via the '/var/lang/bin/python3.8 -m pip install --upgrade pip' command.
 ---> a23dd68c27c7
Step 4/4 : CMD ["app.lambda_handler"]
 ---> Running in f5da3374b915
 ---> 3faf7e42483f
Successfully built 3faf7e42483f
Successfully tagged helloworldfunction:python3.8-v1

Build Succeeded

Built Artifacts  : .aws-sam/build
Built Template   : .aws-sam/build/template.yaml

Commands you can use next
=========================
[*] Invoke Function: sam local invoke
[*] Deploy: sam deploy --guided

ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ sam deploy --guided

Configuring SAM deploy
======================

        Looking for config file [samconfig.toml] :  Not found

        Setting default arguments for 'sam deploy'
        =========================================
        Stack Name [sam-app]: MyHelloWorldLambdaStack
        AWS Region [us-east-2]: us-east-2
        Image Repository for HelloWorldFunction: 258553770771.dkr.ecr.us-east-2.amazonaws.com/myecr  #create ECR myecr through aws console
          helloworldfunction:python3.8-v1 to be pushed to 258553770771.dkr.ecr.us-east-2.amazonaws.com/myecr:helloworldfunction-3faf7e42483f-python3.8-v1

        #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
        Confirm changes before deploy [y/N]: y
        #SAM needs permission to be able to create roles to connect to the resources in your template
        Allow SAM CLI IAM role creation [Y/n]: y
        HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
        Save arguments to configuration file [Y/n]: y
        SAM configuration file [samconfig.toml]: 
        SAM configuration environment [default]: 

        Looking for resources needed for deployment: Not found.
        Creating the required resources...
        Successfully created!

                Managed S3 bucket: aws-sam-cli-managed-default-samclisourcebucket-hyn8fotjq3l6
                A different default S3 bucket can be set in samconfig.toml

        Saved arguments to config file
        Running 'sam deploy' for future deployments will use the parameters saved above.
        The above parameters can be changed by modifying samconfig.toml
        Learn more about samconfig.toml syntax at 
        https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-config.html

The push refers to repository [258553770771.dkr.ecr.us-east-2.amazonaws.com/myecr]
d0658a1ccbf4: Pushed 
8cc473776aa9: Pushed 
66b7350aa423: Pushed 
61f3cc4518fd: Pushed 
d6fa53d6caa6: Pushed 
8de44aa80f89: Pushed 
a9165ff9bec4: Pushed 
06019287a34a: Pushed 
helloworldfunction-3faf7e42483f-python3.8-v1: digest: sha256:bc841c82ae7a47e5e4b6c22a234d3e4467c8fd435a531a19a7b152e9d596246e size: 1999


        Deploying with following values
        ===============================
        Stack name                   : MyHelloWorldLambdaStack
        Region                       : us-east-2
        Confirm changeset            : True
        Deployment image repository  : 
                                       {
                                           "HelloWorldFunction": "258553770771.dkr.ecr.us-east-2.amazonaws.com/myecr"
                                       }
        Deployment s3 bucket         : aws-sam-cli-managed-default-samclisourcebucket-hyn8fotjq3l6
        Capabilities                 : ["CAPABILITY_IAM"]
        Parameter overrides          : {}
        Signing Profiles             : {}

Initiating deployment
=====================
HelloWorldFunction may not have authorization defined.
Uploading to MyHelloWorldLambdaStack/1ada58cd3d43d06885b705600ac4b5e4.template  1167 / 1167  (100.00%)

Waiting for changeset to be created..

CloudFormation stack changeset
-------------------------------------------------------------------------------------------------------------------------------------------------
Operation                            LogicalResourceId                    ResourceType                         Replacement                        
-------------------------------------------------------------------------------------------------------------------------------------------------
+ Add                                HelloWorldFunctionHelloWorldPermis   AWS::Lambda::Permission              N/A                                
                                     sionProd                                                                                                     
+ Add                                HelloWorldFunctionRole               AWS::IAM::Role                       N/A                                
+ Add                                HelloWorldFunction                   AWS::Lambda::Function                N/A                                
+ Add                                ServerlessRestApiDeployment47fc2d5   AWS::ApiGateway::Deployment          N/A                                
                                     f9d                                                                                                          
+ Add                                ServerlessRestApiProdStage           AWS::ApiGateway::Stage               N/A                                
+ Add                                ServerlessRestApi                    AWS::ApiGateway::RestApi             N/A                                
-------------------------------------------------------------------------------------------------------------------------------------------------

Changeset created successfully. arn:aws:cloudformation:us-east-2:258553770771:changeSet/samcli-deploy1622284035/378f5358-30ad-4802-a1d8-fc1d1faccac3


Previewing CloudFormation changeset before deployment
======================================================
Deploy this changeset? [y/N]: y

2021-05-29 10:27:25 - Waiting for stack create/update to complete

CloudFormation events from changeset
-------------------------------------------------------------------------------------------------------------------------------------------------
ResourceStatus                       ResourceType                         LogicalResourceId                    ResourceStatusReason               
-------------------------------------------------------------------------------------------------------------------------------------------------
CREATE_IN_PROGRESS                   AWS::IAM::Role                       HelloWorldFunctionRole               Resource creation Initiated        
CREATE_IN_PROGRESS                   AWS::IAM::Role                       HelloWorldFunctionRole               -                                  
CREATE_COMPLETE                      AWS::IAM::Role                       HelloWorldFunctionRole               -                                  
CREATE_IN_PROGRESS                   AWS::Lambda::Function                HelloWorldFunction                   -                                  
CREATE_IN_PROGRESS                   AWS::Lambda::Function                HelloWorldFunction                   Resource creation Initiated        
CREATE_COMPLETE                      AWS::Lambda::Function                HelloWorldFunction                   -                                  
CREATE_IN_PROGRESS                   AWS::ApiGateway::RestApi             ServerlessRestApi                    -                                  
CREATE_IN_PROGRESS                   AWS::ApiGateway::RestApi             ServerlessRestApi                    Resource creation Initiated        
CREATE_COMPLETE                      AWS::ApiGateway::RestApi             ServerlessRestApi                    -                                  
CREATE_IN_PROGRESS                   AWS::Lambda::Permission              HelloWorldFunctionHelloWorldPermis   -                                  
                                                                          sionProd                                                                
CREATE_IN_PROGRESS                   AWS::Lambda::Permission              HelloWorldFunctionHelloWorldPermis   Resource creation Initiated        
                                                                          sionProd                                                                
CREATE_IN_PROGRESS                   AWS::ApiGateway::Deployment          ServerlessRestApiDeployment47fc2d5   -                                  
                                                                          f9d                                                                     
CREATE_COMPLETE                      AWS::ApiGateway::Deployment          ServerlessRestApiDeployment47fc2d5   -                                  
                                                                          f9d                                                                     
CREATE_IN_PROGRESS                   AWS::ApiGateway::Deployment          ServerlessRestApiDeployment47fc2d5   Resource creation Initiated        
                                                                          f9d                                                                     
CREATE_IN_PROGRESS                   AWS::ApiGateway::Stage               ServerlessRestApiProdStage           -                                  
CREATE_IN_PROGRESS                   AWS::ApiGateway::Stage               ServerlessRestApiProdStage           Resource creation Initiated        
CREATE_COMPLETE                      AWS::ApiGateway::Stage               ServerlessRestApiProdStage           -                                  
CREATE_COMPLETE                      AWS::Lambda::Permission              HelloWorldFunctionHelloWorldPermis   -                                  
                                                                          sionProd                                                                
CREATE_COMPLETE                      AWS::CloudFormation::Stack           MyHelloWorldLambdaStack              -                                  
-------------------------------------------------------------------------------------------------------------------------------------------------

CloudFormation outputs from deployed stack
-------------------------------------------------------------------------------------------------------------------------------------------------
Outputs                                                                                                                                         
-------------------------------------------------------------------------------------------------------------------------------------------------
Key                 HelloWorldFunctionIamRole                                                                                                   
Description         Implicit IAM Role created for Hello World function                                                                          
Value               arn:aws:iam::258553770771:role/MyHelloWorldLambdaStack-HelloWorldFunctionRole-1BK4MOKDWKZ7W                                 

Key                 HelloWorldApi                                                                                                               
Description         API Gateway endpoint URL for Prod stage for Hello World function                                                            
Value               https://jmnsdz2gnc.execute-api.us-east-2.amazonaws.com/Prod/hello/                                                          

Key                 HelloWorldFunction                                                                                                          
Description         Hello World Lambda Function ARN                                                                                             
Value               arn:aws:lambda:us-east-2:258553770771:function:MyHelloWorldLambdaStack-HelloWorldFunction-5YBAaoENERjN                      
-------------------------------------------------------------------------------------------------------------------------------------------------

Successfully created/updated stack - MyHelloWorldLambdaStack in us-east-2  #check CFN and Lambda, they are well created

##Testing



