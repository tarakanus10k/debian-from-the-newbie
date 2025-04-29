# === Настройка и работа с SSH ===
## 1. Создание SSH ключа
Создавать ключи буду на основной машине (windows). Создадим ключ для пользователя "srvadmin" и "script runner" следующими способами:

Для "srvadmin":  
```powershell
ssh-keygen -t ed25519 -C "ed25519-srvadmin-key"
```

Для "script-runner":  
```powershell
ssh-keygen -t ed25519 -C "ed25519-script-runner-key"
```
