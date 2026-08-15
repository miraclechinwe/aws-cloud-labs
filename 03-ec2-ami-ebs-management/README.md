# Lab 03: EC2 AMI and EBS Management

## Objective
In this lab, I worked with EC2, AMIs, and EBS to learn how to replicate an EC2 instance across AWS regions and manage its storage.

## 1. Launch a Linux EC2 Instance
I launched a Linux EC2 instance in the N. Virginia (`us-east-1`) region and connected it to install some web servers.

<img width="1599" height="761" alt="image" src="https://github.com/user-attachments/assets/ec7d6a22-0d36-45bf-b45e-c9d93475f611" />
<img width="1381" height="770" alt="image" src="https://github.com/user-attachments/assets/fba76f86-f0a3-4f73-a646-f54da631d06c" />


## 2. Create an AMI
I created an AMI from the instance to save its current configuration and use it to create another instance.

<img width="1596" height="806" alt="image" src="https://github.com/user-attachments/assets/42841752-5128-41f8-886a-7c578be09584" />


## 3. Copy the AMI to Oregon
I copied the AMI from N. Virginia to Oregon (`us-west-2`) and launched another EC2 instance from the copied AMI.

<img width="1596" height="762" alt="image" src="https://github.com/user-attachments/assets/62090a71-0567-46ee-b525-d8ab64b52501" />
<img width="1599" height="769" alt="image" src="https://github.com/user-attachments/assets/51866b78-5040-4868-b287-6725ddffeff3" />
<img width="1599" height="766" alt="image" src="https://github.com/user-attachments/assets/60e985d1-a2ed-4b70-9221-76c13323e8f2" />


## 4. Create and Attach EBS Volumes
I created two EBS volumes and attached them to the N. Virginia region

<img width="1599" height="768" alt="image" src="https://github.com/user-attachments/assets/68c24dc8-41b2-428d-a40c-ae64ed45e020" />


## 5. Detach and Delete a Volume and Increase the size of the other volume
I detached one of the EBS volumes and deleted it and I increased the size of the remaining EBS volume.
.

<img width="1599" height="816" alt="image" src="https://github.com/user-attachments/assets/ea69af58-e037-44df-889c-17bd6013d418" />


## 6. Back Up the Volume
I created an EBS snapshot to back up the remaining volume.

<img width="1599" height="811" alt="image" src="https://github.com/user-attachments/assets/4c927ea8-0668-4e95-ac0e-af6e5fd230be" />


## What I Learned
This lab helped me understand how AMIs can be used to reproduce EC2 environments and how EBS volumes can be attached, resized, removed, and backed up using snapshots.
