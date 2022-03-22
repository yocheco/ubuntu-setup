# ubuntu-setup

useradd -m admin -s /bin/bash

passwd admin

usermod -aG sudo admin

rsync --archive --chown=admin:admin ~/.ssh /home/admin

