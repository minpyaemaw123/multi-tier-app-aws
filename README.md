# Deploying a Multi-Tier Web Application Stack on AWS Elastic Beanstalk


## Web Application Architecture

![](imgs/architecture.png)

The application stack includes:

1. Nginx Load Balancer
2. Tomcat App Server
3. Rabbit MQ
4. Memcached
5. MySQL Database
6. GoDaddy DNS Service

## Web Application Architecture on AWS

![](imgs/aws.png)

The application stack on AWS includes:

1. Route 53
2. Amazon CloudFront
3. Amazon CloudWatch
4. S3 Bucket
5. Elastic Beanstalk
6. Active MQ
7. Elastic Cache
8. Amazon RDS (MySQL)


## Comparison of AWS Services with Traditional Application Stack Components

| **AWS Services**    | **Traditional App Stack**                  |
|----------------------|-------------------------------------------|
| **Elastic Beanstalk with ELB** | Nginx Load Balancer / Manual ELB Setup |
| **Auto Scaling**     | Manual Scaling or None                   |
| **EFS / S3**         | NFS / EFS / S3                           |
| **RDS**              | MySQL on VM / EC2 Instance               |
| **Elastic Cache**    | Memcached on VM / EC2 Instance           |
| **Active MQ**        | RabbitMQ on VM / EC2 Instance            |
| **Route 53**         | Local DNS (e.g., BIND) / GoDaddy         |
| **CloudFront**       | No CDN / Multi-DC Setup Worldwide        |


## Web Application Source Code

https://github.com/hkhcoder/vprofile-project/tree/awsrefactor

## Flow of Execution
1. [Key Pair and Security Group Setup](01%20-%20Integrating_AWS_IAM_and_ECR_with_GitHub.md)
2. [Terraform Code in IaC Vprofile Repo](02%20-%20Terraform_Code_in_iac-vprofile_repo.md)
3. [Staging Workflow for Terraform Code by GitHub Actions](03%20-%20Staging_Workflow_for_Terraform_Code_by_GitHub_Actions.md)
4. [Main Workflow for Terraform Code](04%20-%20Main_Workflow_for_Terraform_Code.md)
5. [Integrating SonarCloud with GitHub](05%20-%20Integrating_SonarCloud_with_Github.md)
6. [Workflow for APP Code](06%20-%20Workflow_for_APP_Code.md)
7. [Build Image by Docker and Publish to ECR](07%20-%20Build_Image_by_Docker_and_Publish_to_ECR.md)
8. [Using Helm Chart to Deploy Micro-service to EKS](08%20-%20Using_Helms_Charts_to_Deploy_Kubernetes_Definition_Files_to_EKS.md)
9. [Verification](09%20-%20Verfication.md)





