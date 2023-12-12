# aws_ec2_self_host_runner
Create an AWS EC2 Github Action Self hosted Runner
 
 # Functions 
 - create an EC2 instance and register it as a Github self-hosted runner 
 - support spot instance. Fall back to on-demand if no spot instance found or bid price too low. 
 - auto clean runner and ec2 instance

 # Usage
 Create Github secrets for AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_REGION, AWS_SECURITY_GROUP_ID, MY_GITHUB_TOKEN (PAT, must have repo admin permission) 
 and use them in the workflow file:
```yaml
 env:
  AWS_REGION: ${{ secrets.AWS_REGION }}
  GITHUB_TOKEN: ${{ secrets.MY_GITHUB_TOKEN }}
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  SECURITY_GROUP_ID: ${{ secrets.AWS_SECURITY_GROUP_ID }}
  GITHUB_REPO: ${{ github.repository }}
  AMI_ID: ${{ github.event.inputs.ami_id }}
  INSTANCE_TYPE: ${{ github.event.inputs.instance_type }
```  

# Instructions

# Define instance parameters

- AMI_ID: The ID of the Amazon Machine Image (AMI) to use for the instance.
  - Default value: "ami-0e4d0bb9670ea8db0" (Ubuntu Server 20.04 LTS)
- INSTANCE_TYPE: The type of the instance to launch.
  - Default value: "t2.micro"
- SECURITY_GROUP_ID: The ID of the security group to associate with the instance.
  - Replace "YOUR_SECURITY_GROUP_ID" with the actual security group ID.
- GITHUB_TOKEN: The GitHub token to authenticate with the GitHub API. Must have repo admin permission.
  - Replace "YOUR_TOKEN" with the actual GitHub token.
- GITHUB_REPO: The GitHub repository in the format "owner/repo" to clone and use.
  - Default value: "sustainable-computing-io/kepler-model-server"
- REGION: The AWS region to launch the spot instance.
  - Default value: "us-east-2"
- DEBUG: Enable or disable debug mode.
  - Default value: "false"
- KEY_NAME: The name of the key pair to use for the instance.
  - Replace "YOUR_KEY_NAME" with the actual key pair name.
- GITHUB_OUTPUT: The name of the file to output the instance ID to. ***This is only for local test use. Don't set it in the workflow file.***
  - Default value: "github_output.txt"
- ROOT_VOLUME_SIZE: The size of the root volume in GB.
  - Default value: 200
- SPOT_INASTANCE_ONLY: If true, only create a spot instance.
  - Default value: "true"
- CREATE_S3_BUCKET: If true, create a S3 bucket to store the model. 
  - Default value: "false"
- BUCKET_NAME: The name of the S3 bucket to store the model.
  - Default value: The bucket name is the same as the repo name with time date stamp.
