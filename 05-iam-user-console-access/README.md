# Lab 05: IAM Demo 1 – Create an IAM User and Test Console Access

![AWS IAM](https://img.shields.io/badge/AWS_IAM-DD344C?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Amazon EC2](https://img.shields.io/badge/Amazon_EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)
![Security](https://img.shields.io/badge/Security-Least_Privilege-2E7D32?style=for-the-badge)

> **IAM series:** ** Demo 1 Console access** (this lab) · [Demo 2 – AWS CLI access](../06-iam-user-aws-cli-access)

##  Contents

1. [Objective](#-objective)
2. [Architecture](#%EF%B8%8F-architecture)
3. [Key Concepts](#-key-concepts)
4. [Lab Workflow](#-lab-workflow)
5. [Steps](#-steps)
6. [How AWS Decides: Allow or Deny](#%EF%B8%8F-how-aws-decides-allow-or-deny)
7. [Common Problems and Fixes](#%EF%B8%8F-common-problems-and-fixes)
8. [Security Best Practices](#-security-best-practices)
9. [Conclusion](#-conclusion)


##  Objective

In this lab, I created my first IAM (Identity and Access Management) user, signed in to the AWS Management Console as that user, and tested what the user could do **before and after** attaching a permission policy.

The goal is to show that a new IAM user has **no permissions by default**, and that access is granted only through policies, following the **principle of least privilege**.


##  Architecture

```mermaid
flowchart LR
    Root["👑 Root user<br/>(admin)"] -->|creates user &<br/>attaches policy| IAM["🔐 AWS IAM"]
    IAM --> User["🧑‍💻 IAM user<br/>intellipaat-user"]
    Policy["📄 AmazonEC2FullAccess<br/>(AWS managed policy)"] -->|attached to| User
    User -->|signs in from<br/>incognito window| Console["🖥️ AWS Management Console"]
    Console -->|allowed| EC2["🖥️ Amazon EC2<br/>launch instances"]
    Console -.->|not in policy| Denied["⛔ Access denied<br/>(e.g. IAM, S3)"]
```


##  Key Concepts

| Concept | What it means |
|---------|---------------|
| **Root user** | The email login that created the AWS account. It has full access and should not be used for daily work. |
| **IAM user** | An identity for one person or application, that needs to access AWS services or resources. |
| **Console access** | Lets the user sign in to the AWS Management Console with a user name and password. |
| **IAM policy** | A set of permissions. It is a JSON document that defines which actions are allowed or denied on which AWS resources. Think of it as a permission sheet attached to a user, group or role. |
| **Least privilege** | Permissions are limited to what a person needs for their job responsibilities. |

### Types of IAM policies

```mermaid
flowchart LR
    P["📄 IAM Policy"] --> M["Managed policy<br/>(reusable, standalone)"]
    P --> I["Inline policy<br/>(embedded in one user,<br/>group or role)"]
    M --> AM["AWS managed<br/>managed by AWS<br/>e.g. AmazonEC2FullAccess"]
    M --> CM["Customer managed<br/>created and managed by me"]
```

In the IAM console under **Policies**, the **Type** column shows whether a policy is AWS managed or customer managed.

### Ways to give a user permissions

| Option | How it works | Best for |
|--------|--------------|----------|
| **Add user to group** | The user gets all permissions attached to the group | Teams; the recommended way |
| **Copy permissions** | Copies groups and policies from an existing user | Someone with the same job as a colleague |
| **Attach policies directly** | The policy is attached to this one user only | Quick tests (used in this lab) |


##  Lab Workflow

```mermaid
flowchart TD
    A([Start as root user]) --> B["IAM → Users → Create user"]
    B --> C["Name: intellipaat-user<br/>custom password"]
    C --> D["Create user with<br/>no permissions yet"]
    D --> E["Sign in as IAM user<br/>in incognito window"]
    E --> F{"Try to launch<br/>an EC2 instance"}
    F -->|No policy yet| G["⛔ Not authorized"]
    G --> H["As root: attach<br/>AmazonEC2FullAccess"]
    H --> I{"Try to launch<br/>an EC2 instance again"}
    I --> J["✅ Instance launches"]
    J --> K["As root: check the<br/>user's permissions"]
    K --> L([End])
```


##  Steps

### 1. Create the IAM User

Signed in as the root user, I went to **IAM → Users → Create user**.

- **User name:** 
- Ticked **Provide user access to the AWS Management Console**
- Selected **Custom password** and entered a password
- **Unticked** *Users must create a new password at next sign-in*, so I could sign in straight away with the same password for this demo

<img width="1599" height="716" alt="image" src="https://github.com/user-attachments/assets/dfbabd43-aae4-4d29-94bb-e6529a1d0f3a" />


### 2. Set Permissions and Create the User

On the **Set permissions** page, I kept **Add user to group** selected but did not choose a group, so the user was created **without any permissions**. I clicked **Next**, then **Create user**.

<img width="1598" height="665" alt="image" src="https://github.com/user-attachments/assets/71cb6c41-1729-4ac6-b4cc-c4164490a00d" />


### 3. Sign In as the IAM User

I opened an **incognito (private) browser window**, pasted the **IAM user sign-in URL**, and signed in with the user name and password.

Using incognito let me stay signed in as the root user in my normal window and as the IAM user in the private window at the same time.

```mermaid
sequenceDiagram
    actor R as Root user (normal window)
    actor U as IAM user (incognito window)
    participant S as AWS Sign-in
    participant C as AWS Console

    R->>R: Copy IAM user sign-in URL,<br/>user name and password
    U->>S: Open sign-in URL
    U->>S: Enter user name + password
    S->>C: Sign-in successful
    C-->>U: Console opens (no permissions yet)
```

<img width="1599" height="767" alt="image" src="https://github.com/user-attachments/assets/270901c4-285e-4fda-a9e9-77e83f239228" />

<img width="1599" height="707" alt="image" src="https://github.com/user-attachments/assets/59dfdc1a-f94d-48fb-8cb7-f8298011a62f" />



### 4. Test Before Attaching a Policy

As the IAM user, I tried to use EC2. Because no policy was attached, the console showed **not authorized / access denied** messages. A user can login but cannot do anything without a permission, which is called IAM policy: its a permission sheet attached to a user, group or role. 

<img width="1516" height="723" alt="image" src="https://github.com/user-attachments/assets/f79e3294-6a65-456a-a7b2-b9d67e4afdcd" />


### 5. Attach the AmazonEC2FullAccess Policy

Back in the root user window, I went to **IAM → Users → xxxxx → Permissions → Add permissions → Attach policies directly**, searched for **AmazonEC2FullAccess**, ticked the checkbox, clicked **Next**, then **Add permissions**.

<img width="1588" height="711" alt="image" src="https://github.com/user-attachments/assets/9f759130-6b9c-481c-9659-ea7496ce3b4d" />

<img width="1595" height="716" alt="image" src="https://github.com/user-attachments/assets/29f31280-e7db-4e8d-b624-01e9cbcd541c" />



### 6. Test After Attaching the Policy

In the IAM user's incognito window, I clicked **Launch instance** to check whether the user could now launch an EC2 instance, and apart from EC2 Access, this user cannot access any other thing. 

| Test as `intellipaat-user` | Before policy | After AmazonEC2FullAccess |
|----------------------------|:-------------:|:-------------------------:|
| Launch an EC2 instance | ⛔ Denied | ✅ Allowed |
| View EC2 instances | ⛔ Denied | ✅ Allowed |
| Create IAM users | ⛔ Denied | ⛔ Denied (not in policy) |

<img width="1599" height="714" alt="image" src="https://github.com/user-attachments/assets/68e13c76-2dbc-4140-8ebd-ddce9a09e0e5" />


### 7. Check the User's Permissions as Root

Finally, in the root user window, I opened the user's **Permissions** tab and clicked on the attached policy to see exactly which permissions the user has. Clicking **{} JSON** shows the policy document.

<img width="1597" height="724" alt="image" src="https://github.com/user-attachments/assets/ac3a3edf-f9a9-452f-900a-6858b62d8fbd" />

##  How AWS Decides: Allow or Deny

Every time the user does something, AWS checks their policies. By default, **everything is denied** until a policy allows it, and an explicit **Deny always wins**.

```mermaid
flowchart TD
    R([User makes a request]) --> D{"Is there an explicit<br/>Deny in any policy?"}
    D -->|Yes| X["⛔ Denied"]
    D -->|No| A{"Is there an explicit<br/>Allow for this action?"}
    A -->|Yes| OK["✅ Allowed"]
    A -->|No| ID["⛔ Denied<br/>(implicit deny)"]
```

This explains both test results: **before** the policy, nothing was allowed, so EC2 fell through to the implicit deny. **After** attaching AmazonEC2FullAccess, EC2 actions had an explicit Allow, but IAM actions still did not.

**What a policy looks like.** A simplified version of the EC2 full-access idea:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
```

| Part | Meaning |
|------|---------|
| `Effect` | `Allow` or `Deny` |
| `Action` | Which API actions; `ec2:*` means every EC2 action |
| `Resource` | Which resources; `*` means all of them |


##  Common Problems and Fixes

| Problem | Cause | Fix |
|---------|-------|-----|
| IAM user can't sign in | Using the root sign-in page instead of the IAM user sign-in URL | Use the account-specific sign-in URL, or choose **IAM user** and enter the account ID |
| Signing in as the IAM user logs out the root user | Both sessions in the same browser window | Use an incognito/private window for the IAM user |
| "Not authorized" when launching an instance | No policy attached yet | Attach a policy that allows the action (here AmazonEC2FullAccess) |
| Changes don't show in the IAM user's window | Page not refreshed after attaching the policy | Refresh the console page |


##  Security Best Practices

- [x] Use an IAM user instead of the root user for daily work
- [x] Start with no permissions and add only what is needed
- [ ] Use a narrower policy than full access in real environments (e.g. read-only)
- [ ] Require a new password at first sign-in for real users
- [ ] Enable **MFA** for every user with console access
- [ ] Manage permissions with **groups** instead of attaching policies directly
- [ ] Terminate test instances and delete unused users after the lab


## ✅ Conclusion

This lab showed that a new IAM user can sign in but can do nothing until a policy grants permissions. After attaching **AmazonEC2FullAccess**, the user could launch EC2 instances but still could not manage IAM, which demonstrates least privilege and how AWS evaluates permissions.

➡️ **Next:** [IAM Demo 2 – Check an IAM user's access with the AWS CLI](../06-iam-user-aws-cli-access)
