---
title: "Triển khai Linux Elastic Compute Cloud"
date: "`r Sys.Date()`"
weight: 2
pre: "<b>2.2 </b>"
chapter: false
---

### 2.2. Triển khai Linux Elastic Compute Cloud

#### Tạo Security Group

Security Group hoạt động ở Subnet Level, quản lý inbound và outbound traffic đến tài nguyên bên trong VPC. Trong bài lab này, bạn sẽ:

- Tạo Security Group với inbound rules cho phép **SSH** (Source: MY IP ADDRESS) và **ALL ICMP IPv4** (Source: Everywhere).
- Outbound rules cho phép tất cả traffic.

1. Truy cập **VPC Dashboard** > **Security Groups** > Chọn **Create Security Group**.

![alt text](image.png)

2. Trong giao diện **Create Security Group**:

   - Điền **Security Group name**, **Description**, chọn VPC đã tạo.
   - **Inbound Rules**: Thêm 2 rule:
     - **SSH**: Source là **MY IP ADDRESS**.
     - **ALL ICMP IPv4**: Source là **Everywhere**.
   - **Outbound Rules**: Chọn **All Traffic**.

3. Nhấn **Create Security Group**.

![alt text](image-1.png)
![alt text](image-2.png)

4. Kiểm tra giao diện khi tạo thành công.

![alt text](image-3.png)

---

#### Triển khai Linux EC2 Instance

{{% notice info %}}  
**Lưu ý:** Với mục đích tiết kiệm chi phí, bạn có thể dùng **t2.micro** (Free Tier). Tuy nhiên, nếu triển khai trong **us-east-1**, độ trễ và hiệu năng của instance có thể không đủ để chạy bài lab này. Đề xuất sử dụng **t2.medium** để đảm bảo hiệu năng.  
{{% /notice %}}

**Cấu hình EC2 Instance**:

- Loại: **t2.medium**
- Tài nguyên: **2 vCPU**, **4 GB RAM**, Network Bandwidth trung bình.

**Bước triển khai:**

1. Truy cập **EC2 Dashboard** > Nhấn **Launch Instance**.

![alt text](image-4.png)

2. Trong giao diện **Launch an Instance**:
   - **Name and Tags**: Nhập tên instance.
   - **Application and OS Images**: Chọn **Amazon Linux 2023 AMI**.
   - **Instance Type**: Chọn **t2.medium**.
   - **Key Pair**: Nhấn **Create New Key Pair**.

![alt text](image-5.png)

![alt text](image-6.png)

3. Trong giao diện **Create Key Pair**:
   - Điền **Key Pair Name**, chọn **RSA**, định dạng **.pem**.
   - Nhấn **Create Key Pair** và lưu tệp vào thư mục máy của bạn.

![alt text](image-7.png)

4. **Network Settings**:

   - Chọn **Edit**.
   - **VPC**: Chọn VPC đã tạo.
   - **Subnet**: Chọn subnet **public1**.
   - Bật **Auto-assign public IP**.
   - **Firewall**: Chọn **Security Group** đã tạo.

5. Nhấn **Launch Instance** để khởi tạo.

![alt text](image-8.png)

6. Kiểm tra giao diện khi EC2 được tạo thành công.

![alt text](image-9.png)

---

#### Kết nối EC2 Instance qua SSH

1. Trong **EC2 Dashboard**, chọn instance vừa tạo, nhấn **Connect**.
2. Trong giao diện **Connect to Instance**, chuyển sang tab **SSH Client** và sao chép lệnh SSH mẫu.

```bash
ssh -i "demo-s3-tables-kp.pem" ec2-user@ec2-<instance-public-ip>.compute-<region>.amazonaws.com
```

![alt text](image-10.png)

3. Truy cập thư mục chứa key pair đã lưu, dán lệnh vào terminal để kết nối.

4. Xác nhận kết nối thành công.

![alt text](image-11.png)

---

#### Tạo IAM Role và gắn vào EC2 Instance

**Bước 1: Tạo IAM Role**

1. Truy cập **IAM Dashboard** > Chọn **Roles** > **Create Role**.

![alt text](image-12.png)

2. Trong **Select Trusted Entity**:
   - Chọn **AWS Service** > Use case: **EC2**.

![alt text](image-13.png)

3. Trong **Add Permissions**:
   - Tìm kiếm và thêm quyền **AmazonS3FullAccess** và **AmazonS3TablesFullAccess**.

![alt text](image-14.png)

   - Nhấn **Next** để review và đặt tên cho role.

![alt text](image-15.png)

   - Nhấn **Create Role** để hoàn tất.

![alt text](image-16.png)



**Bước 2: Attach IAM Role vào EC2 Instance**

1. Truy cập chi tiết EC2 Instance, chọn **Actions** > **Security** > **Modify IAM Role**.

![alt text](image-17.png)

2. Trong giao diện **Modify IAM Role**, chọn role vừa tạo > Nhấn **Update IAM Role**.

![alt text](image-18.png)

3. Kiểm tra giao diện khi gắn IAM Role thành công.

![alt text](image-19.png)