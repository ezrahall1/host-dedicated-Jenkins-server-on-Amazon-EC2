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

- Connect to http://<your_server_public_DNS>:8080 from your favorite browser. You will be able to access Jenkins through its management interface:

<img src="https://i.imgur.com/9Jzkg1Q.png" height="80%" width="80%" alt="Image 4"/>

Use the following command to display this password:

- [ec2-user ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword

<img src="https://i.imgur.com/7Oo0i0y.png" height="80%" width="80%" alt="Image 5"/>


<img src="https://i.imgur.com/y7c7Dau.png" height="80%" width="80%" alt="Image 6"/>

<img src="https://i.imgur.com/tGHagsx.png" height="80%" width="80%" alt="Image 6"/>





<H3>Step 3 – Creating bash script and variables</H3>
The next step is you need to create the bash script name for example testscript.sh and create the variables in a text editor using this command nano testscript.sh .

<img src="https://i.imgur.com/nb0aNT5.png" height="80%" width="80%" alt="Image 5"/>

Once you have enter your script you would need to save it and make the bash script is executable by running command chmod +x testscript.sh.
Now you are able to run the bash script using the command ./testscript.sh

<img src="https://i.imgur.com/WtDE4tp.png" height="80%" width="80%" alt="Image 6"/>

<H3>Step 4 – Configure Jenkins</H3>


</p>


