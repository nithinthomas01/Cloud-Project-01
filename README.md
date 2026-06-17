static website deployed on AWS using EC2, S3, Nginx, and Ansible.
Fully configured without any local installations — everything runs in AWS CloudShell.

## Tech Stack

| Tool | Purpose |
|---|---|
| AWS EC2 (t2.micro) | Hosts the Nginx web server |
| AWS S3 | Stores and serves website source files |
| AWS IAM Role | Allows EC2 to read S3 without credentials |
| Nginx | Serves the static website on port 80 |
| Ansible | Automates server setup and file deployment |
| AWS CloudShell | Browser-based terminal — no local installs needed |
|---|---||---|---||---|---||---|---||---|---||---|---||---|---|

## How to Deploy

### Prerequisites
- AWS account (free tier)
- AWS CloudShell access

### Step 1 — Upload site files to S3
```bash
aws s3 mb s3://YOUR-BUCKET-NAME --region ap-south-1
aws s3 sync site/ s3://YOUR-BUCKET-NAME/
```

### Step 2 — Launch EC2 instance (via AWS Console)
- AMI: Amazon Linux 2 (free tier)
- Instance type: t2.micro
- IAM role: attach a role with S3 read access
- Security group: allow port 22 and 80

### Step 3 — Install Ansible in CloudShell
```bash
pip install ansible
```

### Step 4 — Configure inventory
```bash
cp ansible/inventory.ini.example ansible/inventory.ini
# Edit inventory.ini and replace YOUR_EC2_IP with your actual IP
```

### Step 5 — Run the playbook
```bash
ansible-playbook -i ansible/inventory.ini ansible/deploy.yaml
```

### Step 6 — Visit your site
http://YOUR_EC2_PUBLIC_IP


## What I Learned
**- Launching and configuring EC2 instances on AWS
- Using IAM roles to securely grant EC2 access to S3
- Writing Ansible playbooks to automate server configuration
- Configuring Nginx as a web server
- Using AWS CloudShell as a zero-setup DevOps environment
- AWS free tier resource management and cleanup**

