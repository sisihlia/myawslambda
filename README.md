# myawslambda

Check specs
======================
        ubuntu:~/environment/myawslambda (main) $ sam init
        
        Parameters:
        Template Source: 1 - AWS Quick Start Templates
        Package type: 2 -  Image (artifact is an image uploaded to an ECR image repository)
        Base image:  4 - amazon/python3.8-base
        Project name [sam-app]: MyHelloWorldLambda                                                      



Build Image
======================

        ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ sam build


Create and deploy lambda
======================

        ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ sam deploy --guided
        

Configuring SAM deploy
======================


        Setting default arguments for 'sam deploy'
        =========================================
        Stack Name [sam-app]: MyHelloWorldLambdaStack
        AWS Region [us-east-2]: us-east-2
        Image Repository for HelloWorldFunction: 258553770771.dkr.ecr.us-east-2.amazonaws.com/myecr  #create ECR myecr through aws console
        ![image](https://user-images.githubusercontent.com/8087964/120069153-b633db80-c084-11eb-8bbb-41c3c8bf2ea3.png)

          helloworldfunction:python3.8-v1 to be pushed to 258553770771.dkr.ecr.us-east-2.amazonaws.com/myecr:helloworldfunction-3faf7e42483f-python3.8-v1

        #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
        Confirm changes before deploy [y/N]: y
        #SAM needs permission to be able to create roles to connect to the resources in your template
        Allow SAM CLI IAM role creation [Y/n]: y
        HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
        Save arguments to configuration file [Y/n]: y
        SAM configuration file [samconfig.toml]: 
        SAM configuration environment [default]: 

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

## Test lambda

AWS Cloud9 terminal
======================
        ubuntu:~/environment/myawslambda (main) $ curl https://jmnsdz2gnc.execute-api.us-east-2.amazonaws.com/Prod/hello/ 
        {"message": "hello world"}

AWS console
 ![image](https://user-images.githubusercontent.com/8087964/120068925-71f40b80-c083-11eb-8fb2-07d1a1eb0fb1.png)
 ![image](https://user-images.githubusercontent.com/8087964/120068974-a1a31380-c083-11eb-8f95-42ded7743761.png)


AWS Lambda Function in AWS CLoud9
![image](https://user-images.githubusercontent.com/8087964/120068997-cdbe9480-c083-11eb-84b6-76e7077a7e69.png)
======================


        Loading response...
        Invocation result for arn:aws:lambda:us-east-2:258553770771:function:MyHelloWorldLambdaStack-HelloWorldFunction-5YBAaoENERjN
        Logs:
        START RequestId: daa4e6d9-e116-43de-9bd2-2d7c2b1ec141 Version: $LATEST
        END RequestId: daa4e6d9-e116-43de-9bd2-2d7c2b1ec141
        REPORT RequestId: daa4e6d9-e116-43de-9bd2-2d7c2b1ec141	Duration: 0.88 ms	Billed Duration: 1 ms	Memory Size: 128 MB	Max Memory Used: 50 MB	


        Payload:
        {"statusCode": 200, "body": "{\"message\": \"hello world\"}"}


sam local invoke
   ======================

        ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ sam local invoke
        Invoking Container created from helloworldfunction:python3.8-v1
        Building image.................
        Skip pulling image and use local one: helloworldfunction:rapid-1.19.0.

        END RequestId: 7cd008aa-754a-4c64-a9a3-dcf514331f2c
        REPORT RequestId: 7cd008aa-754a-4c64-a9a3-dcf514331f2c  Init Duration: 0.83 ms  Duration: 113.53 ms     Billed Duration: 200 ms Memory Size: 128 MB     Max Memory Used: 128 MB
        {"statusCode": 200, "body": "{\"message\": \"hello world\"}"}

sam local start-api
   ======================

        ubuntu:~/environment/myawslambda/MyHelloWorldLambda (main) $ sam local start-api
        Mounting HelloWorldFunction at http://127.0.0.1:3000/hello [GET]
        You can now browse to the above endpoints to invoke your functions. You do not need to restart/reload SAM CLI while working on your functions, changes will be reflected instantly/automatically. You only need to restart SAM CLI if you update your AWS SAM template
        2021-05-29 12:06:59  * Running on http://127.0.0.1:3000/ (Press CTRL+C to quit)


        In other terminal
        ubuntu:~/environment $ curl http://127.0.0.1:3000/hello
        {"message": "hello world"}



