# Установка и настройка Auditd
## 1. Установка Auditd
Установим "Auditd" командой `apt install auditd`

## 2. Настройка Auditd

### 2.1 Правило мониторинга файла "/etc/passwd", "/etc/shadow", "/etc/sudoers", "/etc/sudoers.d"
Создаем правила следующим образом:  
```bash
auditctl -w /etc/passwd -p wa -k soc_passwd_rule
auditctl -w /etc/shadow -p wa -k soc_shadow_rule
auditctl -w /etc/sudoers -p wa -k soc_sudoers_rule
auditctl -w /etc/sudoers.d -p wa -k soc_sudoers_rule
```

Разберемся более подробно:
- -w: указываем путь до файла для мониторинга.
- -p wa: указываем права доступа (w - запись, a - изменение атрибутов).
- -k: задаем ключ для фильтрации логов.

### 2.2 Правило для мониторинга выполнения интерпретатора python
Создается правило следующим образом:  
```bash
auditctl -a always,exit -F arch=b32 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
```

Разберемся более подробно:
- -a always,exit: always - всегда регистрировать событие, exit - ловить завершение системного вызова.
- -F arch=b32/64: фильтр для 64-битных систем.
- -S execve: отслеживает вызов "execve()".
- -F exe=/usr/bin/python3: путь к исполняемому файлу.

### 2.3 Правило для мониторинга использования sudo
Данное правило будет отслеживать выполнение программ с использованием UID (например выполнение программ через sudo).

Создается правило следующим образом:  
```bash
auditctl -a always,exit -F arch=b32 -C euid!=uid -F auid!=unset -S execve -k user_emul
auditctl -a always,exit -F arch=b64 -C euid!=uid -F auid!=unset -S execve -k user_emul
```

Разберемся более подробно:
- -C euid!=uid: фильтровать случаи, когда эффективный UID не равен настоящему UID
- -F auid!=unset: игнорировать процессы без аудит UID

### 2.4 Правила для мониторинга изменения во времени
Создаются правила следующим образом:  
```bash
auditctl -a always,exit -F arch=b32 -S adjtimex,settimeofday -k time_change 
auditctl -a always,exit -F arch=b64 -S adjtimex,settimeofday -k time_change 
auditctl -a always,exit -F arch=b32 -S clock_settime -F a0=0x0 -k time_change 
auditctl -a always,exit -F arch=b64 -S clock_settime -F a0=0x0 -k time_change 
auditctl -w /etc/localtime -p wa -k time-change
```

## 3. Сохранение правил
Для начала воспользуемся командой `auditctl -l`, чтобы вывести все созданные правила. Вывод должен быть примерно следующим:  
```bash
-w /etc/passwd -p wa -k soc_passwd_rule
-w /etc/shadow -p wa -k soc_shadow_rule
-w /etc/sudoers -p wa -k soc_sudoers_rule
-w /etc/sudoers.d -p wa -k soc_sudoers_rule
-a always,exit -F arch=b32 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
-a always,exit -F arch=b64 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
-a always,exit -F arch=b32 -C euid!=uid -F auid!=unset -S execve -k user_emul
-a always,exit -F arch=b64 -C euid!=uid -F auid!=unset -S execve -k user_emul
-a always,exit -F arch=b32 -S adjtimex,settimeofday -k time_change 
-a always,exit -F arch=b64 -S adjtimex,settimeofday -k time_change 
-a always,exit -F arch=b32 -S clock_settime -F a0=0x0 -k time_change 
-a always,exit -F arch=b64 -S clock_settime -F a0=0x0 -k time_change 
-w /etc/localtime -p wa -k time-change
```

Запись по файлам будем производить следующим образом:  
```bash
bash -c 'auditctl -l | head -n 4 > /etc/audit/rules.d/10-file-watch.rules'
bash -c 'auditctl -l | sed -n 5,6p > /etc/audit/rules.d/20-python-exec.rules'
bash -c 'auditctl -l | sed -n 7,8p > /etc/audit/rules.d/30-uid-change.rules'
bash -c 'auditctl -l | tail -n 5 > /etc/audit/rules.d/40-time-change.rules'
```

Перезапускаем "auditd" командой `systemctl restart auditd`. Далее повторяем команду `auditctl -l` и если вывод идентичен, то все сделано верно.