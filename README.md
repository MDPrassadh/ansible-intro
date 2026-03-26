              vhttps://copilot.microsoft.com/th/id/BCO.f98ea40a-4e7b-4c4b-9a6c-b2a771c25608.png



<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/eed27cf7-3846-47d1-90ab-66a5eeb7adf5" />

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/ed906226-e9eb-4961-8174-0a1c7f75ac06" />

# prassadh-vpc: Secure 3-Tier AWS Architecture with Ansible

This repository contains a complete automation setup for deploying a secure, high-availability 3-tier architecture on AWS using Ansible.

## 📐 Architecture Overview

- **VPC Name**: `prassadh` (`10.0.0.0/16`)
- **Availability Zones**: `ap-south-1a` and `ap-south-1b`
- **Subnets**:
  - Public Subnets: `10.0.1.0/24`, `10.0.2.0/24`
  - Private Subnets: `10.0.11.0/24`, `10.0.12.0/24`
  - Database Subnets: `10.0.21.0/24`, `10.0.22.0/24`
- **Routing**:
  - Public → Internet Gateway
  - Private → NAT Gateway
  - Database → Local routes only
- **Security Groups**:
  - Bastion: SSH from admin IP only
  - Frontend: HTTP/HTTPS from all
  - Backend: App port from frontend, SSH from bastion
  - Database: MySQL from backend, SSH from bastion
- **DNS**: Hosted zone `prassadhmulticloud.online` with records for each tier

## 📦 Files

| File | Purpose |
|------|---------|
| `prassadh_vpc_sgs_routing.yml` | Creates VPC, subnets, routing, and SGs |
| `prassadh_instances_dns.yml` | Launches EC2 instances and DNS records |
| `prassadh_teardown_vpc_sgs.yml` | Deletes VPC, subnets, SGs |
| `prassadh_teardown_instances_dns.yml` | Terminates EC2 and deletes DNS records |

## 🖼️ Architecture Diagram

![Architecture](https://copilot.microsoft.com/th/id/BCO.f98ea40a-4e7b-4c4b-9a6c-b2a771c25608.png)

## 🚀 How to Use

1. Run `prassadh_vpc_sgs_routing.yml` to create infrastructure.
2. Run `prassadh_instances_dns.yml` to launch instances and configure DNS.
3. To clean up, run `prassadh_teardown_instances_dns.yml` followed by `prassadh_teardown_vpc_sgs.yml`.

## 🧠 Interview Ready

This setup is designed to reflect real-world production standards and is ideal for showcasing DevOps skills in interviews or portfolio reviews.

---

Made with ❤️ by Durga Prassadh



secure 3‑tier AWS architectur: ap-south-1   region for better High availablity and fault tolerance i'm using AZ 1a and 1b in ap-south -1 

VPC (gcp-vpc, ap-south-1) → CIDR 10.0.0.0/16.

Public Subnets (1a & 1b) → Bastion + Frontend.

Private Subnet (1a) → Backend.

Database Subnet (1a) → MySQL.

Security Groups → bastion, frontend, backend, database strict with rules.

Route53 Hosted Zone → prassadhmulticloud.online DNS records (root, frontend, backend, mysql, bastion).

Traffic Flow →

Users → Frontend (HTTP/HTTPS).

Frontend → Backend (8080).

Backend → MySQL (3306).

Bastion → Backend/MySQL (SSH/admin).

📝 Practice Notes (Teluguలో)
Application traffic → Frontend → Backend → MySQL.

* Admin traffic → Bastion → Backend/MySQL.

* DNS records → Hosted zoneలో configure చేయాలి.

* High Availability → Subnets 1a & 1bలో redundancy.

* Strict SG rules → Internet నుండి backend/mysqlకి direct access ఉండకూడదు.

* 🔍 Scenario-Based Interview Questions & Answers
Q1: Why is the Bastion host placed in a public subnet?
A: The Bastion host needs to be accessible from the internet via SSH (port 22). Placing it in a public subnet allows administrators to securely connect and then access private instances like backend and database without exposing them directly.

Q2: Why is the Backend server placed in a private subnet?
A: The Backend server handles internal application logic and should not be exposed to the internet. It receives traffic only from the Frontend server and is accessed via SSH from the Bastion host for administration.

Q3: Why is the MySQL database placed in a private subnet?
A: Databases contain sensitive data and must be protected from public access. The MySQL instance is placed in a private subnet and only accepts connections from the Backend server (for application queries) and Bastion host (for admin access).

Q4: Can the Bastion host directly access Backend and MySQL instances?
A: Yes, the Bastion host can SSH into both Backend and MySQL instances. This is strictly for administrative purposes. Application traffic flows through Frontend → Backend → MySQL.

Q5: Why are Security Group references preferred over CIDR blocks?
A: Security Group references are dynamic and more secure. They allow access based on instance roles rather than fixed IP ranges, reducing the risk of misconfiguration and improving modularity.

Q6: Why is the Frontend server placed in a public subnet?
A: The Frontend server handles user-facing web traffic (HTTP/HTTPS). It must be publicly accessible, so it’s placed in a public subnet with security group rules allowing traffic from all IPs on ports 80 and 443.

Q7: Why do we use Route53 DNS records for EC2 instances?
A: Route53 allows us to assign human-readable domain names to EC2 instances. This simplifies access, monitoring, and automation. For example, users can reach the frontend via frontend.example.com instead of an IP address.

Q8: Why do we split subnets across multiple Availability Zones?
A: Splitting subnets across AZs improves high availability and fault tolerance. If one AZ goes down, resources in the other AZ can continue to operate, minimizing downtime.

Q9: Why does the Bastion host need outbound internet access?
A: The Bastion host may need to install packages, fetch updates, or run scripts that require internet access. However, inbound access must be tightly restricted to specific IPs.

Q10: What is the difference between application traffic and admin traffic?
A: Application traffic flows from users to the Frontend, then to Backend, and finally to the Database. Admin traffic is for management and flows from the Bastion host to Backend and MySQL via SSH.


