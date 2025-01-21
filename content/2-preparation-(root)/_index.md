---
title: "Preparation"
date: "`r Sys.Date()`"
weight: 2
pre : "<b>2. </b>"
chapter: false
---

# **Preparation**  

In this step, we will set up the required environment, including creating a **Custom VPC**, launching a **Linux EC2 Instance**, assigning an **IAM Role** to the EC2 instance, and installing tools such as **AWS CLI v2** and **jq** on the EC2 instance.  

{{% notice info %}}  
Since **Amazon S3 Tables** is a new feature, it is only supported in two regions: US East (Ohio, N. Virginia) and US West (Oregon). For this workshop, we will use the **US East (Ohio, N. Virginia)** region.  
{{% /notice %}}  

![region](/images/2-preparation-(root)/image.png)  

### **Contents**  

1. [Setting Up VPC](1-setting-up-vpc)  
2. [Launching a Linux EC2 Instance](2-deploying-linux-EC2)  
3. [Installing Related Tools](3-installing-tools)