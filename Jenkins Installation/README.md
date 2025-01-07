# Jenkins Installation

![Jenkins Logo](https://github.com/user-attachments/assets/9b4f1359-1b21-4231-aeab-8f2358f32bda)

## Introduction

This guide walks you through the process of installing **Jenkins** on a **Linux** system. It includes all necessary steps, from setting up the repository to accessing Jenkins via a web browser. Make sure to follow each step carefully for a successful installation.

For detailed information, always refer to the official Jenkins website:  
[Official Jenkins Installation Guide](https://www.jenkins.io/doc/book/installing/linux/)

---

## Prerequisites

- A **Linux-based system** (Ubuntu/Debian preferred).
- **Root (sudo) privileges** to install and configure Jenkins.

---

## Installation Steps

### Step 1: Switch to Root User
To ensure you have the necessary permissions to install Jenkins, switch to the root user:

```bash
sudo -i
```

### Step 2: Add Jenkins Repository and Install Jenkins

Run the following commands to add the Jenkins repository, update the package list, and install Jenkins.

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

### Step 3: Install Java (Required for Jenkins)

Jenkins requires **Java** to run. Install the Java Runtime Environment (JRE) by running:

```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
```

### Step 4: Enable Jenkins Service at Boot

To ensure that Jenkins starts automatically when the system boots up, enable the Jenkins service:

```bash
sudo systemctl enable jenkins
```

### Step 5: Start Jenkins Service

Start the Jenkins service with the following command:

```bash
sudo systemctl start jenkins
```

### Step 6: Check Jenkins Service Status

You can check the status of the Jenkins service to ensure it is running:

```bash
sudo systemctl status jenkins
```

### Step 7: Access Jenkins Web Interface

Open a web browser and access Jenkins using the public IP address of your server with **port 8080**.

For example:
```
http://<your-server-ip>:8080
```

![Jenkins Web Interface](https://github.com/user-attachments/assets/f815ea78-b146-4f97-a8d9-4295c43b2802)

### Step 8: Retrieve Initial Admin Password

When you first access Jenkins, you'll be prompted for an **initial admin password**. To get this password, run the following command on the Jenkins server:

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the password and paste it in the web interface to proceed.

### Step 9: Complete Setup

Once you have entered the initial password, Jenkins will guide you through the setup process, including installing recommended plugins and creating an admin user.

---

## Verification

After completing the setup process, you should see the Jenkins dashboard, confirming that **Jenkins is successfully installed**.

![Jenkins Dashboard](https://github.com/user-attachments/assets/43191163-fd36-472c-92a2-7cb363e28f50)

---

## Conclusion

Congratulations! You have successfully installed Jenkins on your server. You can now start using Jenkins to create and manage automation pipelines for your projects.

For more advanced configurations and plugin management, refer to the [Jenkins Documentation](https://www.jenkins.io/doc/).

---

## Additional Resources

- [Jenkins Official Documentation](https://www.jenkins.io/doc/)
- [Jenkins Installation Guide for Linux](https://www.jenkins.io/doc/book/installing/linux/)
