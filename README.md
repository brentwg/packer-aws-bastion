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
AWS Region
AWS AMI Name
```
