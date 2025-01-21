---
title: "Installing Toolkits"
date: "`r Sys.Date()`"
weight: 3
pre: "<b>2.3 </b>"
chapter: false
---

### **2.3 Installing Toolkits**

This section provides instructions to install the latest version of **AWS CLI v2** and the **`jq`** tool for processing JSON responses.

---

### **Update AWS CLI v2 to the Latest Version**

1. **Check Current AWS CLI Version:**

   Run the following command on your EC2 instance to check the current version of AWS CLI:

   ```bash
   $ aws --version
   # aws-cli/2.17.18 Python/3.9.20 Linux/6.1.119-129.201.amzn2023.x86_64 source/x86_64.amzn.2023
   ```

   If the current version is **AWS CLI v2.17.18** or older, you need to upgrade it to support **Amazon S3 Tables**.

2. **Update AWS CLI v2:**

   Execute the following commands to download, unzip, and install the latest version of AWS CLI:

   ```bash
   $ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   $ unzip awscliv2.zip
   $ sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
   ```

   ![install-aws-cli](</images/2-preparation-(root)/3-installing-tools/image-1.png>)

   This will install **AWS CLI v2** at `/usr/local/bin`.

3. **Reload Environment Variables:**

   After the installation is complete, reload the environment variables and verify the updated version:

   ```bash
   $ source ~/.bashrc
   $ aws --version
   # aws-cli/2.23.2 Python/3.12.6 Linux/6.1.119-129.201.amzn2023.x86_64 exe/x86_64.amzn.2023
   ```

---

### **Install `jq` Tool**

**`jq`** is a powerful tool for processing and analyzing JSON data.

1. **Check if `jq` is Preinstalled:**

   On **AWS Linux**, `jq` is often preinstalled. To verify, run:

   ```bash
   $ jq --version
   ```

2. **Install `jq` (if not installed):**

   If `jq` is not available, install it using the following command:

   ```bash
   $ sudo apt-get install jq
   ```

3. **Verify Installation:**

   After installation, confirm that `jq` is working correctly by checking its version:

   ```bash
   $ jq --version
   ```
