# 📌 How Ansible Finds `ansible.cfg`

Ansible does not rely on a single configuration file. It searches multiple locations in a specific order to determine the final settings.

**Important:** The first file found takes precedence. Other files are ignored.

## 🔹 Search Order (from highest to lowest priority)

### 1️⃣ Environment Variable: `ANSIBLE_CONFIG`

If this environment variable is set, Ansible uses the specified file directly.

```bash
export ANSIBLE_CONFIG=/myproject/ansible.cfg
```

### 2️⃣ `ansible.cfg` in the Current Directory

This is the most common approach in projects because:

* Project-specific configuration
* Included in Git version control

### 3️⃣ `~/.ansible.cfg` in the User's Home Directory

Holds per-user configuration settings, useful for personal preferences.

### 4️⃣ `/etc/ansible/ansible.cfg`

Default configuration file installed with Ansible. Used if none of the above exist.

### 🔹 View the Active Configuration

```bash
ansible-config view
```

This command shows the configuration file Ansible is currently using and the resolved settings.
