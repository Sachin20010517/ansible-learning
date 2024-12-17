# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```
    
When you are using WSL (Windows Subsystem for Linux)
```
 ssh-keygen -y -f ubuntu-default-key.pem > ubuntu-default-key.pem.pub
 eval $(ssh-agent -s)
 ssh-add ~/Ubuntu_Key1.pem

 
 ssh-copy-id -f -i Ubuntu_Key1.pem ubuntu@3.86.30.71
 
 
 ssh ubuntu@3.86.30.71

````

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
    ```
    sudo nano /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
    ```
>Note: This is for e2 instance, if you are using another type of VM, then use `sudo vim /etc/ssh/sshd_config` command, and uncomment `PasswordAuthentication` feild

- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`
- now create a password for ubuntu user
   ```
   sudo passwd ubuntu
   ````
 - now you can logout and check whether you can access it using password or not
   ```
   ssh-copy-id ubuntu@3.86.30.71
   ````

>Note: For this you must have SSH Key Pair on Your Local Machine. If you are using WSL with windows, please follow following steps
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

```
ssh-add -l
```
- If it shows `The agent has no identities`, you need to add your private key manually:
     ```
      ssh-add ~/.ssh/id_rsa
     ```
```
ssh-add -l
```
```
ssh-copy-id ubuntu@18.206.127.98
```




## Issue:

When you use SSH passwordless authentication in WSL, the SSH agent doesn't automatically load your SSH key after restarting WSL, opening a new terminal, or closing and reopening the terminal. This results in the inability to SSH into your remote servers without re-adding the SSH key manually.

Here’s an example of the steps that work initially, but fail after restarting the terminal:

```
nano ~/.bashrc
```
Add the following lines to start the SSH agent and load your SSH key automatically every time a new terminal session is opened:
```
# Start SSH Agent and add the key automatically
eval $(ssh-agent -s)  # Start the SSH agent
ssh-add -q ~/Ubuntu_Key1.pem  # Replace with the correct path to your private key
```
Apply the changes: After editing the file, apply the changes by running the following command:

```
source ~/.bashrc  # Or source ~/.zshrc for Zsh users
```


   

