---
title: "Managing and Querying Data with Amazon S3 Tables"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

#### **Overview**  

In this workshop, we will explore **[Amazon S3 Tables](https://aws.amazon.com/s3/features/tables/)**—an optimized solution for storing tabular data, specifically designed to meet the needs of **large-scale data analytics**. Typical use cases include storing daily transaction data and processing streaming data. To make data querying convenient, Amazon S3 Tables seamlessly integrates with powerful tools like **Amazon Athena, Amazon EMR, and Apache Spark**.  

{{< youtube bLB_cl-u3jM >}}  

---  

#### **Objectives**  

- Learn how to organize and manage data using Amazon S3 Tables.  
- Create Amazon S3 Tables via the **AWS Management Console** and the **Command Line Interface (CLI)**.  
- Practice querying data by integrating with services like **Amazon Athena, Amazon EMR, or Apache Spark**.  
- Develop AWS resource management skills, including resource cleanup to optimize costs after completion.  

---  

#### **Requirements**  

Before starting, ensure you have:  

1. **AWS Account**:  
   - Register and activate an **IAM User** with necessary access permissions.  
2. **Basic Knowledge**:  
   - Familiarity with Linux, Amazon S3, IAM, and EC2.  
3. **Work Environment**:  
   - A personal computer with administrative access and a stable internet connection.  
   - The following tools installed:  
     - **AWS CLI v2**: For interacting with AWS via command line.  
     - **jq**: A tool for processing JSON files.  

---  

### **Pricing**  

{{% notice warning %}}  
**NOTE:** This workshop may incur costs. To optimize your budget, ensure resources are tightly managed and cleaned up after completion.  
{{% /notice %}}  

#### **Resources Used**  
For this workshop, we’ll use a **t2.medium EC2 instance**, which provides:  
- **2 vCPUs**: Ideal for data management and processing tasks.  
- **4 GB RAM**: Suitable for efficient data querying and manipulation.  

#### **Costs Related to S3 Tables**  
1. **Storage Pricing**:  
   - $0.025 per **1,000 objects**.  

2. **Requests Pricing**:  
   - $0.005 per **1,000 requests** (PUT, COPY, POST, LIST).  
   - $0.0004 per **1,000 requests** (GET, SELECT).  

3. **Maintenance Pricing**:  
   - **Compaction - Objects**: $0.004 per **1,000 objects** processed.  
   - **Compaction - Data Processed**: $0.05 per GB of data processed.  

![s3-tables-pricing](/images/image.png)  

#### **Estimated Total Costs**  
- **EC2 Instance**: At a rate of **$0.0464/hour**, the total cost for **24 hours** is approximately **$1.11/day**.  
- **S3 Tables**: Costs will depend on the volume of data and the number of requests during operations.  

#### **Cost Optimization Tips**  
- Limit the duration of the workshop and clean up resources immediately after completion.  
- With proper management, total costs can be kept to just a few dollars, ensuring an efficient and budget-friendly experience.  

---  

### **Main Content**  

1. [Introduction](1-introduction)  
2. [Preparation](<2-preparation-root/>)  
3. [Accessing Buckets and Tables via AWS Management Console](3-accessing-buckets-and-tables-via-command-line/)  
4. [Accessing Buckets and Tables via Command Line Interface](4-accessing-buckets-and-tables-via-aws-management-console/)  
5. [Conclusion](5-conclusion/)  
6. [Cleaning Up Resources](6-clean-up-resources/)  

![S3-tables-architecture](/images/S3-Tables-Architecture.png)  
