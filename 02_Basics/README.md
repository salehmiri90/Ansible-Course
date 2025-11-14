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
