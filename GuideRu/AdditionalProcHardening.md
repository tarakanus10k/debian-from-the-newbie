# Настройка дополнительных укреплений процессов
## 1. Случайное расположение адрессного пространства
Установим следующий параметр в "/etc/sysctl.conf" или в файл в "/etc/sysctl.d/[имя файла].conf":  
```bash
printf "%s\n" "kernel.randomize_va_space = 2" >> /etc/sysctl.d/60-kernel_sysctl.conf
```

После этого запускаем следующую команду, чтобы установить активный параметр ядра:  
```bash
sysctl -w kernel.randomize_va_space=2
```

## 2. Ограничение "ptrace_scope"
Установим следующий параметр в "/etc/sysctl.conf" или в файл в "/etc/sysctl.d/[имя файла].conf":  
```bash
printf "%s\n" "kernel.yama.ptrace_scope = 1" >> /etc/sysctl.d/60-kernel_sysctl.conf
```

После этого запускаем следующую команду, чтобы установить активный параметр ядра:  
```bash
sysctl -w kernel.yama.ptrace_scope=1
```

## 3. Ограничение дампов памяти
