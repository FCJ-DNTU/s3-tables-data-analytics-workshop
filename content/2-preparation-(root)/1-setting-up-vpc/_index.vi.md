---
title: "Thiết lập Custom Virtual Private Cloud (VPC)"
date: "`r Sys.Date()`"
weight: 1
pre : "<b>2.1 </b>"
chapter: false
---


### 2.1. Thiết lập Custom Virtual Private Cloud  

#### Virtual Private Cloud là gì?  
Amazon Virtual Private Cloud (VPC) cung cấp khả năng cách ly mạng lưới riêng biệt trên nền tảng AWS. Trong bài lab này, bạn sẽ triển khai một **VPC** với cấu hình:  
- **2 Availability Zones (AZs)**  
- **2 Public Subnets** và **2 Private Subnets**  
- Tạo **Public Subnet** và gán EC2 Instance vào đó, cho phép kết nối ra Internet thông qua Internet Gateway.  

#### Triển khai Virtual Private Cloud  

**Bước 1: Khởi tạo VPC**  
1. Đăng nhập vào **AWS Management Console**.  
2. Truy cập **VPC Dashboard** từ thanh điều hướng bên trái và chọn **Your VPCs**.  
3. Nhấp vào nút **Create VPC**.  

    ![vpc-dashboard](/images/2-preparation-(root)/1-setting-up-vpc/image.png)

4. Trong giao diện **Create VPC**, tại mục **VPC Settings**, chọn **Resources to Create** là **VPC and more**.  
5. Nhập tên cho VPC, giữ nguyên các tùy chọn mặc định, và nhấp **Create VPC** để hoàn tất.  

{{% notice tip %}}
 Xem phần **Preview** bên phải để kiểm tra tổng quan tài nguyên sẽ được tạo bao gồm VPC, Subnets, Route Tables, và Network Connections.  
{{% /notice %}}

![creating-vpc](/images/2-preparation-(root)/1-setting-up-vpc/image-1.png)

6. Sau khi hoàn tất, bạn sẽ thấy thông báo tạo VPC thành công.  

    ![successful-vpc](/images/2-preparation-(root)/1-setting-up-vpc/image-2.png)

7. Kiểm tra chi tiết VPC trong tab **VPC Details**.  

    ![vpc-details](/images/2-preparation-(root)/1-setting-up-vpc/image-3.png)

**Bước 2: Gán địa chỉ IPv4 cho Public Subnet**  
1. Từ thanh điều hướng bên trái, chọn **Subnets**.  
2. Tìm kiếm subnet có tên chứa từ khóa "public1".  
3. Nhấp chọn Subnet và chọn **Edit Subnet Settings**.  

    ![edit-subnet-settings](/images/2-preparation-(root)/1-setting-up-vpc/image-4.png)

4. Trong giao diện **Subnet Settings**, bật tùy chọn **Enable auto-assign public IPv4 address**.  
5. Nhấn **Save changes** để lưu thay đổi.  

    ![enable-ipv4](/images/2-preparation-(root)/1-setting-up-vpc/image-5.png)

6. Sau khi hoàn tất, giao diện sẽ hiển thị thông báo thay đổi thành công.  

    ![assign-successfully](/images/2-preparation-(root)/1-setting-up-vpc/image-6.png)