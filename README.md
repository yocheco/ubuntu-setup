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

### Git guardar credenciales
```
git config --global credential.helper cache
```





