# Ansible Role: OPCS - XDR Agent
This role installs or removes the Cortex XDR Agent.

## Requirements

The XDR Agent is downloaded directly from the Cortex API Endpoint. In order for this, and to collect agent information an API Key is required. 
The API key must be an advanced key, and must have the `Ansible Automation` role selected during deployment.

Ask your XDR Administrator to provide the role variables below. 

[Cortex XDR™ API Reference](https://docs.paloaltonetworks.com/cortex/cortex-xdr/cortex-xdr-api.html)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Variable     | Description                                                                                                                             | Default   | Required |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- | --------- | ------------ |
| `xdr_state` | Whether the agent should be installed `present` or not `absent`. `check` can also be specified to just check if the agent is installed | `present` | N |
| `xdr_force` | Force the installation or removal of the agent                                                                                         | `false`   | N  |
| `xdr_base_uri` | Path to Palo Alto Networks Cortex XDR Cloud instance |  | Y |
| `xdr_linux_distribution_id` | Distribution ID for Linux package in XDR |  | Y |
| `xdr_windows_distribution_id` | Distribution ID for Windows package in XDR |  | Y |
| `xdr_api_key_id` | ID for XDR API Token |  | Y |
| `xdr_api_key_advanced` | Advanced API key for XDR API. Must have Ansible profile |  | Y |
| `xdr_agent_installer_name` | Installer binary name. Will have appropriate suffix added. | xdr_agent_installer | N |
| `xdr_windows_temp_path` | Temporary path on Windows for installer and logs | C:\temp\cortex | N |
| `xdr_linux_temp_path` | Temporary path on Linux for installer and logs | /tmp/cortex | N |
| `xdr_msi_product_id` | Windows MSI ID for Cortex Agent | {438C903A-8D5D-4809-B757-0E7788A3D423} | N |
| `xdr_uninstall_password` | Uninstall password only required for Windows agent removal. |  | ? |
| `xdr_version_linux` | Windows agent version being deployed | 7.3.0.16397 | N |
| `xdr_version_windows` | Linux agent version being deployed | 7.3.0.16740 | N |

The version variables are only used for determining if an agent needs to be upgraded. If the installed agent version is less than the versions specified the agent will be upgraded. (Forced install)

## Dependencies

## Example Playbook

```yaml
---
- name: Install Cortex XDR Agent
  hosts: all
  vars:
    xdr_state: present
    xdr_base_uri: https://api-myxdrdomain.xdr.ca.paloaltonetworks.com
    xdr_windows_distribution_id: 9fe8e474517144c0a31085727153587b
    xdr_api_key_id: 1
    xdr_api_key_advanced: apikey
    xdr_uninstall_password: 'secretpassword'
  tasks:
    - include_role: 
        name: cortex-xdr-ansible-role
        
```

