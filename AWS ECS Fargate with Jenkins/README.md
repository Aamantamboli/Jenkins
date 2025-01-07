# AWS ECS Fargate with Jenkins

This guide walks you through setting up **AWS ECS Fargate** to run Jenkins pipelines in a serverless environment. We will create an ECS cluster, set up Jenkins on an EC2 instance, configure it to work with AWS ECS Fargate, and run a pipeline.

---

## Prerequisites

1. **AWS Account**: You need an AWS account to create and configure ECS Fargate and EC2 instances.
2. **Jenkins Installation**: Jenkins should be installed and running. If you haven't installed Jenkins, you can refer to this [Jenkins Installation Guide](https://github.com/Aamantamboli/Jenkins/tree/main/Jenkins%20Installation).

---

## Steps to Setup AWS ECS Fargate with Jenkins

### Step 1: Create ECS Cluster with AWS Fargate (serverless)

- Log in to the AWS Management Console.
- Navigate to **ECS** and create a new ECS cluster.
- Choose **Fargate** as the launch type for serverless computing.

![Create ECS Cluster](https://github.com/user-attachments/assets/42d62f49-0931-4a77-bddc-6418e5a171c7)

### Step 2: Install Jenkins on an EC2 Instance

- Create an EC2 instance and install Jenkins. You can follow the detailed instructions for Jenkins installation in this [guide](https://github.com/Aamantamboli/Jenkins/tree/main/Jenkins%20Installation).

![EC2 Instance for Jenkins](https://github.com/user-attachments/assets/a16073b1-b972-4edc-a2b7-40e0529e8814)

### Step 3: Connect to Jenkins Server

- Access Jenkins via its public IP on port **8080**.

### Step 4: Install Amazon ECS/Fargate Plugin in Jenkins

- In Jenkins, go to **Manage Jenkins** > **Manage Plugins**.
- Search for and install the **Amazon Elastic Container (ECS) / Fargate** plugin.

![Install ECS Plugin](https://github.com/user-attachments/assets/b0ad425a-d430-48cc-b735-3257e0d3668f)

### Step 5: Configure Jenkins Security

- Go to **Manage Jenkins** > **Configure Global Security**.
- Under **TCP Agent**, select the option for a **fixed port**.

![Configure Jenkins Security](https://github.com/user-attachments/assets/443fc21c-3961-464f-864b-e290978bda66)

### Step 6: Create a New Cloud Configuration in Jenkins

- Go to **Manage Jenkins** > **Configure System** > **Clouds**.
- Create a new cloud configuration for **Amazon ECS Fargate**.

![Create New Cloud in Jenkins](https://github.com/user-attachments/assets/fcafb548-3f1b-40f6-a198-d3676532c1c9)

### Step 7: Modify IAM Role for EC2 Instance

- Go to the **EC2 instance**, select it, and click **Actions** > **Security** > **Modify IAM role**.
- Attach an IAM role with appropriate permissions for ECS.

![Modify IAM Role](https://github.com/user-attachments/assets/53f185b9-7f71-46ac-9aba-d822d1b17581)

### Step 8: Create IAM Role for ECS Permissions

- Create an IAM role with **AdministratorAccess** permission.
- Attach this IAM role to the EC2 instance.

![Create IAM Role](https://github.com/user-attachments/assets/f4ccc1d8-a437-47a2-9e86-55c4e80abe59)

### Step 9: Configure Jenkins ECS Cloud Settings

- In Jenkins, under the **Cloud** configuration, select the AWS region where ECS is created.

![Configure ECS Cloud](https://github.com/user-attachments/assets/8d8507fc-c8c5-41ce-aa15-7ee3d9f339d3)

### Step 10: Set Label and Template Name for ECS Agent

- Give the label and template name for your ECS Fargate instance in Jenkins.

![Set Label and Template](https://github.com/user-attachments/assets/2f791b5b-5fbd-432b-9b43-8e5b26038ed8)

### Step 11: Configure Fargate Launch Type and Operating System

- Select **Launch type** as **Fargate**.
- Choose **Operating system family** as **Linux**.

![Configure Fargate Launch Type](https://github.com/user-attachments/assets/808ac193-2616-4f41-876b-e7143db7247a)

### Step 12: Set Soft Limit and CPU Units

- Set the soft limit and CPU units for the ECS task.

![Set Soft Limit and CPU](https://github.com/user-attachments/assets/229f86ce-d71f-4d12-ab6e-3047a89745ce)

### Step 13: Configure Subnets and Security Groups

- Select the subnets and security groups associated with your EC2 instance.
- Save the configuration.

![Configure Subnets and Security Groups](https://github.com/user-attachments/assets/29ec8a53-42d9-48b1-bd6c-c8e577799e89)

### Step 14: Create a New Jenkins Item (Pipeline)

- In Jenkins, create a new **Pipeline** job.

![Create Pipeline Job](https://github.com/user-attachments/assets/23a667de-9e74-4ca4-af9c-97f6eeea25e1)

### Step 15: Define Jenkins Pipeline Script

- Define the Jenkins pipeline using the following script. Ensure the label matches the ECS agent label you configured earlier.

```groovy
pipeline {
    agent {
        label 'ecsAgent'
    }
    stages {
        stage('Test') {
            steps {
                echo 'Running Jenkins pipeline with AWS ECS Fargate'
            }
        }
    }
}
```

### Step 16: Build the Pipeline

- Click **Build Now** to trigger the pipeline.
- The pipeline will start running on ECS Fargate.

![Build Pipeline](https://github.com/user-attachments/assets/007aa0f1-04cc-48d7-bae8-6a6d80b44e50)

### Step 17: Verify Running ECS Task

- Go to the **ECS** console.
- Your task should now be running in the ECS cluster.

![ECS Task Running](https://github.com/user-attachments/assets/80f6acf5-98b0-40cd-8b87-c2f9606fb9fe)

---

## Conclusion

You have successfully set up **AWS ECS Fargate** with **Jenkins** to run Jenkins pipelines in a serverless environment. Now, Jenkins can manage containerized workloads with ECS Fargate, allowing you to run builds, tests, and deploy applications efficiently.

For more information on ECS and Jenkins integration, you can refer to:
- [AWS ECS Documentation](https://docs.aws.amazon.com/ecs/latest/userguide/what-is-fargate.html)
- [Jenkins ECS/Fargate Plugin](https://plugins.jenkins.io/ecs-fargate/)
