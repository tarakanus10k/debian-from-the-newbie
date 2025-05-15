# Настройка AppArmor
## 1. Установлен ли AppArmor
Введем следующую команду для проверки установлен ли AppArmor:  
```bash
dpkg-query -s apparmor &>/dev/null && echo "apparmor is installed"
```

Если вывод равен "apparmor is installed", то AppArmor установлен.

Также проверим, установлены ли ApppArmor-утилиты:  
```bash
dpkg-query -s apparmor-utils &>/dev/null && echo "apparmor-utils is installed"
```

Если вывод равен "apparmor-utils is installed", то ApppArmor-утилиты установлен. Если же в выводе пусто, то скачиваем ApppArmor-утилиты командой:  
```bash
apt install apparmor apparmor-utils
```

## 2. Включен ли AppArmor в конфигурации загрузчика
Проверим, какие профиля загружены и находяться в режиме принужденяи или жалобы:  
```bash
apparmor_status | grep profiles
```

Проверим, есть ли процессы без ограничений:  
```bash
apparmor_status | grep processes
```

Вводим одну из следующих команд для установки всех профилей в режим принуждения/жалобы:  
- принуждения:  
```bash
aa-enforce /etc/apparmor.d/*
```
- жалобы:  
```bash
aa-complain /etc/apparmor.d/*
```