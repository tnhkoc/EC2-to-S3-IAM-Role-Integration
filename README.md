# AWS EC2 to S3 Integration (IAM Role-Based)

This project demonstrates how to securely access Amazon S3 from an EC2 instance using IAM roles, without needing to configure access keys.

---

## ✅ Objective

- Launch an EC2 instance
- Attach an IAM Role with S3 permissions
- Verify that the instance can access S3 using AWS CLI

---

## 🔧 Steps

### 1. Launch EC2 Instance
- Amazon Linux 2 (Free Tier eligible)
- Enable **Auto-assign public IP**
- Allow inbound traffic for:
  - SSH (Port 22)
  - HTTP (Port 80)

### 2. Create and Attach IAM Role
- IAM Role Name: `EC2-S3AccessRole`
- Permissions: `AmazonS3ReadOnlyAccess`
- Attach this role to your EC2 instance via **Actions > Security > Modify IAM Role**

### 3. Connect to EC2 via SSH
```bash
ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
```

### 4. Install AWS CLI (if needed)
```bash
sudo yum update -y
sudo yum install -y aws-cli
```

### 5. Test S3 Access
```bash
aws s3 ls
```
✅ If you see your S3 buckets listed, the IAM role works as expected.

---

## 🔍 Optional: Web Server Setup

```bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Hello from EC2 - $(hostname)</h1>" | sudo tee /var/www/html/index.html
```

You can access it via:
```
http://<your-ec2-public-ip>
```

---

## 🔐 Notes

- No access keys were used at any point.
- EC2 gets temporary credentials via the instance metadata service.
- To inspect IAM info:
```bash
curl http://169.254.169.254/latest/meta-data/iam/info
```

---

## 📷 Screenshot

1. EC2 instance details  
![EC2 Instance](screenshots/01-ec2-instance-details.png)

2. SSH connection success  
![SSH](screenshots/02-ssh-connection-success.png)

3. Apache installation  
![Apache Install](screenshots/03-apache-installation.png)

4. Apache started and index file created  
![Apache Enable](screenshots/04-start-enable-apache.png)

5. Web browser result  
![Browser](screenshots/05-browser-output.png)

6. IAM role setup  
![IAM Role](screenshots/06-iam-role-details.png)

7. IAM role attached to EC2  
![Role Attached](screenshots/07-ec2-iam-role-attached.png)

8. S3 bucket listed from EC2  
![S3 List](screenshots/08-s3-listing.png)

---

## 💡 Useful Links

- [IAM Roles for EC2](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html)
- [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/)

---

## 🏁 Done By

**Tunahan Koç**  
AWS Certified Cloud Practitioner 🌩️
