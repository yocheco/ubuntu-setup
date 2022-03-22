# ubuntu-setup

useradd -m admin -s /bin/bash -g admin

passwd admin

usermod -aG sudo admin

rsync --archive --chown=admin:admin ~/.ssh /home/admin


---------------------- delete users----------------

userdel admin -r admin

----------------------list users-------------------

cat /etc/passwd

--------------------firewall -----------------------------------
ufw app list

Output
Available applications:
  OpenSSH
  
ufw allow OpenSSH
ufw enable
ufw status

Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)


-------------------------git guardar credenciales----------------------
git config --global credential.helper store





