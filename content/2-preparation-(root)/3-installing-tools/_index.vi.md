---
title: "Cài đặt bộ công cụ"
date: "`r Sys.Date()`"
weight: 3
pre : "<b>2.3 </b>"
chapter: false
---

### 2.3. Cài đặt Bộ Công Cụ

Trong phần này, chúng ta sẽ cài đặt AWS CLI v2 phiên bản mới nhất và công cụ `jq` để xử lý dữ liệu JSON trả về.

#### Cập nhật AWS CLI v2 Mới Nhất

Trước tiên, kiểm tra phiên bản AWS CLI hiện tại trên EC2 Instance:

```
aws --version
```

Phiên bản hiện tại là AWS CLI v2.17.18, chưa hỗ trợ S3 Tables. Để cập nhật lên phiên bản mới nhất, bạn có thể sử dụng các lệnh sau:

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

<!-- Hình ảnh 1: Lệnh tải và cài đặt AWS CLI v2 -->

Câu lệnh trên sẽ tải về tệp zip, giải nén, và cài đặt AWS CLI v2 vào thư mục `/usr/local/bin`.

Sau khi cài đặt xong, bạn cần tải lại `PATH`:

```
source ~/.bashrc
```

<!-- Hình ảnh 2: Tải lại file cấu hình bash -->

Kiểm tra lại phiên bản của AWS CLI để xác nhận đã cài đặt thành công:

```
aws --version
```

<!-- Hình ảnh 3: Kiểm tra phiên bản AWS CLI -->

#### Cài đặt jq

`jq` là công cụ hữu ích để xử lý dữ liệu JSON. Mặc định, công cụ này đã có sẵn trên AWS Linux. Tuy nhiên, nếu không có, bạn có thể cài đặt nó bằng lệnh sau:

```
sudo apt-get install jq
```

<!-- Hình ảnh 4: Cài đặt jq -->

Kiểm tra lại phiên bản `jq`:

```
jq --version
```

<!-- Hình ảnh 5: Kiểm tra phiên bản jq -->
