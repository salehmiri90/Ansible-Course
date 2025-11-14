📘 README — Ansible Playbook Basics
Overview

An Ansible Playbook is the core component for automating tasks on your Managed Nodes.
It is written in YAML, runs tasks sequentially, and invokes Ansible modules to perform actions.

🔹 Key Features

Written in YAML:
Human-readable, easy to understand, and suitable for non-programmers.

Sequential Task Execution:
Tasks are executed in the order they are defined, ensuring dependencies are respected.

Invoke Ansible Modules:
Modules are units of work that perform operations on the target systems:

Install packages

Manage users

Configure services

Copy files

And more

🔹 Example Playbook

```
- name: Install and start Nginx on webservers
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

Explanation:

YAML syntax

Two tasks executed sequentially

Uses apt module to install Nginx

Uses service module to start Nginx

✅ Benefits

Automate repetitive tasks easily

Ensure consistent configuration across servers

Simple structure makes it easy to maintain

Playbooks can scale from a few servers to hundreds

💡 Notes

Playbooks are the main way to organize and document automation in Ansible.

Every task should invoke a module or an ad-hoc command.

Playbooks can be version-controlled in Git for collaboration.