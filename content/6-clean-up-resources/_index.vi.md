---
title: "Dọn dẹp tài nguyên"
date: "`r Sys.Date()`"
weight: 6
pre: "<b>6. </b>"
chapter: false
---


### 6. Dọn dẹp tài nguyên

Chúc mừng bạn đã hoàn thành! Bây giờ chúng ta sẽ tiến hành dọn dẹp các tài nguyên để tránh phát sinh chi phí không cần thiết.

Quá trình dọn dẹp sẽ được thực hiện theo thứ tự sau: Xóa Table > Xóa Namespace > Xóa S3 Table Bucket > Xóa EC2 Instance > Xóa Security Group > Xóa VPC > Xóa IAM Role.

Bắt đầu bằng cách SSH vào EC2 instance của bạn.

1. **Xóa Table**

   Thay thế `--table-bucket-arn` bằng ARN của bucket bạn.

```shell
aws s3tables delete-table \
--table-bucket-arn arn:aws:s3tables:us-east-1:242201280000:bucket/jbarr-table-bucket-2 \
--namespace mydata --name table1
```

2. **Xóa Namespace**

```shell
aws s3tables delete-namespace \
--table-bucket-arn arn:aws:s3tables:us-east-1:242201280000:bucket/jbarr-table-bucket-2 \
--namespace mydata
```

3. **Xóa S3 Table Buckets**

```shell
aws s3tables delete-table-bucket \
--table-bucket-arn arn:aws:s3tables:us-east-1:242201280000:bucket/jbarr-table-bucket-2
```

<!-- Hình ảnh 1 -->

4. **Xóa EC2 Instance**

   Truy cập EC2 Dashboard, chọn EC2 instance của bạn và sử dụng hành động "Terminate" để xóa instance.

<!-- Hình ảnh 2 -->

<!-- Hình ảnh 3 -->

5. **Xóa Security Group**

   Truy cập VPC Dashboard, chọn "Security Groups" trong thanh điều hướng bên trái, chọn security group `demo-s3-tables-sg`, nhấn vào dropdown actions, chọn "Delete Security Group."

<!-- Hình ảnh 4 -->

6. **Xóa VPC**

   Truy cập VPC Dashboard, chọn "Your VPCs," chọn VPC `demo-s3-table-vpc`, nhấn vào dropdown actions, chọn "Delete VPC," nhập `delete` để xác nhận và tiếp tục xóa.

<!-- Hình ảnh 5 -->

<!-- Hình ảnh 6 -->

7. **Xóa IAM Role**

   Truy cập IAM Service Dashboard, chọn "Roles" trong thanh điều hướng bên trái, tìm kiếm `ec2-s3-tables-role`, và chọn "Delete."

<!-- Hình ảnh 7 -->

---

Chúc mừng bạn đã hoàn tất! Nếu gặp phải vấn đề hoặc cần hỗ trợ trong việc khắc phục sự cố, đừng ngần ngại liên hệ với tôi qua [LinkedIn](https://linkedin.com/in/minhnghia2k3) hoặc gửi email cho tôi tại [nghialm2603@gmail.com](mailto:nghialm2603@gmail.com).