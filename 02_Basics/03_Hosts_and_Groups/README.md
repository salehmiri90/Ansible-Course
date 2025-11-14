---

# 📘 Ansible Inventory: Groups, Hosts, and Variables

## 📌 Why Grouping Matters

Grouping in Ansible inventory is one of the most important features. It helps manage complexity, reduce repetition, and target automation effectively.

### 1️⃣ Large Organization Structures

In multinational organizations, there are many servers, services, and IT teams. Grouping helps make this complex structure manageable.

### 2️⃣ Different Roles in Infrastructure

IT administrators often work with different categories of systems, such as:

* Web Servers
* Database Servers
* Application Servers

Each category has unique settings, packages, and policies. Without grouping, managing these servers would be repetitive, error-prone, and complex.

### 3️⃣ Reduce Repetition and Simplify Management

By defining variables, packages, roles, or playbooks for a group (e.g., `web`), all hosts in that group inherit the same configuration:

* Reduces repetition
* Minimizes errors
* Simplifies management
* Enables faster playbook execution

### 4️⃣ Targeted Execution

Grouping allows you to run specific playbooks on selected sets of hosts.

---

## 📂 Parent–Child Relationship

Ansible supports **Parent–Child relationships** between groups, allowing hierarchical, organized, and extendable inventory structures.

**Example Structure:**

* Production servers

  * Web servers_US
  * Web servers_EU

---

## ✅ Example 1 – INI Inventory with Parent–Child

```ini
[webservers:children]
webservers_us
webservers_eu
```

* `webservers` is the parent group
* `webservers_us` and `webservers_eu` are child groups
* Playbooks targeting `webservers` affect all child hosts

---

## ✅ Example 2 – YAML Inventory with Parent–Child

```yaml
all:
  children:
    production:
      children:
        web:
          hosts:
            web01:
            web02:
        db:
          hosts:
            db01:
```

* `production` is the parent group
* `web` and `db` are child groups
* All structures are under `all` by default

---

## 🖥 Hosts

**Hosts** are the smallest unit in Ansible inventory:

* Linux servers
* Windows servers
* Network devices (Cisco, Juniper)
* Firewalls
* Cloud instances
* Containers
* Localhost

Each host has an IP, DNS, or SSH endpoint.

---

## 📌 host_vars

`host_vars` are files or directories defining host-specific variables. They allow customization per host without affecting others.

* Automatically loaded by Ansible
* Enables dynamic, host-specific playbook execution

**Example path:** `host_vars/webserver01.yml`

---

## 📌 Groups

Groups are collections of hosts that share similar tasks.

* Groups can contain hosts or other groups (Parent–Child relationship)
* Group variables are stored in `group_vars` directories or files

**Example:**

```yaml
# group_vars/web.yml
http_port: 80
```

* All hosts in the `web` group inherit `http_port: 80`
* Playbooks run without defining variables for each host individually

---

## 📝 Inventory Variable Levels

1. **Host Variables**: Unique per host, e.g., `ansible_host` for IP connection
2. **Groups**: Logical group of hosts, e.g., `web`
3. **Group Variables**: All hosts in a group inherit these settings (ports, file paths, packages)
4. **All Variables**: Applied to all hosts and groups, e.g., SSH username, private key path
