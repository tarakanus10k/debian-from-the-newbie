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
auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
```

Разберемся более подробно:
- -a always,exit: always - всегда регистрировать событие, exit - ловить завершение системного вызова.
- -F arch=b64: фильтр для 64-битных систем.
- -S execve: отслеживает вызов "execve()".
- -F exe=/usr/bin/python3: путь к исполняемому файлу.

## 3. Сохранение правил
Для сохранения написанных правил воспользуемся командой:  
```bash
bash -c "auditctl -l > /etc/audit/rules.d/my-audit-rules.rules"
```

После выполнения данной команды, файл "my-audit-rules.rules" должен содержать следующее:  
```bash
-w /etc/passwd -p wa -k soc_passwd_rule
-w /etc/shadow -p wa -k soc_shadow_rule
-a always,exit -F arch=b64 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
```