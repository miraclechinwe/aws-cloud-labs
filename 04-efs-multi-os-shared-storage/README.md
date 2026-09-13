# Amazon EFS Shared Storage Across Multiple EC2 Instances

## Objective

In this lab, I created an Amazon Elastic File System (EFS) and connected it to three EC2 instances running different Linux operating systems to demonstrate shared file storage.

The EC2 instances used are:

- Amazon Linux
- Ubuntu
- Red Hat Enterprise Linux (RHEL)

The goal of this lab is to demonstrate how Amazon EFS provides shared file storage that can be accessed simultaneously by multiple Linux EC2 instances.


## 1. Create an Amazon EFS File System

I created an Amazon Elastic File System (EFS) to provide shared storage for multiple EC2 instances.

<img width="1596" height="712" alt="image" src="https://github.com/user-attachments/assets/a0735be6-238b-440a-934f-9cb62af38b87" />
<img width="1599" height="713" alt="image" src="https://github.com/user-attachments/assets/a8d421e7-ac0b-4879-86ea-0a1da3a3477e" />


## 2. Configure the EFS Security Group

For this hands-on lab, I modified the security group associated with the EFS mount targets to allow connectivity during the initial configuration.

<img width="1599" height="716" alt="image" src="https://github.com/user-attachments/assets/e6177ead-1a2c-4277-a077-6c0f5ce8ede8" />


## 3. Launch Three EC2 Instances

I launched three EC2 instances using different Linux operating systems:

- Amazon Linux
- Ubuntu
- Red Hat Enterprise Linux (RHEL)

<img width="1596" height="760" alt="image" src="https://github.com/user-attachments/assets/2b07e25f-8a18-464b-ac33-cf2d784deaa0" />

## 4. Configure Three EC2 Instances security groups

During the lab, I configured the security groups for the instances to enable the required network communication with Amazon EFS.

For the first instance, I added an NFS rule to allow communication. For the other two instances, broader traffic rules were temporarily used for connectivity testing during the lab.

<img width="1599" height="581" alt="image" src="https://github.com/user-attachments/assets/351861fe-daac-4d0f-b1ee-9aba0253346e" />

> **Note:** The broad traffic rules were used only for this hands-on demonstration. In a production environment, access should be restricted to only the required ports and trusted sources.

<img width="1598" height="458" alt="image" src="https://github.com/user-attachments/assets/86e67ad0-c8cb-4b6f-901e-09eb7641279e" />


## 5. Verify EC2 Instances and Connect to Red Hat

I verified that all three EC2 instances were running successfully. The instances were running Amazon Linux, Ubuntu, and Red Hat Enterprise Linux (RHEL). I then connected to the Red Hat EC2 instance using the terminal to prepare it for mounting the Amazon EFS file system.

<img width="1352" height="323" alt="image" src="https://github.com/user-attachments/assets/b9ee09c1-e11c-42fb-b720-52b863f8a8c4" />
<img width="1380" height="759" alt="image" src="https://github.com/user-attachments/assets/786b1c67-569f-4799-aee1-f032c2042d1f" />
<img width="1119" height="620" alt="image" src="https://github.com/user-attachments/assets/ddf1a293-2f79-4562-ac66-6645e9c2ed4b" />


## 6. Update Packages on the Three EC2 Instances

After connecting to the three EC2 instances, I updated their package repositories before installing the packages required for EFS.

### Amazon Linux

```bash
sudo yum update -y
```

### Ubuntu

```bash
sudo apt update
```

### Red Hat Enterprise Linux (RHEL)

```bash
sudo yum update -y
```

This ensured that the package information on all three Linux instances was up to date before proceeding with the EFS configuration.

<img width="1107" height="617" alt="image" src="https://github.com/user-attachments/assets/800d5ddf-df08-494d-889c-da2d0c0fbb88" />

## 7. Create a Directory for EFS

I created a directory named `efs` on each of the three EC2 instances. This directory will be used as the mount point for the Amazon EFS file system.

The following command was used:

```bash
mkdir efs
```

I verified that the directory was created using:

```bash
ls
```

<img width="864" height="459" alt="image" src="https://github.com/user-attachments/assets/2cfd2909-fb72-485c-b980-aca0a28691d5" />

## 7. Mount Amazon EFS Using the NFS Client

I opened the Amazon EFS file system and selected **Attach** to view the available mounting options.

I selected **Mount via NFS client** and copied the NFS mount command provided by AWS.

The command was then executed in the CLI of each EC2 instance to mount the EFS file system to the `efs` directory created earlier.

Example:

<img width="1599" height="510" alt="image" src="https://github.com/user-attachments/assets/cb8c5146-5c0d-4710-b744-77eeb19ac244" />

<img width="1476" height="520" alt="image" src="https://github.com/user-attachments/assets/6239dba7-9599-404b-8b20-d73fd66d9edb" />

## 8. Verify Shared Storage

I created a test file in the EFS directory on one EC2 instance and used `ls` on all three instances to verify that the same file was accessible from Amazon Linux, Ubuntu, and Red Hat.

```bash
touch test.txt
ls
```

<img width="1594" height="752" alt="image" src="https://github.com/user-attachments/assets/695d3dc9-0060-4ce9-8e11-10c4c7d5ce02" />

<img width="1599" height="765" alt="image" src="https://github.com/user-attachments/assets/50ad9193-6061-42fe-92ec-05ab977a1c65" />

<img width="1110" height="626" alt="image" src="https://github.com/user-attachments/assets/a77d8c12-3063-41ac-8291-94622d3f7b07" />

## Conclusion

This lab demonstrated how Amazon EFS provides shared file storage that can be accessed by multiple EC2 instances running different Linux operating systems.
