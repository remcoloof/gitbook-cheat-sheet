# Deploy using ECR

## Instructions

### Building and testing

Build an image (ensure you are in the right directory).

```
docker build -t rds-sync .
```

Run the docker container with an image.

```
docker run -p 9000:8080 rds-sync
```

The Lambda function can now be tested.

```
curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'
```

### Deployment

Create a repository in Amazon ECR and click on "Create repository". Then authenticate the Docker CLI to your Amazon ECR registry (use the URI indicated in ECR)

```
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 2389128390.dkr.ecr.eu-central-1.amazonaws.com
```

Tag the image.

```
docker tag rds-sync:latest 2389128390.dkr.ecr.eu-central-1.amazonaws.com/rds-sync:latest
```

Push the image to Amazon ECR.

```
docker push 2389128390.dkr.ecr.eu-central-1.amazonaws.com/rds-sync:latest
```

Next, create an Lambda function with the "arm64" architecture. To ensure connectivity from an RDS instance, change the following configurations;

* Change the role by adding the "AWSLambdaVPCAccessExectionRole" policy.
* Add to the same VPC and security group (default) as the RDS instance.

### Testing

Use the test functionality of Lambda to test if the function is working properly.&#x20;

### Scheduling (optional)

If you want to schedule the Lambda function, e.g. to run a sync every 5 minutes, then you can use Amazon EventBridge. Here you need to setup a scheduling trigger.

## Additional remarks

* Note to let access RDS instances via Lambda; ensure that the RDS instance and Lambda function are in the same VPC and security group (default). Also attach this security group to the RDS instance. If you are unable to change the VPC; go to permissions; click on the execution role; and add the AWSLambdaVPCAccessExecutionRole policy to the role.&#x20;
* If the function takes a long time to execute and fails due to a timeout; change the timeout in the general configuration.&#x20;
* You can make use of environment variables using os.environ\['EXAMPLE'].  &#x20;
* Note the Lambda instance does not have access to the [internet](https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/), hence making requests will make the function timeout. To ensure that the function has access to the internet, create a NAT gateway and associate it to a subnet.&#x20;

## Resources

* [https://docs.aws.amazon.com/lambda/latest/dg/images-create.html](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)
* [https://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describ](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)
* [https://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissions](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)
* [https://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-error](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)
* [https://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.py](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)
* [https://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-database\
  https://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/\
  https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)
* [https://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3e\
  https://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809\
  https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/\
  https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/\
  ](https://docs.aws.amazon.com/lambda/latest/dg/images-create.htmlhttps://stackoverflow.com/questions/41177965/aws-lambdathe-provided-execution-role-does-not-have-permissions-to-call-describhttps://bobbyhadz.com/blog/aws-lambda-provided-execution-role-does-not-have-permissionshttps://stackoverflow.com/questions/68247643/aws-lambda-alpine-python-container-shows-image-launch-error-exec-format-errorhttps://github.com/grantcooksey/aws-lambda-python-examples/blob/master/examples/query\_database/src/query\_database/app.pyhttps://stackoverflow.com/questions/70622018/psycopg2-on-aws-lambda-not-connecting-to-rds-databasehttps://ao.ms/the-provided-execution-role-does-not-have-permissions-to-call-createnetworkinterface-on-ec2/https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.htmlhttps://medium.com/@philippholly/aws-lambda-enable-outgoing-internet-access-within-vpc-8dd250e11e12#.bhx40hq3ehttps://stackoverflow.com/questions/42312496/aws-lambda-using-firebase-admin-initializeapp-timeout/42329809#42329809https://aws.amazon.com/premiumsupport/knowledge-center/internet-access-lambda-function/https://blog.theodo.com/2020/01/internet-access-to-lambda-in-vpc/)

\
