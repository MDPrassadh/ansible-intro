https://copilot.microsoft.com/th/id/BCO.c92ab4d7-28ff-4790-99b0-32664e5fdb6b.png

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/a9cd4853-3ea8-433d-932d-f71d5e22e8ce" />

secure 3‑tier AWS architectur:

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


