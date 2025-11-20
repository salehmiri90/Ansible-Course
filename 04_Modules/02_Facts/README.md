# Ansible Facts

## What are Facts?

Facts in Ansible are similar to variables, but the key difference is that they are **gathered from the host itself**.  
They include information about the operating system, network, memory, CPU, and other system details.

---

## Viewing Facts with the `setup` Module

You can retrieve facts from a host using the `setup` module:

```bash
ansible server1 -m setup
```
### Example Output

```json
"ansible_facts": {
    "ansible_default_ipv4": {
        "address": "10.41.17.37",
        "macaddress": "00:69:08:3b:a9:16",
        "interface": "eth0"
    },
    ...
}
```

✅ Explanation:

ansible_default_ipv4 → Default IP information of the host

Contains address, macaddress, interface, and other hardware/software details

## Enabling or Disabling Fact Gathering in Playbooks

### `gather_facts` Enabled

```yaml
- name: Example with gather_facts enabled
  hosts: all
  gather_facts: yes
  tasks:
    - debug:
        var: ansible_facts['ansible_default_ipv4']['address']

```

### `gather_facts` Disabled

```yaml
- name: Example with gather_facts disabled
  hosts: all
  gather_facts: no
  tasks:
    - debug:
        msg: "Fact gathering is disabled"
```

✅ Explanation:

gather_facts: yes → Automatically collects host information before executing tasks

gather_facts: no → Disables fact gathering to speed up playbook execution

## Using Facts in Playbooks

Facts can be used like regular variables in your playbooks.

They allow tasks to be dynamic, based on actual host information.

Collecting facts may take some time, so you can disable it for faster playbook runs if needed.