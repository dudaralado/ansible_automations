# FreeIPA Deployment with Ansible

This project automates the deployment of a **FreeIPA server container** using Ansible and Podman.

It provisions:
- A FreeIPA server running in a container
- Predefined users and groups for a simple lab/demo environment

---

## 📦 What This Deploys

After a successful run, your FreeIPA instance will include:

### 👥 Users (8 total)
- Developers users
- QA users

### 👥 Groups (2 total)
- `developers`
- `quality_assurance`

---

## ⚙️ Requirements

Before running this project, ensure the following:

- ✅ **Ansible is installed** on the machine where you will execute the playbook  
- ✅ SSH access to the target host (e.g. EC2 instance)
- ✅ Podman is installed on the target host
- ✅ Valid SSH private key configured in the inventory file

To verify Ansible installation:
```bash
ansible --version
```

## 📁 Project Structure
```
FreeIPA_Deploy/
├── inventory
├── bastion.yaml
└── roles/ (if applicable)
```

## 🚀 How to Use
### 1. Update Inventory

Edit the `inventory` file and change the hostname under `[bastion_amazon]` to match your target server:
```[bastion_amazon]
your-ec2-hostname.compute.amazonaws.com
```
Also ensure:

- ansible_user
- ansible_ssh_private_key_file

are correctly set for your environment.

---

### 2. Run the Playbook

Execute the following command:
```
ansible-playbook -i inventory bastion.yaml
```

---

### 🐳 What Happens During Deployment
- Pulls the FreeIPA container image
- Starts the container using Podman
- Configures required ports and volumes
- Sets the container hostname based on inventory configuration
- Creates predefined users and groups

---

### 🧠 Notes
- The hostname defined in the inventory is reused inside the container configuration.
- Ensure DNS resolution works correctly for the hostname you provide.
- This setup is ideal for lab, testing, and learning purposes.
