# k8s-the-hard-way-infra-setup
This repository contains a vagrantfile which boostraps the VMs (without jumphost) via a vagrant file.

# Vagrant Kubernetes Cluster (Debian 12)

This project creates a local Kubernetes test environment using Vagrant and VirtualBox. It provisions **three Debian 12 virtual machines**:

- `server` – Kubernetes control plane node
- `node-0` – Kubernetes worker node
- `node-1` – Kubernetes worker node

Each VM is configured with:
- **Debian 12 (bookworm)**
- **2 GB RAM**
- **20 GB disk space**
- **1 vCPU**
- A private network IP
- Your SSH public key (for passwordless login)

## 🔧 Requirements

Make sure the following software is installed on your system:

- [VirtualBox](https://www.virtualbox.org/) (Version 6 or newer)
- [Vagrant](https://www.vagrantup.com/) (Version 2.2+)
- A valid SSH keypair (`~/.ssh/id_rsa.pub` should exist)

> If you don't have an SSH key yet, you can generate one using:
> ```bash
> ssh-keygen -t ed25519
> ```

## 📦 Installation

1. **Clone this repository or download the Vagrantfile and README**
   ```bash
   git clone <your-repo-url>
   cd <your-repo-directory>
   ```

2. **Start the VMs**
   ```bash
   vagrant up
   ```

   This will download the base Debian 12 box (if not already cached), create three VMs, allocate resources, and inject your SSH key into each.

3. **Access the machines via SSH**
   ```bash
   vagrant ssh server
   vagrant ssh node-0
   vagrant ssh node-1
   ```

4. **Verify network connectivity**
   All nodes are on a private network and can ping each other:
   ```bash
   ping node-0
   ```

## 🧹 Cleanup

To shut down the VMs:
```bash
vagrant halt
```

To destroy the environment completely:
```bash
vagrant destroy -f
```

## 🚀 Next Steps

You can now install go ahead and try [kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way/tree/master)

---

## 📁 VM Overview

| Name    | Role               | IP Address      | RAM  | CPU | Disk  |
|---------|--------------------|-----------------|------|-----|-------|
| server  | Control Plane Node | 192.168.56.10   | 2GB  | 1   | 20GB  |
| node-0  | Worker Node        | 192.168.56.11   | 2GB  | 1   | 20GB  |
| node-1  | Worker Node        | 192.168.56.12   | 2GB  | 1   | 20GB  |

