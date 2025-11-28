# 🖥️ Terraform AWS EC2 Demo (Part 3)

This project demonstrates **provisioning an EC2 instance on AWS using Terraform**, along with networking, security groups, and key pairs.  
It is part of my DevOps learning journey and showcases Infrastructure as Code (IaC) skills.

---

## 🚀 What This Project Demonstrates

- **Terraform Infrastructure as Code (IaC)**
- **AWS EC2 provisioning**
- **VPC, Subnet, and Internet Gateway configuration**
- **Security Groups / SSH access**
- **IAM Roles and Instance Profiles**
- **Terraform Outputs for automation**
- **Version-controlled deployment via GitHub**

---

## 📁 Project Structure
```
.
├── main.tf # Provider and core configuration
├── ec2.tf # EC2 instance + Security Group
├── vpc.tf # VPC, Subnet, Internet Gateway, Route Table
├── iam.tf # IAM Role and Instance Profile
├── variables.tf # Input variables
├── outputs.tf # Terraform outputs
├── ssh/ # SSH keys (private NOT committed)
│ ├── my-key
│ └── my-key.pub
└── screenshots/ # AWS Console screenshots
```
---

## ⚡ Architecture Overview

**Region:** `us-east-1` (N. Virginia)  
**VPC CIDR:** `10.0.0.0/16`  
**Subnet CIDR:** `10.0.1.0/24`  
**Security Group:** SSH allowed from all IPs  
**EC2 Instance Type:** `t2.micro`  
**Key Pair:** `my-terraform-key`  

## Architecture Diagram
```
               ┌───────────┐
               │  Internet │
               └─────┬─────┘
                     │
                     ▼
           ┌───────────────────┐
           │ Security Group    │
           │ Inbound: SSH 22   │
           └────────┬──────────┘
                    │
                    ▼
           ┌───────────────────┐
           │ Internet Gateway  │
           └────────┬──────────┘
                    │
                    ▼
       ┌───────────────────────────┐
       │          VPC              │
       │ CIDR: 10.0.0.0/16         │
       └───────────┬───────────────┘
                   │
                   ▼
       ┌───────────────────────────┐
       │        Subnet             │
       │ CIDR: 10.0.1.0/24         │
       └───────────┬───────────────┘
                   │
                   ▼
       ┌───────────────────────────┐
       │        EC2 Instance       │
       │ Security Group: SSH 22    │
       │ Key Pair: my-terraform-key│
       └───────────────────────────┘
```

---

## 📸 Screenshots from AWS Console

### EC2 Instance
<img width="1099" height="298" alt="Snímek obrazovky 2025-11-28 154526" src="https://github.com/user-attachments/assets/081efd47-d630-45cc-9ef9-17229ef45613" />


<img width="1280" height="300" alt="Snímek obrazovky 2025-11-28 154816" src="https://github.com/user-attachments/assets/3b39923e-5704-4f99-b0fa-e23f4a0169e4" />

### Security Group
<img width="1289" height="706" alt="Snímek obrazovky 2025-11-28 154939" src="https://github.com/user-attachments/assets/59bff68f-cb19-49c8-9c1e-1991d8886169" />


### VPC and Subnet
<img width="1297" height="515" alt="Snímek obrazovky 2025-11-28 154856" src="https://github.com/user-attachments/assets/268f29bd-24aa-4aa0-8cdb-0ce0037f94f9" />

<img width="1285" height="376" alt="image" src="https://github.com/user-attachments/assets/0916950d-cb28-4549-8a6b-b308091c3fc2" />


### Terraform Output
<img width="551" height="71" alt="Snímek obrazovky 2025-11-28 155020" src="https://github.com/user-attachments/assets/a18e4078-19f8-44e8-b772-0d527e43525e" /> 

---

## ▶️ Deployment Steps

**Clone the repository**

```bash
git clone https://github.com/<your-username>/terraform-aws-ec2-demo-part3.git
cd terraform-aws-ec2-demo-part3
```

**Generate SSH key (if not already)**
```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/my-key
```

Update variables.tf if needed (region, key path, instance type)
**Initialize Terraform**
```
terraform init
```

**Validate configuration**
```
terraform validate
```

**Plan the deployment**
```
terraform plan
```

**Apply the deployment**
```
terraform apply
```

Type yes to confirm.

**Connect to EC2 via SSH**
```
ssh -i ~/.ssh/my-key ec2-user@<PUBLIC_IP>
```
**Cleanup**
```
terraform destroy -auto-approve
```

Always destroy resources to avoid unnecessary AWS charges.


## 💡 Notes <br>
Private key (my-key) must never be committed to GitHub <br>
This project is fully reproducible using Terraform <br>
Designed for learning and portfolio purposes <br>
