# Установка и настройка sudo
## 1. Установка sudo
Для установки sudo требуется ввести следующую команду:  
```bash
apt install sudo
```

## 2. Настройка sudo для пользователя "viromant"
Выполняем следующую команду:  
```bash
sudo visudo -f /etc/sudoers.d/viromant
```

И в открывшемся файле прописываем:  
```bash
viromant ALL=(ALL:ALL) NOPASSWD:ALL
```

Сохраняем и теперь пользователь "viromant" может использовать команду "sudo" не вводя пароль.

## 3. Настройка sudo для пользователя "srvadmin"
Выполняем следующую команду:  
```bash
sudo visudo -f /etc/sudoers.d/srvadmin
```

И в открывшемся файле прописываем:  
```bash
srvadmin ALL=(ALL:ALL) ALL
```

Сохраняем и теперь пользователь "srvadmin" может использователь команду "sudo", но при ее использовании ему нужно будет вводить пароль.

## 3. Настройка sudo для пользователя "appadmin"
Для начала создадим пользователя "appadmin". Открываем файл "passwd" и прописываем следующее:  
```bash
appadmin:x:1003:1001:appadmin:/home/appadmin:/bin/bash
```

Добавим пользователя "appadmin" в группу "admins" (создание группы "admins" смотреть в ["Настройка групп и пользователей"](/GuideRu/GroupsAndUsers.md)).

Создадим домашнюю директорию и зададим пароль новому пользователю:  
```bash
mkdir /home/appadmin
chown appadmin /home/appadmin
chmod 700 /home/appadmin
passwd appadmin
```

Создадим дерикторию "/var/log/sudo" с правами доступа 750. В этой дериктории создадим файл "appadmin.log".

Выполняем следующую команду:  
```bash
sudo visudo -f /etc/sudoers.d/appadmin
```

В открытом файле настроим логирование всех команд в формате json в файл "/var/log/sudo/appadmin.log":  
```bash
Defaults:appadmin logfile="/var/log/appadmin.log"
Defaults:appadmin log_format="json"
```

Теперь выполним команду `sudo visudo` и в нем пропишем алиас, который будет разрешать пользователю использовать команду "systemctl":  
```bash
Cmnd_Alias SERVICE_CMD=/bin/systemctl
```

С помощью команды `sudo visudo -f /etc/sudoers.d/appadmin` возвращаемся в файл для настройка прав для пользователя "appadmin" и подключаем наш алиас:  
```bash
appadmin ALL=(ALL:ALL) NOPASSWD:SERVICE_CMD
```

После сохранения может появиться сообщение `Cmnd_Alias "SERVICE_CMD" referenced but not defined`, то используем команду `sudo -U appadmin -l` и если после `appadmin ALL=(ALL:ALL) NOPASSWD:` находится "/bin/systemctl", то все хорошо:)

Сделаем так, чтобы пользователь "appadmin" мог выполнять bash-скрипты, которые находяться в директории "/opt/scripts". Выполняем команду `sudo visudo` и там пишем следующий алиас:  
```bash
Cmnd_Alias BASH_USE=/usr/bin/bash /opt/scripts/*.bash
```

И в файле "/etc/sudoers.d/appadmin" подключаем алиас:  
```bash
appadmin ALL=(ALL:ALL) NOPASSWD:SETENV:SERVICE_CMD,BASH_USE
```

"SETENV" нужен для того, чтобы можно было выполнять скрипты следующей командой:  
```bash
sudo -u appadmin sudo LOGGEDUSER=appadmin bash /opt/scripts/access.bash
```

Как помним в скрипте "access.bash" есть переменная "$LOGGEDUSER". Если бы мы не использовали "LOGGEDUSER=appadmin", то мы не получим корректный вывод скрипта. "SETENV" позволяет нам такое делать.

Запретим пользователю "appadmin" использовать команды `sudo su` `sudo -i`. `sudo visudo` и прописываем алиас:  
```bash
Cmnd_Alias FORBIDDEN_CMD=/bin/sudo su, /bin/sudo -i
```

И в файле "/etc/sudoers.d/appadmin" подключаем алиас:  
```bash
appadmin ALL=(ALL:ALL) !FORBIDDEN_CMD
```

Запретим пользователю выполнять подкоманды входа в системный шелл в утилитах "vim/less/more". `sudo visudo` и прописываем алиас:  
```bash
Cmnd_Alias EDITORS=/usr/bin/vim, /usr/bin/vim.tiny, /usr/bin/less, /usr/bin/more
```

И в файле "/etc/sudoers.d/appadmin" подключаем алиас:  
```bash
appadmin ALL=(ALL:ALL) !EDITORS
```

## 4. Проверка корректности доступа

Если при использовании команды `sudo visudo -c` у вас следующий вывод:  
![{E56C0D7F-A772-4416-8882-82990764FC74}](https://github.com/user-attachments/assets/50441757-726f-49a4-8ee9-ad314a734941)

То используем команду `sudo chmod 0440 /etc/sudoers.d/*`.
