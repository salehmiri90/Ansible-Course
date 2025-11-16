# Ansible CLI Essentials

This guide introduces the essential Ansible command-line tools you should know before getting started. These tools help you **test**, **execute**, and **debug** tasks quickly and effectively.

## --help
Use `--help` with any Ansible command to display a summary of available options and full usage details.

## General Usage
The basic format of an Ansible ad-hoc command is:

```
ansible <host-pattern> [options]
```

With the `ansible` command, you execute **a single task** (a module plus its arguments) on one or more hosts, **without using a playbook**.

## Useful Options

### -a or --args
Used to provide arguments required by a module.

### Switching to a Sudo-Enabled User
If the SSH login user is not a sudoer, but another user (e.g., `opsuser`) has sudo access, you can switch to that user:

```
ansible all -m command -a "whoami" -b --become-user=opsuser
```

## What Is an Ad-Hoc Command?
An ad-hoc command is a one-time Ansible command executed **without a playbook**.

## The Ping Module
Ansible’s ping is not ICMP ping. It checks:
- SSH connectivity
- Python availability
- Ability to run a simple module

```
ansible all -m ping
```

### Example Output
```
web1 | SUCCESS => {
    "ping": "pong",
    "changed": false,
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }
}
```

## Common Options

### -m MODULE_NAME
```
ansible all -m shell
```

### -a MODULE_ARGS
```
ansible all -m shell -a "uptime"
```

### -b or --become
```
ansible all -m yum -a "name=nginx state=latest" -b
```

### -e EXTRA_VARS
```
ansible all -m debug -e "msg=HelloWorld"
```

## Common Ad-Hoc Examples

### 1. Ping All Hosts
```
ansible all -m ping
```

### 2. Run uptime on web group
```
ansible web -m command -a "uptime"
```

### 3. Gather Facts
```
ansible web1 -m setup
```