# Ansible Ad-hoc Commands

This repository contains a curated list of useful Ansible ad-hoc commands for practicing and managing remote systems effectively.

## Prerequisites

1. Create a inventory file in the`/etc/ansible/hosts` directory. If it was't created by default, make sure to create this directory 
   ```bash
    sudo nano /etc/ansible/hosts/inventory.ini
   ```

2. Configure your inventory file (default: `/etc/ansible/hosts`):
   ```
    ubuntu@54.172.6.7
    ubuntu@18.206.127.98
   ```

---

## Ad-hoc Commands

Below is a categorized list of Ansible ad-hoc commands.

### 1. **Ping All Hosts**
Test connectivity with all the hosts in your inventory:
```bash
ansible -i /etc/ansible/hosts/inventory.ini -m ping all
```

### 2. **Run a Shell Command**
Run a shell command (e.g., check disk space):
```bash
ansible -i /etc/ansible/hosts/inventory.ini -m ping all
```

### 3. **Copy Files to Remote Hosts**
Copy a file from the control node to the remote hosts:
```bash
ansible all -m copy -a "src=/path/to/local/file dest=/path/to/remote/file"
```

### 4. **Check Free Memory**
Get information about free memory on remote hosts:
```bash
ansible -i /etc/ansible/hosts/inventory.ini -m shell -a "free -m" all
```

### 6. **Install a Package**
Install a package using the `apt` or `yum` module:

- For CentOS/RHEL:
  ```bash
  ```

- For Debian/Ubuntu:
  ```bash
  ansible -i /etc/ansible/hosts/inventory.ini -m shell -a "sudo apt install docker.io -y" all
  ```



### 7. **Create a User**
Create a new user on remote hosts:
```bash
ansible -i /etc/ansible/hosts/inventory.ini -m user -a "name=admin-sachin password={{ '1234' | password_hash('sha512') }} state=present" db --become --become-user=root
```

##Ansible Inventory File Grouping

### 8. **Grouping Hosts in the Inventory File**
In Ansible, the inventory file is used to define groups of hosts and their properties. Grouping hosts together allows you to run commands and tasks on specific subsets of your infrastructure, which can be very useful for managing large-scale environments.
```bash
[web]
ubuntu@18.206.127.98
ubuntu@54.172.6.7

[db]
ubuntu@44.201.221.194
```
### 9. **Ping only DB group Hosts**

```bash
ansible -i /etc/ansible/hosts/inventory.ini -m ping db
```

### 10. **Check Uptime**
Check the uptime of remote hosts:
```bash
ansible -i /etc/ansible/hosts/inventory.ini -m command -a "uptime" all
```


## License

This repository is licensed under the [MIT License](LICENSE).
