---
title: "Chuẩn bị"
date: "`r Sys.Date()`"
weight: 2
pre : "<b>2. </b>"
chapter: false
---

### 2. Chuẩn bị 

Trong bước này, chúng ta sẽ thiết lập môi trường cần thiết, bao gồm **Custom VPC**, khởi tạo **Linux EC2 Instance**, tạo **IAM Role** gán vào EC2 và cài đặt các công cụ như **AWS CLI v2**, **jq** trên EC2 Instance.

{{% notice info %}}
Vì **Amazon S3 Tables** là tính năng mới nên chỉ hỗ trợ 2 regions: US East (Ohio, N. Virginia) và US West (Oregon) AWS Regions. Ở bài workshop này mình sẽ sử dụng region **US East (Ohio, N. Virginia)**
{{% /notice %}}

![region](/images/2-preparation-(root)/image.png)

#### Nội Dung
1. [Thiết lập VPC](1-setting-up-vpc)
2. [Khởi tạo Linux EC2 Instance](2-deploying-linux-EC2)
3. [Cài đặt các công cụ liên quan](3-installing-tools)
