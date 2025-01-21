---
title: "Deploying Linux Elastic Compute Cloud (EC2)"
date: "`r Sys.Date()`"
weight: 2
pre: "<b>2.2 </b>"
chapter: false
---

#### **Create a Security Group**

A Security Group operates at the subnet level to manage inbound and outbound traffic for resources in the VPC. In this lab, we will:

- Create a Security Group with inbound rules to allow:
  - **SSH** (Source: **MY IP ADDRESS**).
  - **ALL ICMP IPv4** (Source: **Everywhere**).
- Set outbound rules to allow all traffic.

#### **Steps:**

1. Navigate to **VPC Dashboard** > **Security Groups** > Click **Create Security Group**.

   ![vpc-dashboard](</images/2-preparation-(root)/2-deploying-linux-EC2/image.png>)

2. In the **Create Security Group** screen:

   - Fill in the **Security Group Name** and **Description**.
   - Select the VPC created earlier.
   - Add **Inbound Rules**:
     - **SSH**: Source = **MY IP ADDRESS**.
     - **ALL ICMP IPv4**: Source = **Everywhere**.
   - For **Outbound Rules**, choose **All Traffic**.

3. Click **Create Security Group**.

   ![create-sg-1](</images/2-preparation-(root)/2-deploying-linux-EC2/image-1.png>)  
   ![create-sg-2](</images/2-preparation-(root)/2-deploying-linux-EC2/image-2.png>)

4. A confirmation screen will appear after successful creation.

   ![create-sg-successfully](</images/2-preparation-(root)/2-deploying-linux-EC2/image-3.png>)

---

### **Deploy Linux EC2 Instance**

{{% notice info %}}  
**Note:** For cost savings, use **t2.micro** (Free Tier). However, in **us-east-1**, performance may not be adequate. Using **t2.medium** is recommended for better performance.  
{{% /notice %}}

#### **Instance Configuration:**

- Type: **t2.medium**.
- Resources: **2 vCPU**, **4 GB RAM**, Medium Network Bandwidth.

#### **Steps to Launch:**

1. Go to **EC2 Dashboard** and click **Launch Instance**.

   ![launch-ec2-instance](</images/2-preparation-(root)/2-deploying-linux-EC2/image-4.png>)

2. In the **Launch an Instance** screen:

   - **Name and Tags**: Enter a name for your instance.
   - **Application and OS Images**: Select **Amazon Linux 2023 AMI**.
   - **Instance Type**: Choose **t2.medium**.
   - **Key Pair**: Click **Create New Key Pair**.

   ![creating-ec2-1](</images/2-preparation-(root)/2-deploying-linux-EC2/image-5.png>)  
   ![creating-ec2-2](</images/2-preparation-(root)/2-deploying-linux-EC2/image-6.png>)

3. In the **Create Key Pair** dialog:

   - Provide a **Key Pair Name**, select **RSA**, and set format to **.pem**.
   - Click **Create Key Pair** and save the file to your computer.

   ![create-key-paris](</images/2-preparation-(root)/2-deploying-linux-EC2/image-7.png>)

4. **Network Settings**:

   - Select **Edit**.
   - **VPC**: Choose the VPC you created earlier.
   - **Subnet**: Select **public1**.
   - Enable **Auto-assign Public IP**.
   - For **Firewall**, select the Security Group created earlier.

5. Click **Launch Instance**.

   ![network-settings](</images/2-preparation-(root)/2-deploying-linux-EC2/image-8.png>)

6. A confirmation screen will indicate the instance was created successfully.

   ![create-ec2-successfully](</images/2-preparation-(root)/2-deploying-linux-EC2/image-9.png>)

---

### **Connect to EC2 Instance via SSH**

1. In the **EC2 Dashboard**, select the instance and click **Connect**.
2. Go to the **SSH Client** tab and copy the sample SSH command.

```bash
ssh -i "demo-s3-tables-kp.pem" ec2-user@ec2-<instance-public-ip>.compute-<region>.amazonaws.com
```

![ec2-ssh](</images/2-preparation-(root)/2-deploying-linux-EC2/image-10.png>)

3. Navigate to the directory containing your key pair file and paste the SSH command into your terminal.
4. Confirm a successful connection.

   ![ssh-successfully](</images/2-preparation-(root)/2-deploying-linux-EC2/image-11.png>)

---

### **Create an IAM Role and Attach to EC2 Instance**

#### **Step 1: Create IAM Role**

1. Go to **IAM Dashboard** > Click **Roles** > **Create Role**.

   ![creating-role](</images/2-preparation-(root)/2-deploying-linux-EC2/image-12.png>)

2. In **Select Trusted Entity**:

   - Choose **AWS Service**.
   - Use case: **EC2**.

   ![creating-role-interface](</images/2-preparation-(root)/2-deploying-linux-EC2/image-13.png>)

3. In **Add Permissions**:

   - Add the permissions **AmazonS3FullAccess** and **AmazonS3TablesFullAccess**.

   ![add-permissions](</images/2-preparation-(root)/2-deploying-linux-EC2/image-14.png>)

4. Review and provide a name for the role.
5. Click **Create Role**.

   ![reviewing-and-naming](</images/2-preparation-(root)/2-deploying-linux-EC2/image-15.png>)  
   ![create-role-successfully](</images/2-preparation-(root)/2-deploying-linux-EC2/image-16.png>)

---

#### **Step 2: Attach IAM Role to EC2 Instance**

1. Open the instance details, go to **Actions** > **Security** > **Modify IAM Role**.

   ![ec2-details](</images/2-preparation-(root)/2-deploying-linux-EC2/image-17.png>)

2. In the **Modify IAM Role** screen:

   - Select the role you just created.
   - Click **Update IAM Role**.

   ![update-iam-role](</images/2-preparation-(root)/2-deploying-linux-EC2/image-18.png>)

3. A confirmation message will show a successful role attachment.

   ![attach-role-successfully](</images/2-preparation-(root)/2-deploying-linux-EC2/image-19.png>)
