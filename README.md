# ubuntu setup


### Create admin user

👤 Create a new user name admin and add home files and bash
```
useradd -m admin -s /bin/bash -g admin
```

🔐 Add passwor to new user admin
```
passwd admin
```

🥷🏻 Add sudo group
```
usermod -aG sudo admin
```

📄 Copy shh to login
```
rsync --archive --chown=admin:admin ~/.ssh /home/admin
```

### Delete user

☠️ Delete user
```
userdel admin -r admin
```
👁 View passwords to user in the machine
```
cat /etc/passwd
```

### Install firewall

```
ufw app list
```
Output
Available applications:
  OpenSSH

```
ufw allow OpenSSH
```
```
ufw enable
```
```
ufw status
```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)

### SSH

🔐 Copy public key ssh to server 
[-p] to port
```
ssh-copy-id ubuntu@192.168.0.x
```

🪤 Delete login to password 
```
nano /etc/ssh/ssh_config
```
and #   PasswordAuthentication yes.  to no

📓 File save public ssh rsa keys in /home/$USER/.ssh

### Git
🧠 guardar credenciales
```
git config --global credential.helper store
```

```
git config --global credential.helper cache
```


