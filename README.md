# ☁️ AWS Cloud Labs

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

Hands-on labs documenting my practical experience building, configuring, securing and managing infrastructure on **Amazon Web Services (AWS)**. Each lab includes the objective, steps, problems I ran into and how I solved them.

## 🎯 Goals
- Build practical AWS skills through real deployments
- Understand AWS compute, storage and networking
- Apply cloud security best practices (least privilege, Security Groups, key management)
- Document problems and solutions like in a real engineering job

## 🧪 Labs

| # | Lab | AWS Services | Key Skills | Status |
|---|-----|--------------|------------|--------|
| 01 | [Launch & Connect to a Linux EC2 Instance](./01-ec2-linux-ssh-instanceconnect) | EC2, Security Groups | SSH, key pairs, EC2 Instance Connect | ✅ Completed |
| 02 | [Deploy an Nginx Web Server](./02-ec2-nginx-web-server) | EC2 | Linux, Nginx, inbound rules | ✅ Completed |
| 03 | [AMI & EBS Volume Management](./03-ec2-ami-ebs-management) | EC2, EBS, AMI | Snapshots, volumes, backup & restore | ✅ Completed |
| 04 | [Shared Storage with EFS Across Operating Systems](./04-efs-multi-os-shared-storage) | EFS, EC2 | NFS mounting, shared storage | ✅ Completed |
| 05 | [IAM Demo 1: Create an IAM User & Test Console Access](./05-iam-user-console-access) | IAM, EC2 | IAM users, console sign-in, managed policies, least privilege | ✅ Completed |
| 06 | [IAM Demo 2: Check IAM User Access with the AWS CLI](./06-iam-user-aws-cli-access) | IAM, EC2, AWS CLI | Access keys, `aws configure`, CLI commands, AccessDenied testing | ✅ Completed |

## 🛠️ Technologies
- **AWS:** EC2, EBS, EFS, AMI, VPC, Security Groups, IAM
- **Operating systems:** Amazon Linux, Linux administration
- **Web server:** Nginx
- **Tools:** AWS CLI, SSH, Git, GitHub

## 🔒 Security
No private keys, passwords, AWS access keys or other secrets are stored in this repository. All resources were deleted after each lab to avoid unnecessary costs.

## 📫 Contact
- LinkedIn: [your LinkedIn link]
- Certifications: [e.g. AWS Certified Cloud Practitioner]
