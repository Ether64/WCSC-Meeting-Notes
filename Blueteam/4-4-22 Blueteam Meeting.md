# Linux hardening (cont..)

-  First place should look: /etc/ssh

- `PermitRootLogin` should be disallowed

- Change sshd config: `sudo nano /etc/sshd_config`

- `sudo ufw default deny incoming`

- `sudo ufw default allow outgoing`

 - `sudo ufw allow 22`

- Find listening connections on machine `netstat -tulpn`

- Run netstat every 5-10 minute to see if a persistent shell is running on a machine.

- `htop` is a good way to filter for strange processes running on a Linux machine.

- Create script: ```!#bin/bash/ nc -nvlp 8080```

- Good way to check if crontab is running: 