---
title: "Setting Up a Custom Virtual Private Cloud (VPC)"
date: "`r Sys.Date()`"
weight: 1
pre: "<b>2.1 </b>"
chapter: false
---

#### **What is a Virtual Private Cloud?**

Amazon Virtual Private Cloud (VPC) allows you to create an isolated, private network on AWS. In this lab, we will set up a **VPC** with the following configuration:

- **2 Availability Zones (AZs)**
- **2 Public Subnets** and **2 Private Subnets**
- Assign an **EC2 Instance** to the **Public Subnet**, enabling Internet access via an Internet Gateway.

---

#### **Steps to Deploy a Virtual Private Cloud**

#### **Step 1: Create a VPC**

1. Log in to the **AWS Management Console**.
2. Navigate to the **VPC Dashboard** from the left-hand menu and select **Your VPCs**.
3. Click on the **Create VPC** button.

   ![vpc-dashboard](</images/2-preparation-(root)/1-setting-up-vpc/image.png>)

4. In the **Create VPC** screen:
   - Under **VPC Settings**, set **Resources to Create** to **VPC and more**.
   - Enter a name for the VPC, keep the default settings, and click **Create VPC**.

{{% notice tip %}}  
Review the **Preview** pane on the right to check the resources being created, including the VPC, Subnets, Route Tables, and Network Connections.  
{{% /notice %}}

![creating-vpc](</images/2-preparation-(root)/1-setting-up-vpc/image-1.png>)

5. Once completed, a success notification will appear.

   ![successful-vpc](</images/2-preparation-(root)/1-setting-up-vpc/image-2.png>)

6. Review your VPC details in the **VPC Details** tab.

   ![vpc-details](</images/2-preparation-(root)/1-setting-up-vpc/image-3.png>)

---

#### **Step 2: Enable IPv4 Address Assignment for the Public Subnet**

1. From the left-hand menu, go to **Subnets**.
2. Locate the subnet with a name containing "public1".
3. Select the subnet and click **Edit Subnet Settings**.

   ![edit-subnet-settings](</images/2-preparation-(root)/1-setting-up-vpc/image-4.png>)

4. In the **Subnet Settings** screen, enable **Auto-assign public IPv4 address**.
5. Click **Save changes** to apply.

   ![enable-ipv4](</images/2-preparation-(root)/1-setting-up-vpc/image-5.png>)

6. A success message will confirm the changes.

   ![assign-successfully](</images/2-preparation-(root)/1-setting-up-vpc/image-6.png>)
