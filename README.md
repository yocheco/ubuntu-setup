# ubuntu setup

sudo htop


### Update sistem
```
sudo apt update
sudo apt upgrade
```

### 🐋 Install docker
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```
### 🐋 Install docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


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

File ssh_config
```
 PasswordAuthentication no
 PermitEmptyPasswords no
 PermitRootLogin no
 ```
 sudo systemctl restart ssh
 

📓 File save public ssh rsa keys in /home/$USER/.ssh

### Git
🧠 guardar credenciales
```
git config --global credential.helper store
```

```
git config --global credential.helper cache
```


