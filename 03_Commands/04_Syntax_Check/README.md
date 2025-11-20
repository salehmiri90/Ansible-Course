# Ansible Playbook Syntax Check

Before running a playbook, it's important to ensure that the YAML structure is valid. Ansible provides a built-in method to check the syntax of a playbook **without executing any task**. This helps avoid errors, prevent risky changes, and speed up debugging.

## Why Syntax Checking Matters

- Prevents executing a broken or unsafe playbook  
- Detects YAML errors before applying changes  
- Saves time during testing and troubleshooting  
- Increases confidence when running playbooks in sensitive environments (especially production)

## What the Syntax Check Does

When running a syntax check, Ansible:

✔ Validates YAML structure  
✔ Ensures indentation and spacing are correct  
✔ Checks essential keys like `hosts`, `tasks`, `name`, etc.  
✔ Does **not** execute any task — only validates structure  

## When Should You Use Syntax Checks?

You should run a syntax check:

- Before running a playbook in **stage** or **production**  
- After adding roles, includes, variables, or major structural changes  
- During debugging or refactoring a playbook  
- Before every Git commit or push  

## Common Errors Found in Syntax Checks

- Incorrect indentation  
- Typos in module or key names  
- Tasks placed at the wrong YAML level  
- Missing `:` after a key  
- Issues in imported or included files  

## Example: Running a Syntax Check

To validate the syntax of a playbook, use:

```bash
ansible-playbook playbook.yml --syntax-check
```

## Faulty Playbook Example (Missing `:`)

An intentionally incorrect playbook:

```yaml
---
- name: install and start apache 
  hosts: web
  become: yes

  tasks:
    - name: httpd package is present
      yum
      name: httpd 
      state: latest
```

## Corrected Version

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
```

## Summary

- Syntax checking prevents errors and saves time  
- Use `--syntax-check` before running or deploying any playbook  
