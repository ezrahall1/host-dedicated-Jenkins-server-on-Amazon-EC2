<h1>Host a dedicated Jenkins server on Amazon EC2</h1>

<h2>Description</h2>
This project will demonstrate how to host a dedicated Jenkins Server on Amazon EC2.
Jenkins is an open-source automation server that integrates with a number of AWS services, such as AWS CodeCommit, AWS CodeDeploy, Amazon EC2 Spot, and Amazon EC2 Fleet. 
<br />


<h2>Services Used</h2>

- <b>EC2</b>
- <b>VPC</b> 

<h2>Environments Used </h2>

- <b>AWS</b>
- <b>Putty</b>

<h2>Program walk-through:</h2>
<H3>Step 1 - Create security group</H3>
Once you have log into the AWS account you would need to navigate to EC2, click on security groups.
You will create a security group and add the following rules: * Allow inbound HTTP access from anywhere. * Allow inbound SSH traffic from your computer’s public IP address so that you can connect to your EC2 instance.

From there you would need to launch an EC2 instance Enter the name of the EC2 select Amazon Linux, make sure the Amazon Machine Image (AMI) says free tier eligible. For the instance type make sure you select free tier eligible or you would be charged. Create a new key pair if you do not already have one. In the network settings section leave "allow SSH traffic from" ticked. Leave the rest as default and click launch instance.


<img src="https://i.imgur.com/fdVAGzB.png" height="80%" width="80%" alt="Image 1"/>


<H3>Step 2 – Connecting to EC2 instance </H3>
Once the EC2 instance is in a running state you would need to connect to it. Right click and select connect.

<img src="https://i.imgur.com/kaoMGqH.png" height="80%" width="80%" alt="Image 2"/>

<img src="https://i.imgur.com/WQEebAw.png" height="80%" width="80%" alt="Image 3"/>



There are many applications you can use to connect to your EC2 instance. For this project I will be using [Putty](https://www.putty.org).
Once you have successfully connected to your EC2 instance using Putty you should see something like this:
<img src="https://i.imgur.com/wsd36ox.png" height="80%" width="80%" alt="Image 4"/>

<H3>Step 3 – Install Jenkins</H3>
To ensure that your software packages are up to date on your instance, use the following command to perform a quick software update:

- [ec2-user ~]$ sudo yum update –y

Add the Jenkins repo using the following command:

- [ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \https://pkg.jenkins.io/redhat-stable/jenkins.repo

Import a key file from Jenkins-CI to enable installation from the package:

- [ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
- [ec2-user ~]$ sudo yum upgrade

Install Java:

- [ec2-user ~]$ sudo amazon-linux-extras install java-openjdk11 -y

Install Jenkins:

- [ec2-user ~]$ sudo yum install jenkins -y

Enable the Jenkins service to start at boot:

- [ec2-user ~]$ sudo systemctl enable jenkins

Start Jenkins as a service:

- [ec2-user ~]$ sudo systemctl start jenkins

You can check the status of the Jenkins service using the command:

- [ec2-user ~]$ sudo systemctl status jenkins

<H3>Step 4 – Configure Jenkins</H3>

Jenkins is now installed and running on your EC2 instance. To configure Jenkins:

- Connect to http://<your_server_public_DNS>:8080 from your browser. You will be able to access Jenkins through its management interface:

<img src="https://i.imgur.com/9Jzkg1Q.png" height="80%" width="80%" alt="Image 4"/>

Use the following command to display this password:

- [ec2-user ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword

The Jenkins installation script directs you to the Customize Jenkins page. Click Install suggested plugins.
Once the installation is complete, Create First Admin User, click Save and Continue.



<img src="https://i.imgur.com/7Oo0i0y.png" height="80%" width="80%" alt="Image 5"/>


<img src="https://i.imgur.com/y7c7Dau.png" height="80%" width="80%" alt="Image 6"/>

<img src="https://i.imgur.com/tGHagsx.png" height="80%" width="80%" alt="Image 7"/>

On the left-hand side, click Manage Jenkins, and then click Manage Plugins. Click on the Available tab, and then enter Amazon EC2 plugin at the top right.
Select the checkbox next to Amazon EC2 plugin, and then click Install without restart.

<img src="https://i.imgur.com/cYMCPYv.png" height="80%" width="80%" alt="Image 8"/>

Once the installation is done, click Back to Dashboard.
Click on Configure a cloud.



Click Add a new cloud, and select Amazon EC2. A collection of new fields appears.
Fill out all the fields. (Note: You will have to Add Credentials of the kind AWS Credentials.)

<img src="https://i.imgur.com/7syZfaI.png" height="80%" width="80%" alt="Image 9"/>


</p>


