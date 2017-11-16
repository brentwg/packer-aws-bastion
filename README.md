# Packer - AWS Bation AMI
Packer script used to create my default Bastion AMI

## Quickstart
Step 1:  
Source the aws.env file
```
source aws.env
```  
Step 2:  
Validate the Packer template file  
```
packer validate packer-bastion.json
```  
Step 3:  
Build and deploy the AWS AMI  
```
packer build packer-bastion.json
```  

## AWS Credentials
To manage AWS credential, I use a program called `pass`. For more information about `pass` see the following link:  
- [The Standard Unix Password Manager: Pass](https://www.passwordstore.org/)  

The `aws.env` file queries `pass` and sets environment variables for the following information:  
```
AWS Access Key (for both the AWS cli)
AWS Secret Key (for both the AWS cli)

Non-pass info:
AWS Region
AWS AMI Name
```

**NOTE**: Change the `aws.env` values (ie `"$(pass aws-brentwg/access-key)"`) for each variable to match those in your own AWS environment.


## Packer Template Variables and Settings
Packer template variables are listed below. Please set appropriate values for your own environment.  

```
aws_access_key
aws_secret_key
aws_region
ami_name
```  
Other template settings include the following:  
```
instance_type
ssh_username
```

## Provisioning
The following automations are performed by the template:  

1. Python `pip` will install the latest version of `ansible`  
1. Ansible will run a playbook called `playbook.yaml`  
1. And the `root` account is stripped of any authorized SSH keys  

`playbook.yaml` executes the following actions:  
- all outstanding software updates are applied  
- [ClamAV](https://www.clamav.net/) is installed and configured  
- An [O/S hardening](https://github.com/dev-sec/ansible-os-hardening) role is applied  
- The AWS CloudWatch installation and configuration [role](https://github.com/dharrisio/ansible-role-aws-cloudwatch-logs-agent) is applied  