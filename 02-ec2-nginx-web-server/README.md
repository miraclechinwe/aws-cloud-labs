# Lab 02: Deploy a Nginx Web Server on AWS EC2

## Objective
Launch an Ubuntu EC2 instance and configure Nginx to host a custom web page.

## 1. Launch EC2 Instance
- Region: US East (N. Virginia) `us-east-1`
- Operating System: Ubuntu
- Configured the required security group rules.

<img width="1532" height="770" alt="image" src="https://github.com/user-attachments/assets/5d56b871-1f4b-47d4-95b8-0d1612b02068" />


## 2. Connect to the Instance
Connected to the Ubuntu EC2 instance.

<img width="690" height="774" alt="image" src="https://github.com/user-attachments/assets/e482f674-6349-4b77-a426-1e2fa62280e2" />


## 3. Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

<img width="1357" height="661" alt="image" src="https://github.com/user-attachments/assets/b2a7556c-7c6b-4613-9018-8e6c7d7b48cb" />


## 4. Create Custom Web Page
Replaced the default Nginx page with a custom **Hello World** page.

<img width="1055" height="664" alt="image" src="https://github.com/user-attachments/assets/f85e66c1-7a6c-4dd6-b075-7dac3662bf80" />


## 5. Test the Web Server
Accessed the EC2 public IP from a browser and confirmed that the web page was running successfully.

<img width="538" height="260" alt="image" src="https://github.com/user-attachments/assets/4299b1fb-1ffa-47ae-a94a-ac35d5289e31" />


## Key Takeaway
I learned how to deploy an Ubuntu EC2 instance, install Nginx, and host a basic web page on AWS.
