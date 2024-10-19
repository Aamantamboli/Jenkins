# <div align="center"> AWS ECS Fargate with Jenkins</div>

<p align="center">
<img src="https://github.com/user-attachments/assets/c9601f51-5a10-44d7-99b8-9cdb27526d84" widht="200" height="180"/> <img src="https://github.com/user-attachments/assets/bb300598-8601-4202-9f5d-6956a3afd991"/>
</p>

# Step 1: Create ECS Cluster with AWS Fargate (serverless)

![Screenshot 2024-10-17 100249](https://github.com/user-attachments/assets/42d62f49-0931-4a77-bddc-6418e5a171c7)

# Step 2: Create instance and install Jenkins in it [(you can refer here for installation)](https://github.com/Aamantamboli/Jenkins/tree/main/Jenkins%20Installation)

![Screenshot 2024-10-17 100355](https://github.com/user-attachments/assets/a16073b1-b972-4edc-a2b7-40e0529e8814)

# Step 3: Connect Jenkins server with it's public IP and 8080 port
# Step 4: Go to manage jenkins > plugins and install Amazon Elastic Container (ECS) / Fargate 

![Screenshot 2024-10-17 103848](https://github.com/user-attachments/assets/b0ad425a-d430-48cc-b735-3257e0d3668f)

# Step 5: Go to manage jenkins > security and in security got to TCP agent and select fixed port 

![Screenshot 2024-10-17 103746](https://github.com/user-attachments/assets/443fc21c-3961-464f-864b-e290978bda66)

# Step 6: Go to manage jenkins > clouds and create new cloud 

![Screenshot 2024-10-17 103929](https://github.com/user-attachments/assets/fcafb548-3f1b-40f6-a198-d3676532c1c9)

# Step 7: Go to Instance clcik on action > security and modify IAM role

![Screenshot 2024-10-17 101909](https://github.com/user-attachments/assets/53f185b9-7f71-46ac-9aba-d822d1b17581)

# Step 8: Create a IAM role and give permission of admin then select that role

![Screenshot 2024-10-17 101925](https://github.com/user-attachments/assets/f4ccc1d8-a437-47a2-9e86-55c4e80abe59)

# Step 9: Then come to jenkins cloud configure and Select the region where ECS is created 

![Screenshot 2024-10-17 104000](https://github.com/user-attachments/assets/8d8507fc-c8c5-41ce-aa15-7ee3d9f339d3)

# Step 10: Give label and template name 

![Screenshot 2024-10-18 100536](https://github.com/user-attachments/assets/2f791b5b-5fbd-432b-9b43-8e5b26038ed8)

# Step 11: Select launch type Fargate and operating system family LINUX 

![Screenshot 2024-10-18 090359](https://github.com/user-attachments/assets/808ac193-2616-4f41-876b-e7143db7247a)

# Step 12: Give soft limit and CPU units 

![Screenshot 2024-10-17 104326](https://github.com/user-attachments/assets/229f86ce-d71f-4d12-ab6e-3047a89745ce)

# Step 13: Give subnets and security group of your instance and save it

![Screenshot 2024-10-17 104512](https://github.com/user-attachments/assets/29ec8a53-42d9-48b1-bd6c-c8e577799e89)

# Step 14: Create new item 

![Screenshot 2024-10-03 172357](https://github.com/user-attachments/assets/23a667de-9e74-4ca4-af9c-97f6eeea25e1)

# Step 15: Write a pipeline must give your label properly 
```
pipeline {
 agent {
   label 'ecsAgent'
       }
 stages {
   stage('Test') {
    steps{
      echo 'Running Jenkins pipeline with AWS ECS Fargate'
         }
       }
    }
  }
```

# Step 16: CLick on Build now your pipeline will be successfully build 

![Screenshot 2024-10-17 230742](https://github.com/user-attachments/assets/007aa0f1-04cc-48d7-bae8-6a6d80b44e50)

# Step 17: Go to ECS and your task will be running 

![Screenshot 2024-10-17 231543](https://github.com/user-attachments/assets/80f6acf5-98b0-40cd-8b87-c2f9606fb9fe)
