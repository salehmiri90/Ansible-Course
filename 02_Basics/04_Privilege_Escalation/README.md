---

# 🔑 Ansible Connection Methods and Privilege Escalation

## 📌 How Ansible Connects to Hosts

There are two primary connection methods in Ansible:

### 1️⃣ User/Password

* Connects using username and password
* Simple but less secure

**Pros:** Easy, no key needed
**Cons:** Low security, impractical for large environments

### 2️⃣ SSH Key (Public/Private Key)

**Steps:**

1. Generate a key on the control node
2. Add the public key to the target server
3. Connect without a password

**Advantages:**

* High security
* Suitable for production and large environments
* Run playbooks on hundreds of hosts without entering passwords

Always use SSH keys in production. Use `ansible_ssh_private_key_file` in inventory for private keys. User/password is only for testing.

---

## 🛡 Privileged Tasks and `become`

Many tasks require root or sudo access, e.g., package installation, service management, modifying system files.

**Scenario:** Installing Nginx on Linux

* Without sudo: permission denied
* With `become: yes`: task succeeds

### 🔹 Important Security Notes

* The user must be in `wheel` group or allowed in `/etc/sudoers`
* Example sudoers entry for user `admin`:

```text
admin ALL=(ALL) NOPASSWD: ALL
```

### 🔹 Become Method

Ansible supports multiple methods to escalate privileges depending on OS and policies:

* `sudo` (default on Linux)
* `pfexec` (Oracle Solaris)
* `doas` (BSD systems)
* `ksu` (Kerberos environments)
* `runas` (Windows)

**Inventory example:**

```ini
server1 ansible_host=172.20.1.100 ansible_user=admin
```

* User `admin` can `become` `saleh` (a sudoer user)

**Playbook snippet:**

```yaml
become: yes
become_user: saleh
become_method: sudo
```

### 🔹 Why `become` matters

* Elevates privileges for tasks
* `become_user` allows switching to a user other than root
* Without correct privileges, `become` will fail

---

## 📌 Best Practices for Privilege Escalation

1. **Move settings to `ansible.cfg`**

   * Avoid repetition in multiple playbooks
   * Centralized configuration

2. **Define in Inventory (`all:vars`)**

   * Global override for all hosts
   * Example:

```ini
[all:vars]
ansible_become=yes
ansible_become_method=sudo
ansible_become_user=saleh
```

3. **Use `group_vars/all.yml` for project-level control**

* Recommended in large/enterprise projects
* Versionable with Git
* Separate configurations per environment (`dev`, `stage`, `prod`)
* Can override per group:

```
group_vars/web/
group_vars/db/
group_vars/prod/
```

**Takeaway:**

* `ansible.cfg` → global-level
* `group_vars/all.yml` → project-level, more flexible
* Keeps playbooks clean, maintainable, and policy-driven
