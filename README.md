# ubuntu setup

sudo htop


### Update sistem
```
sudo apt update
sudo apt upgrade --yes
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


=========================================================

/etc/ssh/sshd_config

PasswordAuthentication no
PermitRootLogin no
PubkeyAcceptedAlgorithms=ssh-ed25519,ecdsa-sha2-nistp256
sudo systemctl restart ssh



sudo ss -tp | grep ssh


who


sudo grep "Accepted" /var/log/auth.log
sudo grep "Accepted" /var/log/auth.log
sudo grep "session opened" /var/log/auth.log

scp admin@146.190.34.217:~/services/ikp_data/storage/logs/error.log .


Lista las fechas de modificación:
ls -l /etc/cron.*



1.3. Revisar el Archivo Principal de cron
ls -l /etc/crontab

### Install fail2ban
```
sudo apt install fail2ban
```
```
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
sudo systemctl status fail2ban
```

#### Config

```
sudo nano /etc/fail2ban/jail.loca
```

file jail.loca
```
[sshd]
enabled = true
port = ssh
maxretry = 3
bantime = 3600
```

=======================================================

1. Ver Instalaciones Recientes con dpkg (sistemas basados en Debian/Ubuntu)
El comando dpkg permite listar los paquetes instalados y sus fechas.

Ver lista de paquetes instalados recientemente:

bash
Copiar código
grep " install " /var/log/dpkg.log
Para buscar instalaciones en fechas específicas: Por ejemplo, del 15 de diciembre:

bash
Copiar código
grep " install " /var/log/dpkg.log | grep "2024-12-15"
Si los logs fueron rotados: Revisa los logs comprimidos:

bash
Copiar código
zgrep " install " /var/log/dpkg.log.*
2. Ver Instalaciones Recientes con rpm (sistemas basados en Red Hat/CentOS/Fedora)
Listar paquetes instalados ordenados por fecha:

bash
Copiar código
rpm -qa --last
Buscar un paquete instalado en una fecha específica:

bash
Copiar código
rpm -qa --last | grep "Dec 15"
3. Ver Modificaciones en Archivos del Sistema
Si algo fue instalado manualmente, revisa qué archivos se modificaron recientemente:

Buscar archivos modificados recientemente:

bash
Copiar código
find / -type f -mtime -7 2>/dev/null
Esto muestra los archivos modificados en los últimos 7 días.
Cambia -7 por el número de días que deseas analizar.
En directorios específicos (por ejemplo, /usr/bin):

bash
Copiar código
find /usr/bin -type f -mtime -7
Buscar binarios recién creados:

bash
Copiar código
find /usr/bin -type f -ctime -7
4. Ver Comandos Ejecutados Recientemente
Revisa los comandos ejecutados recientemente, lo cual podría incluir comandos para instalar software.

Historial de Bash: Ve el historial del usuario actual:

bash
Copiar código
history
Revisar otros usuarios: Revisa el archivo ~/.bash_history de otros usuarios, por ejemplo:

bash
Copiar código
sudo cat /home/admin/.bash_history
Filtra comandos relacionados con instalación: Por ejemplo, apt, yum, dnf, pip o wget:

bash
Copiar código
history | grep -E "apt|yum|dnf|wget|curl"
5. Ver Tareas Automatizadas
Revisa si alguien agregó tareas que instalen algo automáticamente.

Verificar cron jobs:

Lista las tareas programadas para todos los usuarios:
bash
Copiar código
sudo cat /etc/crontab
sudo ls /var/spool/cron/crontabs
Revisar scripts en /etc/cron.*:

bash
Copiar código
sudo ls -l /etc/cron.d/
sudo ls -l /etc/cron.daily/
6. Ver Nuevos Usuarios Creados
Si alguien instaló algo, podría haber creado un usuario adicional para administración.

Revisar usuarios recientes:

bash
Copiar código
sudo grep "/home" /etc/passwd
Ver cambios recientes en el archivo passwd:

bash
Copiar código
sudo stat /etc/passwd
7. Buscar Aplicaciones en Ejecución
Revisa si hay procesos inusuales ejecutándose, lo cual podría ser software recién instalado.

Ver procesos en ejecución:

bash
Copiar código
ps aux
Buscar procesos por directorio: Si sospechas de un directorio específico (por ejemplo, /tmp):

bash
Copiar código
ps aux | grep /tmp
Revisar procesos escuchando puertos (red):

bash
Copiar código
sudo ss -tulnp
8. Logs de Sistema
Revisa logs del sistema para buscar eventos inusuales.

Logs de auditoría (si auditd está habilitado):

bash
Copiar código
sudo ausearch -ts recent
Logs generales de sistema:162.243.188.66

=======================================================

1. Opciones de Antivirus para Linux
1.1. ClamAV
ClamAV es un antivirus gratuito y de código abierto, ampliamente utilizado para escanear archivos y detectar malware.

Instalar ClamAV:

bash
Copiar código
sudo apt update
sudo apt install clamav clamav-daemon
Actualizar la base de datos de virus:

bash
Copiar código
sudo freshclam
Escanear todo el sistema:

bash
Copiar código
sudo clamscan -r /
Escanear directorios específicos (por ejemplo, /home):

bash
Copiar código
sudo clamscan -r /home
Eliminar archivos infectados automáticamente:

bash
Copiar código
sudo clamscan -r --remove /

1.2. Sophos Antivirus
Sophos es gratuito para uso personal y ofrece protección avanzada.

Descargar e instalar Sophos:

Ve al sitio oficial de Sophos.
Descarga el instalador para Linux.
Sigue las instrucciones del archivo README incluido.
Escanear el sistema: Una vez instalado, usa el comando savscan para realizar análisis:

bash
Copiar código
sudo /opt/sophos-av/bin/savscan /

1.3. ESET NOD32
ESET ofrece una versión para Linux con funcionalidades avanzadas.

Descargar e instalar:

Ve al sitio oficial de ESET para Linux.
Descarga el archivo .deb para Ubuntu/Debian.
Instálalo:
bash
Copiar código
sudo dpkg -i eset_nod32av_*.deb
sudo apt install -f
Usar la interfaz gráfica o comandos para escanear.

1.4. Lynis (Auditoría de Seguridad)
Lynis no es un antivirus tradicional, pero realiza auditorías de seguridad y detecta configuraciones inseguras o potencialmente comprometidas.

Instalar Lynis:

bash
Copiar código
sudo apt update
sudo apt install lynis
Realizar un análisis completo:

bash
Copiar código
sudo lynis audit system
Lynis te proporcionará un informe con recomendaciones para mejorar la seguridad.

2. Detectar Rootkits
2.1. Rkhunter
Rkhunter detecta rootkits, backdoors y configuraciones inseguras.

Instalar Rkhunter:

bash
Copiar código
sudo apt install rkhunter
Actualizar la base de datos:

bash
Copiar código
sudo rkhunter --update
Realizar un análisis completo:

bash
Copiar código
sudo rkhunter --check
2.2. Chkrootkit
Chkrootkit es otra herramienta para detectar rootkits.

Instalar Chkrootkit:

bash
Copiar código
sudo apt install chkrootkit
Ejecutar un análisis:

bash
Copiar código
sudo chkrootkit
3. Monitoreo de Cambios en el Sistema

3.1. AIDE (Advanced Intrusion Detection Environment)
AIDE monitorea cambios en archivos críticos del sistema.

Instalar AIDE:

bash
Copiar código
sudo apt install aide
Inicializar la base de datos:

bash
Copiar código
sudo aideinit
sudo mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db
Verificar cambios:

bash
Copiar código
sudo aide --check
4. Configuración de Escaneo Regular
Usar cron para escaneos automáticos: Programa escaneos regulares con cron. Por ejemplo, para ClamAV:
bash
Copiar código
sudo crontab -e
Agrega esta línea para escanear diariamente a las 3:00 AM:
plaintext
Copiar código
0 3 * * * /usr/bin/clamscan -r / > /var/log/clamav-scan.log



