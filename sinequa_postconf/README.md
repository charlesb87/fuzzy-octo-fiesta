# README: sinequa_postconf

This Ansible role performs post-configuration tasks for **Sinequa 4 Azure environments**. It handles disk mounting, system hardening, service management, and the installation of developer tools across several VM roles.

---

## Role Purpose

The role is intended to run against different **host groups** and applies specific configuration logic depending on the target.

### Common
Applied to **all hosts**:
- Disables the Recycle Bin
- Sets the system timezone
- Mounts the **F:** drive
- Maps **Azure Files shares**

### Engine (`vm_engine`)
- Mounts and prepares the **1024 GB index disks**
- Assigns and cleans the **G:** drive

### Web App (`vm_webapp`)
- Configures firewall rules to allow portal access on **TCP 8443**

### Dev / Demo (`vm_dev`, `vm_dev2`, `vm_demo`)
Installs developer utilities such as:
- **Notepad++**
- **Insomnia**
- **Fiddler Classic**

---

## Requirements

### Ansible Collections

- `ansible.windows`
- `community.windows`
- `chocolatey.chocolatey`
- `azure.azcollection`

### Privileges

Most Windows operations are executed using **`runas` with the `SYSTEM` user**.

---

## Role Variables

Variables are defined in `defaults/main.yml`. You must provide the required Azure environment details.

| Variable | Description |
|--------|-------------|
| `storage_account_name` | Name of the Azure Storage Account |
| `storage_account_key` | Access key for the storage account |
| `azure_share_suffix` | Name of the Azure File Share |
| `secure_keyvault_name` | URI of the Key Vault storing local admin passwords |
| `insomnia_url` | Direct download URL for the Insomnia installer |
| `fiddler_url` | Direct download URL for the Fiddler Classic installer |

---

## Directory Structure
