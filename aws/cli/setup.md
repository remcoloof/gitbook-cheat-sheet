# Setup

## Instructions

In order to use the CLI of AWS use the following commands. First, attempt to login and enter the credentials.&#x20;

```
aws configure –-profile <profile_name>
```

In AWS command you can use `--profile <profile_name>`. For instance

```
aws ecr get-login-password --region us-east-1 --profile <profile_name> | docker login ....
```

## Resources

* [https://stackoverflow.com/questions/70452836/docker-push-to-aws-ecr-hangs-immediately-and-times-out](https://stackoverflow.com/questions/70452836/docker-push-to-aws-ecr-hangs-immediately-and-times-outhttps://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds-create)
* [https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds-create\
  ](https://stackoverflow.com/questions/70452836/docker-push-to-aws-ecr-hangs-immediately-and-times-outhttps://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds-create)
