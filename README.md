# ubuntu-setup

useradd -m -s /bin/bash admin

usermod -aG sudo admin

rsync --archive --chown=admin:admin ~/.ssh /home/admin
