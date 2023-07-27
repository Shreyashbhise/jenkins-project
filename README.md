

    Go to AWS Console
    Instances(running)
    Launch instances

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/3842e8de-4ab1-4ad9-a805-20f8fb8354b1)


Install Jenkins.

Pre-Requisites:

    Java (JDK)

Run the below commands to install Java and Jenkins

Install Java

sudo apt update
sudo apt install openjdk-11-jre

Verify Java is Installed

java -version

Now, you can proceed with installing Jenkins

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins


*Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

    EC2 > Instances > Click on
    In the bottom tabs -> Click on Security
    Security groups
    Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).


Login to Jenkins using the below URL:

http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/9a76e415-bd3f-4e79-8bc0-905ed9207c3a)

Click on Install suggested plugins

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/5f2b6cf8-b5e6-4f30-92b5-02cd4814f101)

Wait for the Jenkins to Install suggested plugins

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/f543c924-e2a1-4776-943e-a974e3a226fe)

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/0d99c39d-7c52-4b31-bf6f-c085b94e74a5)

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/5e14f730-93fe-4799-8197-aea71668f485)

Install the Docker Pipeline plugin in Jenkins:

    Log in to Jenkins.
    Go to Manage Jenkins > Manage Plugins.
    In the Available tab, search for "Docker Pipeline".
    Select the plugin and click the Install button.
    Restart Jenkins after the plugin is installed.


![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/4152ac4a-132a-4d36-b9b1-b141afdc4f0c)
Docker Slave Configuration

Run the below command to Install Docker

sudo apt update
sudo apt install docker.io

Grant Jenkins user and Ubuntu user permission to docker deamon.

sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker

Once you are done with the above steps, it is better to restart Jenkins.

http://<ec2-instance-public-ip>:8080/restart

The docker agent configuration is now successful.

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/b3d7f0f5-e1a5-4ac8-8918-e29a4789936a)

![image](https://github.com/Shreyashbhise/jenkins-project/assets/108046802/5ac95822-9e13-4d64-ba1e-ab9b60bce57b)
