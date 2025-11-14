# Ansible Overview & Fundamentals

## 1️⃣ What is Ansible?

Ansible is an agentless automation engine that allows you to **deploy, configure, secure, and orchestrate** your entire IT environment — servers, network devices, storage, applications, and cloud resources.

**Key Advantages:**
- **Agentless:** No installation required on managed nodes.
- **Human-readable YAML:** Easy to understand and maintain.
- **Idempotent tasks:** Ensures the desired state without extra checks.
- **Parallel execution:** Update multiple hosts simultaneously.

---

## 2️⃣ Core Components of Ansible

| Component        | Description |
|-----------------|-------------|
| **Control Node** | Machine where Ansible is installed and playbooks are executed. |
| **Managed Nodes**| Servers or devices managed by Ansible (Linux, Windows, network devices). |
| **Inventory**    | List of hosts (static or dynamic) that Ansible can automate. |
| **Modules**      | Units of work that perform actions on managed nodes (install, copy, configure, etc.). |
| **Playbooks**    | YAML files defining tasks, their order, and execution logic. |
| **Plugins**      | Extend functionality (filter, callback, lookup, connection, inventory). |
| **Roles**        | Structured organization for large projects. |

**Architecture Diagram:**

```
          +-----------------+
          |  Control Node   |
          | (Ansible Engine)|
          +--------+--------+
                   |
           SSH / WinRM / API
                   |
   +---------------+----------------+
   |               |                |
Managed Node 1  Managed Node 2  Managed Node 3
(Linux)        (Windows)       (Network Device)
```

---

## 3️⃣ Inventory (Targets for Automation)

### Static Inventory Example
```ini
[web]
webserver1.example.com
webserver2.example.com

[db]
dbserver1.example.com

[firewalls]
checkpoint01.internal.com

[loadbalancers]
f5-01.internal.com
```

### Groups & Dynamic Inventory
- Groups help organize hosts logically.
- Dynamic inventory is supported for cloud environments (AWS, GCP, VMware).

---

## 4️⃣ Modules — Tools in the Toolkit

Modules perform tasks like:

- Install packages (`apt`, `yum`)
- Manage users (`user`)
- Configure services (`service`)
- Copy files (`copy`, `template`)
- Interact with cloud providers, containers, and network devices

**Example: Deploying an HTML page**
```yaml
- name: Ensure latest index.html is deployed
  template:
    src: files/index.html
    dest: /var/www/html/
```

---

## 5️⃣ Plugins — Gears in the Engine

Plugins extend Ansible functionality.

**Types:**
- **Filter Plugins:** Transform variables (`{{ some_variable | to_nice_yaml }}`)
- **Lookup Plugins:** Retrieve data from files or external sources.
- **Callback Plugins:** Customize output or notifications.
- **Connection Plugins:** Manage communication to hosts.
- **Inventory Plugins:** Generate dynamic inventories.

---

## 6️⃣ Playbooks — YAML-Based Automation

Playbooks define **sequential tasks** to automate infrastructure.

**Example: Install and start Nginx on Linux servers**
```yaml
- name: Install and start Nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Install Nginx package
      apt:
        name: nginx
        state: present

    - name: Ensure Nginx service is running
      service:
        name: nginx
        state: started
```

**Key Concepts:**
- Tasks run sequentially.
- Declarative and idempotent.
- Easy to scale from a few servers to hundreds.

---

## 7️⃣ YAML Basics for Playbooks

**XML → JSON → YAML Example**

**XML:**
```xml
<user>
  <name>Saleh</name>
  <age>30</age>
</user>
```

**JSON:**
```json
{
  "name": "Saleh",
  "age": 30
}
```

**YAML:**
```yaml
user:
  name: Saleh
  age: 30
```

**List of Dictionaries:**
```yaml
users:
  - name: Saleh
    age: 30
  - name: Sara
    age: 25
```

**⚠ YAML Indentation Rules**
```yaml
# Wrong
users:
 - name: Saleh
   age: 30
 - name: Sara
  age: 25   # incorrect

# Correct
users:
  - name: Saleh
    age: 30
  - name: Sara
    age: 25
```

---

## 8️⃣ Execution Models

### Local Execution (Network Devices)
- Module code runs on Control Node.
- Configurations sent via SSH/API.
- Ideal for routers, switches, and firewalls.

### Remote Execution (Linux/Windows Hosts)
- Module code copied to managed node, executed, then removed.
- Ensures agentless, idempotent automation.

**Diagram:**
```
Control Node
    |
    | Copy → Execute → Remove
    v
Managed Node (Linux/Windows)
```

---

## 9️⃣ Example Use Case: User Creation on Multiple Linux Servers

| Method    | Time Required |
|-----------|---------------|
| Manual    | ~30 minutes   |
| Ansible   | <5 minutes    |

**Playbook:**
```yaml
- name: Create a new user on all servers
  user:
    name: saleh
```

All servers are updated consistently and efficiently.

---

## 🔹 Key Benefits

- Automate repetitive tasks quickly
- Reduce human errors
- Ensure consistent configuration across multiple servers
- Apply automation across Linux, Windows, network, cloud, storage, and containers
- Version-controlled playbooks for collaboration

---

## Architecture Overview for Linux Infrastructure
```
       +------------------+
       |  Control Node    |
       |  (Ansible Engine)|
       +--------+---------+
                |
         SSH / WinRM
                |
   +------------+------------+
   |            |            |
Linux Server  Network SW   Firewall
(Managed Node) (Managed Node) (Managed Node)
   |            |            |
Package mgmt   VLAN config  Rules & ACLs
Service mgmt  Interface mgmt Logging
```

