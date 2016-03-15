Introduction
============
[Amazon Web Services](https://archetypal.signin.aws.amazon.com) hosts archetypal Connect. 


Signup
======
https://www.amazon.com/ap/signin?openid.assoc_handle=aws&openid.return_to=https%3A%2F%2Fsignin.aws.amazon.com%2Foauth%3Fresponse_type%3Dcode%26client_id%3Darn%253Aaws%253Aiam%253A%253A015428540659%253Auser%252Fawssignupportal%26redirect_uri%3Dhttps%253A%252F%252Fportal.aws.amazon.com%252Fbilling%252Fsignup%253Fnc2%253Dh_ct%2526redirect_url%253Dhttps%25253A%25252F%25252Faws.amazon.com%25252Fregistration-confirmation%2526state%253DhashArgs%252523%2526isauthcode%253Dtrue%26noAuthCookie%3Dtrue&openid.mode=checkid_setup&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&action=&disableCorpSignUp=&clientContext=&marketPlaceId=&poolName=&authCookies=&pageId=aws.ssop&siteState=pre-register%2Cen_US&accountStatusPolicy=P1&sso=&openid.pape.preferred_auth_policies=MultifactorPhysical&openid.pape.max_auth_age=120&openid.ns.pape=http%3A%2F%2Fspecs.openid.net%2Fextensions%2Fpape%2F1.0&server=%2Fap%2Fsignin%3Fie%3DUTF8&accountPoolAlias=&forceMobileApp=0&language=en_US&forceMobileLayout=0

See Initial Configuration below.


Introduction
============

-Verify Setup - IAM users, roles, key pair, S3
-Clear all configurations in EC2, ECS, VPC, CloudFormation
-Login with an IAM user
-Use Wizard to create Amazon EC2 Container Service with Amazon ECS Sample
-Adjust task defnition name, servie name, select ELB for simple-app:80, select keypair, create or select IAM roles.



Command Line Interface (CLI)
============================

Install the CLI for tools to configure.  The CLI may be used for diagnostics.  
However, configuration of AWS should be done via the SDK for NodeJS

```
aws configure --pro
```



Install client:  Windows (http://docs.aws.amazon.com/cli/latest/userguide/installing.html#install-msi-on-windows)

Use aws configure --profile

SDK for Node JS
===============

https://aws.amazon.com/sdk-for-node-js/

```
npm install -g aws-sdk
```




Deploy
======
Adjust load balancer to create additional instance.
Switch task on service.


SSH
===
To SSH into an EC2 instance, ensure that there is an inboud SSH rule for the Security Group for the EC2 instance.

To SSH, must use the keypair pem file used to create the instance.  This may be present in the Launch configuration.

Example SSH login (via bash shell) which must use the Public DNS name for the ec2 instance.
```
ssh -i ~/.ssh/archetypal.pem ec2-user@<Public DNS>
```


To test launch configuration user data on an instance:

```
sudo yum install -y aws-cli
aws s3 cp s3://archetypal/docker/ecs.config /etc/ecs/ecs.config
```

Modify launch configuration to install ecs.config:

```
#!/bin/bash
yum install -y aws-cli
aws s3 cp s3://archetypal/docker/ecs.config /etc/ecs/ecs.config
```

Amazon ECS-Optimized Amazon Linux AMI


EC2 Network & Security
======================
Key Pairs -- generated keypair in order to ssh into instances.  Saved keypair encrypted to s3://archetypal/keypair.
Locally place keypair in ~/.ssh


EC2 Load Balancing
==================
Balances load among instances, external facing SSL


EC2 Auto Scaling 
================

Launch Configurations
---------------------
Configuration for instance launches.

Groups
----------------
Groups to auto scale instances.  Delete auto scaling groups before terminating instances.


EC2 Container Service
=====================

Task Definition
---------------
Defines the docker images and docker run info that will run on a single EC2 instance and security group.  
Volumes may be defined for the EC2 instance.  The tasks may be scaled to multiple instances.


Service
-------
Service binds ELB load balancer host ports to task definition images host ports and manages the 
distribution of task instances.



Docker Containers

Do default AWS instance, use ELB for port 80, select archetypal keypair.




Elastic Beanstalk
=================

S3
==
Storage buckets
archetypal is main bucket.
archetypal/docker - docker credentials for ECS/EB



CloudFormation
==============
Templates for building cloud services



Initial Configuration:

IAM
===
Created IAM link -- https://archetypal.signin.aws.amazon.com/console For users to login
bt IAM user with AdministratorAccess group

Generated:
ecsServiceRole
ecsInstanceRole

Created S3DockerConfigReadOnlyAccess policy attached to ecsInstanceRole:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": "arn:aws:s3:::archetypal/docker/*"
        }
    ]
}
```


Virtual Private Cloud
=====================
Create default VPC named archetypal using the wizard which will create default security group.

Internet Gateways
=================
Expose VPC to internet.
http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html

Route Tables
============

Elastic IPs
===========
Create ip for instance


Install Docker
==============

Debian

Remote in as admin@ip.

Need to modify hosts to add hostname:

```
cat /etc/hostname
sudo pico /etc/hosts
```

Add hostname mapping to 127.0.0.1 in /etc/hosts:
```
127.0.0.1   ip-10-0-0-208
```

To add docker

```
sudo apt-get update
sudo apt-get install -y curl
sudo groupadd -g 497 docker
sudo usermod -a -G docker admin
sudo curl -sSL https://get.docker.com/ | sh
```

Check



http://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html#install_docker

Docker instructions (reference)
```
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker ec2-user
```

After adding to group, logout and back in again.


SES
===
Ses setup with DKIM otherwise recipients may see amazonses as a third party sender.  Modified DNS.  Need to request rate limit.

