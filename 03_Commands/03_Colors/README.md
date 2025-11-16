# Understanding Ansible Output Colors

When running Ansible playbooks, the output is displayed in different colors. These colors help you quickly understand what happened during execution.

## Meaning of Colors

- **Green**: The task executed successfully and **no changes** were made.  
- **Yellow**: The task executed successfully and **changes were made**.  
- **Red**: The task **failed** to execute.  
- **Blue**: The task was **skipped** due to a conditional.

> Note: Colors are only for quick readability of the output.

```yaml
[user@ansible] $ ansible-playbook saleh.yml
PLAY [webservers] ***************************************

TASK [Ensure httpd package is present] ******************
ok: [web1]
changed: [web2] Failed: [web3]
skipping:[web4] 
```
