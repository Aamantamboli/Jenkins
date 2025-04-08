# Jenkins Master-Worker Node Setup on AWS

This guide walks through the steps to configure a Jenkins Master node and connect it to a Worker node on AWS EC2 instances. This is useful when you want to offload build tasks from the master node to separate worker nodes.

---

## 🛠️ Prerequisites

- AWS account with permission to create EC2 instances
- Basic understanding of Jenkins and SSH
- Two different key pairs for accessing master and worker (recommended)

---

## ☁️ Step 1: Launch EC2 Instances

### ➤ Jenkins Master Node
- Launch a **Ubuntu Server** instance
- Create or assign a **Security Group** allowing:
  - Port **22** (SSH)
  - Port **80** (HTTP)
  - Port **8080** (Jenkins default)

### ➤ Worker Node
- Launch another **Ubuntu Server** instance
- Use a different **Security Group** allowing:
  - Port **22** (SSH)
  - Port **80** (HTTP)

📌 **Note**: Ensure both instances are in the same **VPC** and **Availability Zone** for better connectivity.

---

## ⚙️ Step 2: Install Jenkins on Master Node

SSH into the master node and run the following commands:

```bash
sudo apt update
sudo apt install openjdk-17-jre -y
java -version
```

### Add Jenkins Repository and Install Jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
```

### Start and Enable Jenkins Service

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

## ☕ Step 3: Install Java on Worker Node

SSH into the worker node and install Java:

```bash
sudo apt update
sudo apt install openjdk-17-jre -y
java -version
```

---

## 🌐 Step 4: Access Jenkins Dashboard

- Visit `http://<Master-Node-Public-IP>:8080` in your browser
- Use the password from `/var/lib/jenkins/secrets/initialAdminPassword` to unlock

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![image](https://github.com/user-attachments/assets/c8c2f169-a8fe-46ce-b01d-0cfa331a891c)

---

## 📦 Step 5: Install Suggested Plugins

- Once logged in, select **Install Suggested Plugins**
- Wait for plugin installation to complete

---

## 🚀 Step 6: Start Using Jenkins

- Create the first admin user
- Configure instance URL if prompted

---

## 🤖 Step 7: Add a Worker Node to Jenkins

1. Go to **Manage Jenkins** > **Nodes** > **New Node**
2. Enter a **Node Name**, select **Permanent Agent**, then click OK
3. Configure the following:

    - **Remote root directory** (e.g., `/home/ubuntu/jenkins`)
    - **Labels** (for job targeting)
    - **Launch method**: *Launch agent via SSH*

![image](https://github.com/user-attachments/assets/fd5e137d-448e-4e94-8ca5-14225bcc6924)

---

## 🔐 Step 8: Configure SSH for Worker Node

1. Under **Host**, enter the **public IP** of the worker node
2. Under **Credentials**, click **Add**:
   - Select **Kind**: *SSH Username with private key*
   - Username: `ubuntu` (or your EC2 default user)
   - Private Key: Paste the content of your `.pem` file
3. Under **Host Key Verification Strategy**, select:
   - *Non-verifying Verification Strategy*

![image](https://github.com/user-attachments/assets/0f3d72b7-8518-4e76-b7c1-b90a177a5857)

---

## ✅ Step 9: Save and Connect

- Click **Save**
- Jenkins will try to establish an SSH connection and start the agent

![image](https://github.com/user-attachments/assets/53e490e6-8ca8-4db1-a42e-3e7b00026d2b)

---

## 📌 Notes

- Ensure that the worker instance's security group allows inbound SSH (port 22)
- Verify that both instances can ping each other using private IPs (optional)
- You can repeat the steps to add more workers as needed
