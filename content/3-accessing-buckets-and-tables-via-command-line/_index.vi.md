---
title: "Truy cập S3 Buckets và Tables sử dụng Command Line"
date: "`r Sys.Date()`"
weight: 3
pre: "<b>3. </b>"
chapter: false
---

### 3. Truy cập S3 Buckets và Tables qua Command Line Interface

#### Tạo và Quản lý Table Bucket

Sau khi thiết lập các công cụ cần thiết, bạn có thể tạo và quản lý S3 Table Buckets sử dụng [AWS CLI](https://aws.amazon.com/cli/). Dưới đây là hướng dẫn chi tiết:

1. **Tạo S3 Table Bucket**  
   Trong phiên SSH trên EC2 Instance, chạy lệnh sau để tạo Table Bucket:

   ```bash
   aws s3tables create-table-bucket --name jbarr-table-bucket-2 | jq .arn
   "arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2"
   ```

2. **Thiết lập Biến Môi Trường**  
   Lưu ARN của Bucket vào một biến môi trường để dễ thao tác:

   ```bash
   export ARN="arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2"
   ```

3. **Liệt Kê Các Table Buckets**  
   Xem danh sách các Table Buckets đã tạo:

   ```bash
   aws s3tables list-table-buckets | jq .tableBuckets[].arn
   "arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2"
   ```

---

#### Cài đặt và Sử dụng Apache Spark để Quản lý Tables

Bạn có thể thao tác với các Tables trong Bucket thông qua [Apache Spark](https://spark.apache.org/).

1. **Cài đặt Java 17**  

   {{% notice note %}}
   [Spark runs on Java 8/11/17](https://spark.apache.org/docs/latest/#:~:text=Spark%20runs%20on%20Java%208/11/17)
   {{% /notice %}}

   Apache Spark yêu cầu Java 8/11/17 để chạy. Cài đặt **Java 17** bằng lệnh sau:

   ```bash
   sudo dnf install java-17-amazon-corretto
   ```

   ![install-java-17](/images/3-accessing-buckets-and-tables-via-command-line/image-2.png)

2. **Tải và Cài đặt Apache Spark**  
   Tải phiên bản mới nhất của Apache Spark:

   ```bash
   wget https://dlcdn.apache.org/spark/spark-3.5.4/spark-3.5.4-bin-hadoop3.tgz
   tar -xvf spark-3.5.4-bin-hadoop3.tgz
   ```

![install-spark](/images/3-accessing-buckets-and-tables-via-command-line/image-3.png)

Thêm đường dẫn Spark binary vào `PATH`:

```bash
vi ~/.bashrc
```

Thêm dòng sau vào cuối file:

```bash
export PATH=$PATH:/home/ec2-user/spark-3.5.4-bin-hadoop3/bin/
```

![export-spark](/images/3-accessing-buckets-and-tables-via-command-line/image-4.png)

Lưu và thoát (`ESC` > `:wq`), sau đó kiểm tra phiên bản Spark:

```bash
spark-shell --version
```

![spark-version](/images/3-accessing-buckets-and-tables-via-command-line/image-5.png)

3. **Sử dụng Spark-Shell để Quản lý Tables**  
    Khởi chạy Spark-Shell với Apache Iceberg và cấu hình cần thiết. Thay ARN bằng giá trị ARN của Bucket của bạn:

   Thay thế `<aws:s3tables:us-east-1:0123456789012:bucket/jbarr-table-bucket-2>` bằng ARN của Table Bucket bạn đã tạo

   ```bash
   spark-shell \
   --packages org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.6.1,software.amazon.s3tables:s3-tables-catalog-for-iceberg-runtime:0.1.3,software.amazon.awssdk:s3:2.20.42,software.amazon.awssdk:sts:2.20.42,software.amazon.awssdk:kms:2.20.42,software.amazon.awssdk:glue:2.20.42,software.amazon.awssdk:dynamodb:2.20.42  \
   --conf spark.sql.catalog.s3tablesbucket=org.apache.iceberg.spark.SparkCatalog \
   --conf spark.sql.catalog.s3tablesbucket.catalog-impl=software.amazon.s3tables.iceberg.S3TablesCatalog \
   --conf spark.sql.catalog.s3tablesbucket.warehouse=<arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2> \
   --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions
   ```

   ![accessing-spark-shell](/images/3-accessing-buckets-and-tables-via-command-line/image-6.png)

4. **Tạo Namespace và Table**  
   Tạo namespace và table trong Bucket:

   ```scala
   spark.sql("""CREATE NAMESPACE IF NOT EXISTS s3tablesbucket.mydata""")
   spark.sql("""CREATE TABLE IF NOT EXISTS s3tablesbucket.mydata.table1
   (id INT, name STRING, value INT) USING iceberg""")
   ```

   ![creating-namespace-and-table](/images/3-accessing-buckets-and-tables-via-command-line/image-7.png)

5. **Chèn và Truy Vấn Dữ Liệu**  
   Chèn dữ liệu mẫu và truy vấn để kiểm tra:

   ```scala
   spark.sql("""INSERT INTO s3tablesbucket.mydata.table1
     VALUES
     (1, 'Jeff', 100),
     (2, 'Carmen', 200),
     (3, 'Stephen', 300)
   """)
   spark.sql("SELECT * FROM s3tablesbucket.mydata.table1").show()
   ```

   ![insert-data](/images/3-accessing-buckets-and-tables-via-command-line/image-8.png)

---

Bằng cách sử dụng **AWS CLI và Apache Spark**, bạn đã tạo và thao tác thành công với S3 Table Buckets. Công cụ này mang lại hiệu quả cao trong việc quản lý và phân tích dữ liệu lớn.
