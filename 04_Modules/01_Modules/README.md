# Ansible Modules Overview

Modules in Ansible are like tools in a toolbox. They allow us to perform different actions on servers and systems. Each task in a playbook usually uses a module.

---

## Common Categories of Ansible Modules

### 1️⃣ System Modules
Manage operating system features and services:
- **selinux** → Configure SELinux  
- **service** → Manage services (start/stop/restart)  
- **ufw** → Manage Ubuntu firewall  
- **time** → Configure system time  

### 2️⃣ Commands & Shell
Execute commands and scripts:
- **command** → Run simple commands  
- **shell** → Run commands via shell  
- **script** → Run a script file  

### 3️⃣ Files
Manage files and directories:
- **copy** → Copy files to the remote server  
- **archive** → Create and extract archives  
- **find** → Find files on the system  

### 4️⃣ Databases
Manage databases:
- **mysql** → MySQL management  
- **postgresql** → PostgreSQL management  
- **mongodb** → MongoDB management  

### 5️⃣ Cloud & Containers
Manage cloud services and containers:
- **aws** → Amazon services  
- **azure** → Microsoft Azure services  
- **gcp** → Google Cloud services  
- **docker** → Manage containers  

### 6️⃣ Windows
Manage Windows systems:
- **copy** → Copy files on Windows  
- **file** → Manage files and folders  
- **hosts** → Manage Windows hosts file  
- **services** → Manage Windows services  

> Full list of modules: [Ansible official modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)

---

## Module Examples

### File Module

```yaml
---
- hosts: all
  tasks:
    - name: Create Directory
      file:
        path: /opt/app
        state: directory
    - name: Create File
      file:
        path: /opt/app/index.html
        state: touch
        owner: app-owner
        group: app-owner
        mode: '0644'
```

### Archive Module

```yaml
---
- hosts: all
  tasks:
    - name: Compress a folder
      archive:
        path: /opt/app/
        dest: /tmp/app.gz
    - name: Uncompress a folder
      unarchive:
        src: /tmp/app.gz
        dest: /opt/app/
        remote_src: yes
```

### User/Group Module

```yaml
---
- hosts: all
  tasks:
    - name: Create a user Saleh
      user:
        name: saleh
        uid: 1001
        group: wecamp
        shell: /bin/bash
    - name: Create a group
      group:
        name: wecamp

```

### How Modules Work

Each module performs a specific action

Tasks can be executed in sequence

Modules are idempotent, meaning if a task has already been performed, it will not make unnecessary changes

### Cron Module

The cron module is used to create scheduled tasks on Linux systems. It allows scripts and commands to be run automatically at specified times.

### Specific Time

```yaml
---
- hosts: all
  tasks:
    - name: Create a scheduled task
      cron:
        name: Run daily health report
        job: sh /opt/scripts/health.sh
        month: 2
        day: 19
        hour: 8
        minute: 10

```

### Repeating Every 2 Minutes

```yaml
---
- hosts: all
  tasks:
    - name: Create a scheduled task
      cron:
        name: Run health check every 2 minutes
        job: sh /opt/scripts/health.sh
        month: "*"
        day: "*"
        hour: "*"
        minute: "*/2"
        weekday: "*"
```

* → all values (every hour, day, month)

*/2 → execute every 2 minutes

Combine minute, hour, day, month, weekday for cron schedule patterns

## Summary

Modules allow tasks to perform operations on systems automatically

Tasks are usually idempotent and predictable

Use modules for packages, services, files, users, cron jobs, storage, and more

Always check module documentation for proper parameters and best practices
