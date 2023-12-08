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