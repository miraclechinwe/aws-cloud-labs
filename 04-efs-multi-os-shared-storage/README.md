# Amazon EFS Shared Storage Across Multiple EC2 Instances

## Overview

This hands-on AWS lab demonstrates how to create an Amazon Elastic File System (EFS) and connect it to three Amazon EC2 instances running different Linux operating systems.

The EC2 instances used are:

- Amazon Linux
- Ubuntu
- Red Hat Enterprise Linux (RHEL)

The goal of this lab is to demonstrate how Amazon EFS provides shared file storage that can be accessed simultaneously by multiple Linux EC2 instances.

## Architecture

Amazon EFS acts as the shared file system for all three EC2 instances.

```text
                    Amazon EFS
                 Shared File System
                       |
              -------------------
              |        |        |
              |        |        |
         Amazon Linux Ubuntu  Red Hat
              EC2      EC2      EC2
