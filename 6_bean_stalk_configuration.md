# Elastic Beanstalk Setup

1. Create IAM Role for the Beanstalk.
	
	This role is necessary for Beanstalk to interact with related AWS Services. 

	Role Name: bean-role
	
	Policies Attached: 
	
	- AWSElasticBeanstalkWebTier
	
	- AdministratorAccess-AWSElasticBeanstalk
	
	- AWSElasticBeanstalkRoleSNS
	
	- AWSElasticBeanstalkCustomPlatformforEC2Role
	
	![](imgs/IAM_Role_for_EBS.png)
	
	![](imgs/IAM_Role_for_EBS_2.png)
	
	![](imgs/IAM_Role_for_EBS_3.png.png)
	
2. Create Application in Elastic Beanstalk
	
	As we are deploying web app, **Web server environment** is used.
	
	Application Name: demo-web-app
	
	Domain: demo-web-app-mpm21	
	
	![](imgs/ebs-1.png)
	
	In **Platform**, **Tomcat** is used.
	
	We select **Tomcat 9 with Correct 11** to be compatible with the web app source code.
	
	![](imgs/ebs-2.png)
	
	![](imgs/ebs-3.png)
	
	In **Service Access**, Select **Create and use new service role**.
	**aws-elasticbeanstalk-service-role** will be created
	
	And select the role we created **bean-role** for EC2 instance profile.
	
	![](imgs/ebs-4.png)
	
	For **VPC and Subnets**, Default VPC and all subnets are selected.
	
	![](imgs/ebs-5.png)
	
	Please select all availability zones for **Database**

	![](imgs/ebs-6.png)
	
	Provide the tags for categorization.
	
	![](imgs/ebs-7.png)
	
	
	![](imgs/ebs-8.png)
	
	For security group, **backend-sg** is used for internal communications with the previous services we configured.
	
	![](imgs/ebs-9.png)
	
	In **Auto Scaling**, **Load Balanced** is used.
	
	Here, we define **Min 2 instances and Max 4** instances with On-Demand instances.
	
	![](imgs/ebs-10.png)
	
	As we are doing the lab for demo purpose, **t3.micro** instance type is used.
	
	As we examine the default **AMI ID** of Elastic Beanstalk, we find the customized Elastic Beanstalk AMI is used.
	
	![](imgs/ebs-11.png)
	
	![](imgs/ebs-12.png)
	
	![](imgs/ebs-13.png)
	
	![](imgs/ebs-14.png)
	
	![](imgs/ebs-15.png)
	
	For **Listeners**, we keep default first and later will come back here and edit.
	
	![](imgs/ebs-16.png)
	
	For **Processes**, please change **Health check Path** to **/login** as it is the URL path for the web app.
	
	![](imgs/ebs-17.png)
	
	Enable **Log files access**
	
	![](imgs/ebs-18.png)
	
	Use **Enhanced** Monitoring.
	
	![](imgs/ebs-19.png)
	
	We can also set the scheduled time for updates and email notifications.
	
	![](imgs/ebs-20.png)  
	
	The following settings are crucial as they determine how the application handles traffic during deployments, in accordance with the specified Deployment Policy. 
	
	Currently, we use a **rolling** update strategy with a 50% update threshold. This ensures zero downtime during updates, as 50% of the application instances remain active to handle incoming traffic while the update is applied to the other 50%.
	
	
	![](imgs/ebs-21.png)
	
	Nginx Proxy server is used.

	
	![](imgs/ebs-22.png)
	
	Finally, review the preview the previous configurations and submit.  
	It will take around 15 minutes for EBS application to be fully created.
	
	Check the events of Elastic Beanstalk after all finished.
	
3. **Take note the end point of Elastic Beanstalk.**

4. Enable ACLs on S3 created by Beanstalk

	Go to S3 and find the bucket created by Elastic 	Beanstalk.

	**Permissions > Object Ownership > ACLs enabled**
![](imgs/s3-acl.png)
	
5. Edit the health check path of EBS Application.
   **
   
   **Beanstalk > Environment > Configuration > Instance Traffic and Scaling> Process > Edit the default>**

	Health Check 

	Path: /login

	Sessions: Sessions Stickiness - Enabled 	(Especially for Vprofile Project)
	
6. Add SSL certificate for HTTPS

   Listeners > Add Listeners > 443, HTTPS, Select Certificate from ACM and save. Then apply.
 ![](imgs/https-ssl.png)
7. Modify the vprofile-backend-sg security group to allow all inbound traffic from the Beanstalk instance.

    Retrieve the Security Group ID of the Beanstalk instance.
    
    Navigate to Security Groups and select vprofile-backend-sg.
    
    Go to the Inbound Rules section and add a new rule:
    
 	Type: All Traffic
 
 	Source: Security Group ID of the Beanstalk instance (to allow traffic from the Beanstalk instance).