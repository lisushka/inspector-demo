# Amazon Inspector Demo

## Structure

This demo will run Amazon Inspector on two `t2.micro` instances.  One of these instances is configured to run [BigBlueButton](), an open-source video-conferencing platform.  The other instance has TCP port 22 (the SSH port) open to the CIDR block `0.0.0.0/0`, making it world-readable.  The intention is to build this demo out into a larger workshop that looks at a wider variety of use-cases for Amazon Inspector, and integrates it with other AWS services.

## Try it yourself

This project builds using [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/).

1. Fork this repository to your GitHub account, and import it into your Azure Pipelines project.

1. In AWS, go to `EC2` > `Key pairs`, and create a key pair if you haven't already.

1. Replace `your-keypair` in `ec2-cf.yaml` with the name of your key pair.

1. Create an IAM user with admin permissions for EC2, CloudFormation, VPC, and Amazon Inspector.

1. Under `your IAM user` > `Security credentials`, generate an access key for your user.  We'll need this in the next step.

1. In Azure Pipelines, go to `Settings` (the cog in the bottom left) > `Service connections`, and click `New service connection`.  Select `AWS`, enter your access key and secret token, and name the connection `AWS Service Connection`.

1. Run the pipeline to see the build results.

1. Once you're done, delete the CloudFormation stack in AWS so that you aren't billed for the instances.

## To Do

- Cause pipeline to fail on high-risk vulnerabilities
- Set up a test instance with a CVE, and have the pipeline run host assessments as well as network assessments
- Pipe ARN of Inspector run to findings task, so that the run returned in the pipeline matches the run it started