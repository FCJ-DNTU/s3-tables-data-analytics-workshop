---
title: "Resource Cleanup"
date: "`r Sys.Date()`"
weight: 6
pre: "<b>6. </b>"
chapter: false
---

### 6. Resource Cleanup

Congratulations on completing the workshop! Now, let's proceed with cleaning up resources to avoid unnecessary costs.

The cleanup process will follow this order: Delete Table > Delete Namespace > Delete S3 Table Bucket > Delete EC2 Instance > Delete Security Group > Delete VPC > Delete IAM Role.

Start by SSHing into your EC2 instance.

1. **Delete Table**

   Replace `<arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2>` with your bucket's ARN.

```shell
aws s3tables delete-table \
--table-bucket-arn <arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2> \
--namespace mydata --name table1
```

2. **Delete Namespace**

```shell
aws s3tables delete-namespace \
--table-bucket-arn <arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2> \
--namespace mydata
```

3. **Delete S3 Table Buckets**

```shell
aws s3tables delete-table-bucket \
--table-bucket-arn <arn:aws:s3tables:us-east-1:123456789012:bucket/jbarr-table-bucket-2>
```

![delete-s3-table-buckets](/images/6-clean-up-resources/image.png)

4. **Delete EC2 Instance**

   Go to the EC2 Dashboard, select your EC2 instance, and use the "Terminate" action to delete the instance.

![delete-ec2-instance-1](/images/6-clean-up-resources/image-1.png)

![delete-ec2-instance-2](/images/6-clean-up-resources/image-2.png)

5. **Delete Security Group**

   Go to the VPC Dashboard, select "Security Groups" in the left navigation pane, select the `demo-s3-tables-sg` security group, click on the dropdown actions, and select "Delete Security Group."

![delete-sg](/images/6-clean-up-resources/image-3.png)

6. **Delete VPC**

   Go to the VPC Dashboard, select "Your VPCs," choose the `demo-s3-table-vpc`, click on the dropdown actions, select "Delete VPC," type `delete` to confirm, and proceed with the deletion.

![delete-vpc-1](/images/6-clean-up-resources/image-4.png)

![delete-vpc-2](/images/6-clean-up-resources/image-5.png)

7. **Delete IAM Role**

   Go to the IAM Service Dashboard, select "Roles" in the left navigation pane, search for `ec2-s3-tables-role`, and select "Delete."

![delete-iam-role](/images/6-clean-up-resources/image-6.png)

---

Congratulations again! If you encounter any issues or need assistance troubleshooting, feel free to reach out to me via [LinkedIn](https://linkedin.com/in/minhnghia2k3) or email me at [nghialm2603@gmail.com](mailto:nghialm2603@gmail.com).
