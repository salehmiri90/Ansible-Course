# 📘 Install Ansible on Control Node

This guide explains how to install Ansible on your **control node** across different Linux distributions, macOS, and alternative installation options.

---

## 1️⃣ Install Using Package Manager

### Red Hat / CentOS / Fedora

```bash
# RHEL 7 / CentOS 7
sudo yum install ansible

# RHEL 8 / Fedora
sudo dnf install ansible
```

### Debian / Ubuntu

```bash
sudo apt-get update
sudo apt-get install ansible
```

### macOS

```bash
# Using Homebrew
brew install ansible
```

---

## 2️⃣ Install Using pip (Python Package Manager)

```bash
sudo pip install ansible
```

**Flexible installation method:**

* Can be used on any Linux distribution
* Supports virtual environments

> **Tip:** Use `pip install --user ansible` if you don’t have sudo access.

---

## 3️⃣ Advanced Options

### Install from Source via Git

```bash
git clone https://github.com/ansible/ansible.git
cd ansible
source ./hacking/env-setup
```

### Build RPM Yourself

* Useful for environments requiring custom packaging
* Provides full control over installation paths and versions

---

## ✅ Notes

**Control Node Requirements:**

* Python 3.8+
* SSH access to managed nodes
* Root or sudo privileges are required for system-wide installation

> For Windows control node, use **WSL (Windows Subsystem for Linux)** or a Linux VM.

---

## 🔹 Summary

* The fastest method is using your Linux distribution’s package manager
* `pip` allows installation of the latest version and flexible deployment
* Source installation or building RPMs is recommended for customized or enterprise environments

---

## 📘 Install Ansible on Control Node via pip

This guide explains how to install Ansible using **pip**, including installing pip itself, installing a specific version, and upgrading Ansible.

### 1️⃣ Install pip (if not installed)

#### RHEL / CentOS

```bash
sudo yum install epel-release
sudo yum install python-pip
```

* `epel-release` provides access to additional packages
* `python-pip` installs pip for Python 2 or 3 depending on your system

### 2️⃣ Install Ansible

```bash
sudo pip install ansible
```

* Installs the latest stable version of Ansible
* Works with virtual environments (virtualenv)
* Flexible method for testing or development

### 3️⃣ Install a Specific Version of Ansible

```bash
sudo pip install ansible==2.4
```

* Useful for project compatibility
* Ensures playbooks work with a known version

### 4️⃣ Upgrade Ansible

```bash
sudo pip install --upgrade ansible
```

* Replaces any existing Ansible version with the latest release
* Ensures newest features and bug fixes

---

## ✅ Notes

* Installing via pip is flexible and convenient for development/testing
* For production environments, package manager installation is usually recommended
* You can use virtual environments to manage multiple Ansible versions

---

## 🔹 Summary

* Install pip if missing
* Install Ansible via pip
* Optionally install a specific version
* Upgrade Ansible as needed
