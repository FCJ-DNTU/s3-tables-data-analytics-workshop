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

   Thay thế `<arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2>` bằng ARN của bucket bạn.

```shell
aws s3tables delete-table \
--table-bucket-arn <arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2> \
--namespace mydata --name table1
```

2. **Xóa Namespace**

```shell
aws s3tables delete-namespace \
--table-bucket-arn <arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2> \
--namespace mydata
```

3. **Xóa S3 Table Buckets**

```shell
aws s3tables delete-table-bucket \
--table-bucket-arn <arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2>
```

![delete-s3-table-buckets](/images/6-clean-up-resources/image.png)

4. **Xóa EC2 Instance**

   Truy cập EC2 Dashboard, chọn EC2 instance của bạn và sử dụng hành động "Terminate" để xóa instance.

![delete-ec2-instance-1](/images/6-clean-up-resources/image-1.png)

![delete-ec2-instance-2](/images/6-clean-up-resources/image-2.png)

5. **Xóa Security Group**

   Truy cập VPC Dashboard, chọn "Security Groups" trong thanh điều hướng bên trái, chọn security group `demo-s3-tables-sg`, nhấn vào dropdown actions, chọn "Delete Security Group."

![delete-sg](/images/6-clean-up-resources/image-3.png)

6. **Xóa VPC**

   Truy cập VPC Dashboard, chọn "Your VPCs," chọn VPC `demo-s3-table-vpc`, nhấn vào dropdown actions, chọn "Delete VPC," nhập `delete` để xác nhận và tiếp tục xóa.

![delete-vpc-1](/images/6-clean-up-resources/image-4.png)

![delete-vpc-2](/images/6-clean-up-resources/image-5.png)

7. **Xóa IAM Role**

   Truy cập IAM Service Dashboard, chọn "Roles" trong thanh điều hướng bên trái, tìm kiếm `ec2-s3-tables-role`, và chọn "Delete."

![delete-iam-role](/images/6-clean-up-resources/image-6.png)

---

Chúc mừng bạn đã hoàn tất! Nếu gặp phải vấn đề hoặc cần hỗ trợ trong việc khắc phục sự cố, đừng ngần ngại liên hệ với tôi qua [LinkedIn](https://linkedin.com/in/minhnghia2k3) hoặc gửi email hỗ trợ tại [nghialm2603@gmail.com]().