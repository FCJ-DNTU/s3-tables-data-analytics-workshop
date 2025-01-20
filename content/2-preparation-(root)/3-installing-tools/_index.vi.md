---
title: "Cài đặt bộ công cụ"
date: "`r Sys.Date()`"
weight: 3
pre: "<b>2.3 </b>"
chapter: false
---

### 2.3. Cài đặt Bộ Công Cụ

Phần này hướng dẫn cách cài đặt **AWS CLI v2** phiên bản mới nhất và công cụ **`jq`**, hỗ trợ xử lý dữ liệu JSON trả về.

#### Cập nhật AWS CLI v2 lên Phiên Bản Mới Nhất

Đầu tiên, kiểm tra phiên bản hiện tại của AWS CLI trên EC2 Instance:

```bash
aws --version
```

![alt text](image.png)

Nếu phiên bản hiện tại là AWS CLI v2.17.18 hoặc cũ hơn, bạn cần nâng cấp để hỗ trợ **Amazon S3 Tables**. Thực hiện các lệnh sau để cập nhật:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

![alt text](image-1.png)

Lệnh trên sẽ tải tệp cài đặt, giải nén, và cài đặt **AWS CLI v2** tại đường dẫn `/usr/local/bin`. Sau khi hoàn tất, tải lại biến môi trường bằng lệnh:

```bash
$ source ~/.bashrc
$ aws --version
```

![alt text](image-2.png)

#### Cài đặt Công Cụ `jq`

**`jq`** là một công cụ mạnh mẽ để xử lý và phân tích dữ liệu JSON. Trên hệ điều hành **AWS Linux**, công cụ này thường được cài đặt sẵn. Trong trường hợp chưa có, bạn có thể cài đặt bằng lệnh:

`$ sudo apt-get install jq`

Sau khi cài đặt, kiểm tra phiên bản `jq` để đảm bảo mọi thứ hoạt động bình thường:

```bash
$ jq --version
```

![alt text](image-3.png)
