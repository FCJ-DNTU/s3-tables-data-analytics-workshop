---
title: "Giới thiệu"
date: "`r Sys.Date()`"
weight: 1
pre: "<b>1. </b>"
chapter: false
---

### 1. Giới thiệu

#### Khái niệm về Amazon S3

**Amazon Simple Storage Service (Amazon S3)** là dịch vụ lưu trữ đối tượng hàng đầu với khả năng mở rộng, tính sẵn sàng cao, và bảo mật tối ưu. Amazon S3 được ứng dụng trong nhiều trường hợp như lưu trữ data lakes, website, ứng dụng di động, sao lưu, khôi phục, và phân tích dữ liệu lớn.

#### Amazon S3 Tables là gì?

![s3-tables](/images/1-introduction/image-1.png)

**Amazon S3 Tables** cung cấp giải pháp lưu trữ dạng bảng đầu tiên trên nền tảng lưu trữ đối tượng đám mây với sự hỗ trợ tích hợp cho **[Apache Iceberg](https://iceberg.apache.org/)**. Đây là một dịch vụ được tối ưu hóa để lưu trữ và quản lý dữ liệu dạng bảng ở quy mô lớn.

#### Cách hoạt động của Amazon S3 Tables

- **Lưu trữ dữ liệu có cấu trúc với định dạng Apache Parquet**  
  S3 Tables được thiết kế đặc biệt để lưu trữ dữ liệu có cấu trúc, giúp tổ chức dữ liệu trong định dạng **Parquet**, một định dạng được tối ưu hóa cho phân tích dữ liệu lớn.

- **Tự động tối ưu hóa dữ liệu**  
  S3 Tables tự động thực hiện tối ưu hóa dữ liệu cơ bản thông qua quá trình **compaction**. Công việc này bao gồm viết lại và hợp nhất các tệp dữ liệu (Parquet), giúp cải thiện hiệu suất truy vấn và giảm thiểu chi phí lưu trữ.

#### Lợi ích của Amazon S3 Tables

- **Khả năng mở rộng vượt trội**  
  Đơn giản hóa quản lý data lakes ở mọi quy mô, từ quy mô nhỏ đến việc vận hành hàng ngàn bảng trong môi trường Iceberg.

- **Hiệu năng nâng cao**  
  Tăng hiệu suất truy vấn lên đến **3 lần** nhờ tối ưu hóa bảng liên tục so với các bảng Iceberg không được quản lý. Đồng thời, cải thiện khả năng xử lý giao dịch lên đến **10 lần** so với các bảng Iceberg lưu trữ trên S3 thông thường.

- **Dịch vụ được quản lý hoàn toàn**  
  Tự động thực hiện các tác vụ bảo trì như **compaction**, quản lý snapshot, và loại bỏ tệp không tham chiếu, tối ưu hóa hiệu quả truy vấn và chi phí theo thời gian.

- **Tích hợp liền mạch**  
  Truy cập các tính năng phân tích Iceberg nâng cao và truy vấn dữ liệu thông qua các dịch vụ AWS quen thuộc như **Amazon Athena**, **Redshift**, và **EMR**. S3 Tables cũng tương thích với nhiều công cụ mã nguồn mở phổ biến.

- **Bảo mật đơn giản hóa**  
  Tạo bảng như các tài nguyên chính thức trên AWS và áp dụng quyền truy cập để dễ dàng quản lý và kiểm soát bảo mật.

![s3-benefit](/images/1-introduction/image-2.png)

#### Các thành phần chính trong S3 Tables

1. **Table Buckets**: Loại bucket đặc biệt dành cho lưu trữ dữ liệu phân tích, hỗ trợ quản lý các bảng **[Iceberg](https://iceberg.apache.org/)** với nhiều schema khác nhau.
2. **Tables**: Tập dữ liệu có cấu trúc được tổ chức trong table bucket. Tables được quản lý hoàn toàn với các tính năng tự động như nén dữ liệu, xóa file không được tham chiếu, và quản lý snapshot.
3. **Namespaces**: Các nhóm table trong bucket, giúp tổ chức và phân loại dữ liệu hiệu quả.

#### AWS Glue Data Catalog

[**AWS Glue Data Catalog**](https://docs.aws.amazon.com/prescriptive-guidance/latest/serverless-etl-aws-glue/aws-glue-data-catalog.html#:~:text=The%20AWS%20Glue%20Data%20Catalog,formats%2C%20schemas%2C%20and%20sources.) là kho metadata trung tâm, lưu trữ thông tin về vị trí, lược đồ và thông số runtime của dữ liệu. Glue Data Catalog hoạt động như một index giúp truy vấn dễ dàng và có thể đăng ký làm nguồn dữ liệu trong **Lake Formation**.

Glue Data Catalog tự động đồng bộ các **table buckets, namespaces và tables** dưới dạng các đối tượng metadata trong AWS Glue, giúp quản lý dữ liệu đơn giản và hiệu quả.

![glue-data-catalog](/images/1-introduction/image.png)

#### Các dịch vụ AWS Analytics tích hợp với S3 Tables

1. [**Amazon Athena**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-athena.html): Dịch vụ truy vấn SQL tương tác trực tiếp với S3, không cần cài đặt server.
2. [**Amazon Redshift**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-redshift.html): Kho dữ liệu petabyte-scale, hỗ trợ phân tích dữ liệu hiệu quả với Redshift Serverless cho phép truy cập mà không cần cấu hình phức tạp.
3. [**Amazon EMR**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-emr.html): Nền tảng big data giúp chạy các framework như Apache Hadoop và Spark để xử lý dữ liệu lớn.
4. [**Amazon QuickSight**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-quicksight.html): Công cụ phân tích dữ liệu nhanh, cung cấp các biểu đồ trực quan và hỗ trợ mở rộng cho hàng trăm nghìn người dùng với **SPICE Engine**.
5. [**Amazon Data Firehose**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables-integrating-firehose.html): Dịch vụ streaming dữ liệu thời gian thực, tích hợp với S3, Redshift, OpenSearch, và Apache Iceberg Tables.

![aws-analytics-services](/images/1-introduction/image-3.png)