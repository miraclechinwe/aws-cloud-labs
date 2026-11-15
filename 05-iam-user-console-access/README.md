# Lab 05: Creating an IAM User with Console Access and Permissions

## Objective

In this lab, I created an IAM (Identity and Access Management) user in AWS, gave the user access to the AWS Management Console, required a password reset at first sign-in, and granted permissions by attaching a policy.

The goal of this lab is to demonstrate how to give a person their own identity in an AWS account instead of sharing the root user, while following the **principle of least privilege**.

## Key Concepts

- **IAM User** – an identity for one person or application, with its own credentials
- **Console access** – lets the user sign in to the AWS Management Console with a password
- **IAM Policy** – a JSON document that allows or denies specific actions on specific resources
- **Least privilege** – give users only the permissions they need to do their job


## 1. Open the IAM Console

I signed in to the AWS Management Console, searched for **IAM**, and opened **Users** from the left menu. I then selected **Create user**.

<!-- 📸 Screenshot: IAM dashboard / Users page -->


## 2. Set User Details and Enable Console Access

I entered a user name and ticked **Provide user access to the AWS Management Console**, then selected **I want to create an IAM user**.

For the console password, I chose a password and enabled **Users must create a new password at next sign-in**, so the user sets their own password the first time they log in.

<!-- 📸 Screenshot: User details page with console access options -->


## 3. Set Permissions

On the **Set permissions** page, AWS gives three options:

- **Add user to group** – the user gets the permissions of the group (best practice for teams)
- **Copy permissions** – copy groups and policies from an existing user
- **Attach policies directly** – attach a managed policy to this user only

I selected **Attach policies directly** and attached the **[policy name]** policy.

<!-- 📸 Screenshot: Set permissions page with the selected policy -->

> **Note:** For this lab, a policy was attached directly to the user. In a real environment, it is better to attach policies to **groups** and add users to those groups, so permissions are easier to manage.


## 4. Review and Create the User

I reviewed the user details and permissions summary, then selected **Create user**.

On the **Retrieve password** page, AWS showed the **console sign-in URL**, the user name and the password. This information can also be downloaded as a `.csv` file.

<!-- 📸 Screenshot: Review page / user created successfully (hide the password and account ID) -->


## 5. Reset / Manage Console Access

To manage the user's console access later, I opened the user, went to the **Security credentials** tab, and selected **Manage console access**.

From here, an administrator can:

- **Reset the password** (auto-generated or custom)
- Require a new password at next sign-in
- **Disable** console access completely

<!-- 📸 Screenshot: Security credentials tab → Manage console access -->


## 6. Verify the Permissions

I opened the **Permissions** tab of the user to confirm the policy was attached. Permissions can also be added or removed here with **Add permissions** and **Remove**.

<!-- 📸 Screenshot: Permissions tab showing the attached policy -->


## 7. Sign In as the New IAM User

I opened the console sign-in URL in a private browser window, signed in with the IAM user name and password, and was asked to set a new password.

After signing in, I tested the permissions: actions allowed by the policy worked, and actions outside the policy showed an **access denied** message.

<!-- 📸 Screenshot: IAM user sign-in page / change password page -->
<!-- 📸 Screenshot: Access allowed vs access denied -->


## 8. Clean Up

After the lab, I deleted the IAM user to keep the account secure.


## Conclusion

This lab demonstrated how to create an IAM user, enable and reset console access, and control what the user can do by attaching policies. Using individual IAM users with least-privilege permissions is safer than sharing the root account.
