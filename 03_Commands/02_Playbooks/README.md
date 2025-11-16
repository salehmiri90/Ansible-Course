# Ansible Playbook Basics

An **Ansible Playbook** is a YAML file that defines a series of tasks to execute on one or more servers. Playbooks are the first step into real automation with Ansible.

---

## 🔹 Playbook
A YAML file containing one or more **Plays**.  
Each Play defines **what tasks to run on which hosts**.

## 🔹 Play
Each Play includes:
- Optional but recommended name for the Play
- `hosts`: the servers where tasks will run
- `become`: whether sudo privileges are required
- `tasks`: the list of actions to execute

## 🔹 Task
A Task is a single action such as:
- Running a command
- Installing a package
- Running a script
- Copying a file
- Rebooting or shutting down a server
- Starting or stopping services

## 🔹 Playbook Structure
YAML structure is **critical** in Ansible Playbooks:
- Each Playbook starts with `---`
- Each Play starts with `-`
- Key sections in a Playbook:
  - `name`
  - `hosts`
  - `become`
  - `tasks`
- Each Task includes:
  - `name`
  - Module name (e.g., `yum`, `template`, `service`)
  - Module parameters

## 🔹 Example Summary
In this example:
- Web servers belong to the `web` group
- `become: yes` indicates using sudo
- Three Tasks are executed:
  1. Install the latest Apache (`httpd`) package
  2. Copy the `index.html` file to the server
  3. Start the `httpd` service

### How it works:
- The Play defines **hosts**, **become**, and **tasks**.
- Each Task is a single operation with its module and parameters.
- Modules are the tools used to perform actions.

### Modules Used in This Playbook

1. **yum module** – installs packages
```yaml
yum:
  name: httpd
  state: latest
```
2. **template module** – copies files using Jinja2 templates
```yaml
template:
  src: files/index.html
  dest: /var/www/html/
```
3. **service module** – manages services
```yaml
service:
  name: httpd
  state: started
```

## 🔹 Full Playbook Example

```yaml
---
- name: install and start apache
  hosts: web
  become: yes

  tasks:

    - name: httpd package is present
      yum:
        name: httpd
        state: latest

    - name: latest index.html file is present
      template:
        src: files/index.html
        dest: /var/www/html/

    - name: httpd is started
      service:
        name: httpd
        state: started
```
