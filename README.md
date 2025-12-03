# Static Website CI/CD Deployment using Terraform and Jenkins

## ⭐ Overview

This project delivers a complete end-to-end CI/CD pipeline for deploying a Static Website on AWS, fully automated using Terraform, Jenkins, and GitHub. The goal is to eliminate manual configuration and create a fast, reliable, and scalable deployment process suitable for real-world DevOps workflows.

Using Terraform, the entire cloud infrastructure is provisioned automatically—including EC2 instance, security groups and necessary server setup. Once deployed, Jenkins takes over as the CI/CD engine, continuously monitoring the GitHub repository for changes.

* Every time a developer pushes code:

* Jenkins automatically pulls the latest version

* The updated website files are securely transferred to the EC2 server

* The web server is refreshed to reflect the new content

* Deployment is completed in seconds—without downtime

This project showcases how Infrastructure-as-Code and Continuous Delivery can work together to create a seamless, repeatable, and production-grade workflow for static web hosting. It is ideal for learning DevOps automation, cloud provisioning, CI/CD pipelines, and real-time deployment strategies.

---

## 1. Clone the Repository and Modify Files

Clone the static website project to your local system and make required modifications.

```bash
git clone https://github.com/dalvipiyush07/static-website-project.git
cd static-website-project
```

Update HTML, CSS, or configuration files as needed.

---

## 2. Launch EC2 Instance using Terraform

A Terraform configuration is used to create:
- EC2 instance  
- Security Group  
- Key Pair  
- User Data for Nginx setup

Run Terraform:

```bash
terraform init
terraform plan
terraform apply
```

After apply, Terraform will output the EC2 Public IP.

**Screenshot:**  
![Terraform Apply](./imgs/Screenshot%20(125).png)

---

## 3. Jenkins Setup (Plugins and Credentials)

Login to Jenkins and follow the setup steps:

### Required Plugins
- Git Plugin  
- Pipeline Plugin  
- SSH Agent Plugin  
- GitHub Integration Plugin  

### Add Credentials
Navigate to:
```
Jenkins Dashboard → Manage Jenkins → Credentials → Global
```
Add:
- SSH Private Key (for EC2 deployment)
- GitHub token (optional)

---

## 4. Add Jenkinsfile and Push to GitHub

Create a `Jenkinsfile` in the root of your repository.  
Commit and push:

```bash
git add .
git commit -m "Add Jenkinsfile for CI/CD"
git push origin main
```

---

## 5. Configure GitHub Webhook

Go to your GitHub repository:

```
Settings → Webhooks → Add Webhook
```

Enter:
- Payload URL: `http://<your-jenkins-ip>:8080/github-webhook/`
- Content type: `application/json`
- Trigger: "Just the push event"

**Screenshot:**  
![](./img/github.png)

---

## 6. Jenkins Build Output

Whenever the repository receives a new commit:
- Webhook triggers Jenkins  
- Pipeline pulls the updated code  
- Deployment is performed automatically  

**Screenshot:**  
![Jenkins Output](./imgs/Screenshot%20(127).png)

---

## 7. Application Running Successfully

After successful deployment, open browser:

```
http://<EC2_PUBLIC_IP>
```

Your static website will load successfully.

---

## Conclusion
This project shows how Terraform and Jenkins can fully automate the deployment of a static website on AWS. With Infrastructure-as-Code and a continuous delivery pipeline, every code change is deployed instantly and reliably, making the process fast, repeatable, and efficient. It provides a simple yet powerful example of real-world DevOps automation.

---
