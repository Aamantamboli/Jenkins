# Jenkins-Installation 

![new](https://github.com/user-attachments/assets/9b4f1359-1b21-4231-aeab-8f2358f32bda)

[Always refer on official website of jenkins](https://www.jenkins.io/doc/book/installing/linux/)
## Step 1: Go to root user
```
sudo -i
```
## Step 2: Long Term Support release 
```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
## Step 3: Installation of Java
```
sudo apt update
sudo apt install fontconfig openjdk-17-jre
```
## Step 4: You can enable the Jenkins service to start at boot with the command
```
sudo systemctl enable jenkins
```
## Step 5: You can start the Jenkins service with the command
```
sudo systemctl start jenkins
```
## Step 6: You can check the status of the Jenkins service using the command
```
sudo systemctl status jenkins
```
## Step 7: Copy public IP of Jenkins Server and hit it on browser with port 8080

![image](https://github.com/user-attachments/assets/f815ea78-b146-4f97-a8d9-4295c43b2802)

## Step 8: Now connect your server and copy password by command and paste it  
```
cat /var/lib/jenkins/secrets/initialAdminPassword
```
**Successfully Installed Jenkins**

![image](https://github.com/user-attachments/assets/43191163-fd36-472c-92a2-7cb363e28f50)
