---
title: "Quản Lý và Truy Vấn Dữ Liệu Với Amazon S3 Tables"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

# Quản Lý và Truy Vấn Dữ Liệu Với Amazon S3 Tables


#### **Tổng Quan**

Trong workshop này, chúng ta sẽ khám phá **[Amazon S3 Tables](https://aws.amazon.com/s3/features/tables/)** – một giải pháp tối ưu hóa lưu trữ dữ liệu dưới dạng bảng, được thiết kế để đáp ứng nhu cầu **phân tích dữ liệu ở quy mô lớn**. Một số trường hợp sử dụng tiêu biểu bao gồm: lưu trữ dữ liệu giao dịch mua bán hàng ngày và xử lý Streaming Data. Để thuận tiện trong việc truy vấn dữ liệu, Amazon S3 Tables dễ dàng tích hợp với các công cụ mạnh mẽ như **Amazon Athena, Amazon EMR, và Apache Spark.**

{{< youtube bLB_cl-u3jM >}}


---

#### **Mục Tiêu**

- Nắm vững cách tổ chức và quản lý dữ liệu trên Amazon S3 Tables.
- Thực hiện tạo Amazon S3 Tables thông qua **AWS Management Console** và **Command Line Interface (CLI)**.
- Thực hành truy vấn dữ liệu bằng cách tích hợp với các dịch vụ như **Amazon Athena, Amazon EMR, hoặc Apache Spark**.
- Xây dựng kỹ năng quản lý tài nguyên AWS, bao gồm thực hành dọn dẹp tài nguyên sau khi hoàn thành để tối ưu chi phí.

---

#### **Yêu Cầu**

Trước khi bắt đầu, bạn cần đảm bảo:

1. **Tài khoản AWS**:
   - Đăng ký tài khoản và kích hoạt một **IAM User** với quyền truy cập cần thiết.
2. **Kiến thức cơ bản**:
   - Có hiểu biết cơ bản về Linux, Amazon S3, IAM và EC2.
3. **Môi trường làm việc**:
   - Máy tính cá nhân với quyền quản trị và kết nối internet ổn định.
   - Cài đặt các công cụ sau:
     - **AWS CLI v2**: Dùng để tương tác với AWS thông qua dòng lệnh.
     - **jq**: Công cụ xử lý tệp JSON.

---

### **Pricing**

{{% notice warning %}}  
**LƯU Ý:** Việc triển khai workshop này có thể phát sinh chi phí. Để tối ưu hóa ngân sách, hãy đảm bảo quản lý tài nguyên chặt chẽ và dọn dẹp chúng sau khi hoàn thành.  
{{% /notice %}}

#### **Tài nguyên sử dụng**
Để triển khai workshop, chúng ta sử dụng **EC2 instance loại t2.medium**, cung cấp:  
- **2 vCPU**: Phù hợp cho các tác vụ quản lý và xử lý dữ liệu.  
- **4 GB RAM**: Đáp ứng nhu cầu truy vấn và thao tác dữ liệu một cách hiệu quả.  

#### **Chi phí liên quan đến S3 Tables**
1. **Storage Pricing**:  
   - $0.025 cho mỗi **1,000 objects**.  

2. **Requests Pricing**:  
   - $0.005 cho mỗi **1,000 requests** (PUT, COPY, POST, LIST).  
   - $0.0004 cho mỗi **1,000 requests** (GET, SELECT).  

3. **Maintenance Pricing**:  
   - **Compaction - Objects**: $0.004 mỗi **1,000 objects** được xử lý.  
   - **Compaction - Data Processed**: $0.05 mỗi GB dữ liệu được xử lý.  

![s3-tables-pricing](/images/image.png)

#### **Ước tính tổng chi phí**
- **EC2 Instance**: Với mức giá **$0.0464/giờ**, tổng chi phí sử dụng trong **24 giờ** là khoảng **$1.11/ngày**.  
- **S3 Tables**: Phụ thuộc vào khối lượng dữ liệu và số lượng requests trong quá trình thao tác.  

#### **Tối ưu hóa chi phí**
- Giới hạn thời gian triển khai workshop và dọn dẹp tài nguyên ngay sau khi hoàn thành.  
- Nếu quản lý tốt, tổng chi phí có thể chỉ ở mức vài đô la, đảm bảo tiết kiệm và hiệu quả cho ngân sách.  

---

### **Nội Dung Chính**

1. [Giới thiệu](1-introduction)
2. [Chuẩn bị](<2-preparation-root/>)  
3. [Truy cập buckets và tables sử dụng AWS Management Console](3-accessing-buckets-and-tables-via-command-line/)  
4. [Truy cập buckets và tables sử dụng Command Line Interface](4-accessing-buckets-and-tables-via-aws-management-console/)  
5. [Kết luận](5-conclusion/)  
6. [Dọn dẹp tài nguyên](6-clean-up-resources/)  

![S3-tables-architecture](/images/S3-Tables-Architecture.png)