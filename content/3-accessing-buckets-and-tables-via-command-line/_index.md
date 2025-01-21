---
title: "Accessing S3 Buckets and Tables Using Command Line"
date: "`r Sys.Date()`"
weight: 3
pre: "<b>3. </b>"
chapter: false
---

### **3. Accessing S3 Buckets and Tables via CLI**

This guide explains how to create and manage S3 Table Buckets using [AWS CLI](https://aws.amazon.com/cli/) and interact with them through **Apache Spark**.

---

### **Create and Manage Table Buckets**

1. **Create an S3 Table Bucket:**

   In your EC2 SSH session, run the following command to create a Table Bucket:

   ```bash
   $ aws s3tables create-table-bucket --name jbarr-table-bucket-2 | jq .arn
   "arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2"
   ```

2. **Set Environment Variable for Bucket ARN:**

   Save the ARN of the bucket in an environment variable:

   ```bash
   $ export ARN="arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2"
   ```

3. **List Table Buckets:**

   View all created Table Buckets:

   ```bash
   $ aws s3tables list-table-buckets | jq .tableBuckets[].arn
   "arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2"
   ```

---

### **Setup and Use Apache Spark for Table Management**

**Apache Spark** provides advanced tools for interacting with tables in buckets.

1. **Install Java 17:**

   {{% notice note %}}  
   [Spark requires Java 8/11/17](https://spark.apache.org/docs/latest/#:~:text=Spark%20runs%20on%20Java%208/11/17).  
   {{% /notice %}}

   Install **Java 17** using the following command:

   ```bash
   $ sudo dnf install java-17-amazon-corretto
   ```

   ![install-java-17](/images/3-accessing-buckets-and-tables-via-command-line/image-2.png)

2. **Download and Install Apache Spark:**

   Download the latest version of **Apache Spark**:

   ```bash
   $ wget https://dlcdn.apache.org/spark/spark-3.5.4/spark-3.5.4-bin-hadoop3.tgz
   $ tar -xvf spark-3.5.4-bin-hadoop3.tgz
   ```

   Add Spark binaries to the `PATH` environment variable:

   ```bash
   $ vi ~/.bashrc
   ```

   Add this line to the end of the file:

   ```bash
   export PATH=$PATH:/home/ec2-user/spark-3.5.4-bin-hadoop3/bin/
   ```

   Save and exit (`ESC` > `:wq`). Verify Spark installation:

   ```bash
   $ spark-shell --version
   ```

   ![spark-version](/images/3-accessing-buckets-and-tables-via-command-line/image-5.png)

3. **Use Spark-Shell to Manage Tables:**

   Launch **Spark-Shell** with the required configuration. Replace `<arn>` with your Table Bucket ARN:

   ```bash
   $ spark-shell \
   --packages org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.6.1,software.amazon.s3tables:s3-tables-catalog-for-iceberg-runtime:0.1.3,software.amazon.awssdk:s3:2.20.42,software.amazon.awssdk:sts:2.20.42,software.amazon.awssdk:kms:2.20.42,software.amazon.awssdk:glue:2.20.42,software.amazon.awssdk:dynamodb:2.20.42 \
   --conf spark.sql.catalog.s3tablesbucket=org.apache.iceberg.spark.SparkCatalog \
   --conf spark.sql.catalog.s3tablesbucket.catalog-impl=software.amazon.s3tables.iceberg.S3TablesCatalog \
   --conf spark.sql.catalog.s3tablesbucket.warehouse=<arn:aws:s3tables:us-east-2:123456789012:bucket/jbarr-table-bucket-2> \
   --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions
   ```

   ![accessing-spark-shell](/images/3-accessing-buckets-and-tables-via-command-line/image-6.png)

4. **Create Namespace and Table:**

   Use Spark-SQL to create a namespace and a table:

   ```scala
   $ spark.sql("""CREATE NAMESPACE IF NOT EXISTS s3tablesbucket.mydata""")
   $ spark.sql("""CREATE TABLE IF NOT EXISTS s3tablesbucket.mydata.table1
   (id INT, name STRING, value INT) USING iceberg""")
   ```

   ![creating-namespace-and-table](/images/3-accessing-buckets-and-tables-via-command-line/image-7.png)

5. **Insert and Query Data:**

   Insert sample data and query it to verify:

   ```scala
   $ spark.sql("""INSERT INTO s3tablesbucket.mydata.table1
     VALUES
     (1, 'Jeff', 100),
     (2, 'Carmen', 200),
     (3, 'Stephen', 300)
   """)
   spark.sql("SELECT * FROM s3tablesbucket.mydata.table1").show()
   ```

   ![insert-data](/images/3-accessing-buckets-and-tables-via-command-line/image-8.png)
