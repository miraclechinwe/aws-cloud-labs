# Lab 01: Launch and Connect to a Linux EC2 Instance

## Objective
Launch an Amazon Linux EC2 instance and connect to it using EC2 Instance Connect and SSH.

## 1. Launch EC2 Instance
I launched an Amazon Linux 2023 EC2 instance and configured the required network and security settings.

<img width="1598" height="764" alt="image" src="https://github.com/user-attachments/assets/4bbce36d-2958-4dd9-9c25-8f0ad0ce8955" />


## 2. Connect Using EC2 Instance Connect
I connected to the Linux instance directly from the AWS Management Console using EC2 Instance Connect.

<img width="1599" height="568" alt="image" src="https://github.com/user-attachments/assets/bb491b7c-e30e-4f49-b5d6-ca49f0e218b5" />


## 3. Connect Using SSH
I also connected remotely from Windows Command Prompt using my `.pem` key pair.

```bash
ssh -i <key-pair>.pem ec2-user@<public-ip>
```

<img width="830" height="577" alt="image" src="https://github.com/user-attachments/assets/8d2cd497-5ef2-4cf6-9402-a25c265b255f" />


## 4. Run Linux Commands
After connecting, I practiced basic Linux commands.

```bash
touch miracle.com
ls
```

## Key Takeaway
I learned two ways to access an Amazon Linux EC2 instance: EC2 Instance Connect through the AWS Console and SSH from my local computer.
