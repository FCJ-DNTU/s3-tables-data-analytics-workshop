---
title: "Kết luận"
date: "`r Sys.Date()`"
weight: 5
pre: "<b>5. </b>"
chapter: false
---

### 5. Kết luận

Workshop này đã hướng dẫn bạn cách tạo và quản lý **Amazon S3 Tables** thông qua cả giao diện AWS Management Console và CLI. Chúng ta đã thực hiện các bước:  
- Tạo **S3 Table Buckets** để lưu trữ dữ liệu theo cấu trúc.  
- Tích hợp **Apache Spark** với **S3 Tables Catalog** để truy vấn và xử lý dữ liệu lớn.  
- Chèn và truy vấn dữ liệu mẫu từ **Iceberg Tables** thông qua Spark-Shell.  

#### Lợi ích của Amazon S3 Tables:  
1. **Hiệu suất truy vấn tối ưu**: Nhờ khả năng phân vùng và xử lý dữ liệu hiệu quả, giúp giảm thời gian truy vấn đối với các bộ dữ liệu lớn.  
2. **Quản lý tự động**: S3 Tables hỗ trợ khả năng quản lý metadata, phiên bản dữ liệu và tự động cập nhật schema.  
3. **Tích hợp linh hoạt**: Làm việc liền mạch với các dịch vụ phân tích AWS như **AWS Glue**, **Amazon Athena**, và **Amazon EMR**.  

#### Lưu ý:  
Hiện tại, tính năng **Amazon S3 Tables** chỉ khả dụng tại một số vùng AWS (như **US East (N. Virginia)** và **US West (Oregon)**). Hãy kiểm tra tài liệu AWS chính thức để biết thêm chi tiết về tính khả dụng.  

#### Tài liệu tham khảo:  
- **Amazon S3 Pricing**: [https://aws.amazon.com/s3/pricing/](https://aws.amazon.com/s3/pricing/)  
- **AWS Glue Data Catalog Documentation**: [https://docs.aws.amazon.com/glue/latest/dg/populate-data-catalog.html](https://docs.aws.amazon.com/glue/latest/dg/populate-data-catalog.html)  
- **New Amazon S3 Tables: Storage optimized for analytics workloads**: [https://aws.amazon.com/blogs/aws/new-amazon-s3-tables-storage-optimized-for-analytics-workloads/](https://aws.amazon.com/blogs/aws/new-amazon-s3-tables-storage-optimized-for-analytics-workloads/)
- **Querying Amazon S3 tables with Apache Spark**: [https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-open-source-spark.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-open-source-spark.html)
- **Using Amazon S3 Tables with AWS analytics services**: [https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-aws.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-aws.html)

Với **Amazon S3 Tables**, bạn có thể khai thác tiềm năng của dữ liệu lớn một cách hiệu quả và tận dụng tối đa hệ sinh thái AWS.  