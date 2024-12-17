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

### 5. **Restart a Service**
Restart a service, e.g., `nginx`:
```bash
ansible webservers -m service -a "name=nginx state=restarted"
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

### 7. **Change File Permissions**
Change permissions for a file:
```bash
ansible all -m file -a "path=/path/to/file mode=0644"
```

### 8. **Create a User**
Create a new user on remote hosts:
```bash
ansible all -m user -a "name=testuser state=present"
```

### 9. **Gather Facts**
Get detailed information about the managed hosts:
```bash
ansible all -m setup
```

### 10. **Check Uptime**
Check the uptime of remote hosts:
```bash
ansible all -m command -a "uptime"
```

### 11. **Reboot Hosts**
Reboot remote hosts:
```bash
ansible all -m reboot
```

### 12. **Fetch a File from Remote Hosts**
Retrieve a file from remote hosts to the control node:
```bash
ansible all -m fetch -a "src=/remote/path/to/file dest=/local/path"
```

### 13. **Manage Firewall Rules**
Enable HTTP traffic in the firewall (e.g., using `firewalld` on CentOS):
```bash
ansible all -m firewalld -a "port=80/tcp state=enabled permanent=true"
```

---

## How to Contribute

1. Fork the repository.
2. Create a new branch for your changes:
   ```bash
   git checkout -b my-feature-branch
   ```
3. Commit your changes:
   ```bash
   git commit -m "Added new Ansible command examples"
   ```
4. Push your branch:
   ```bash
   git push origin my-feature-branch
   ```
5. Open a pull request.

---

## License

This repository is licensed under the [MIT License](LICENSE).
