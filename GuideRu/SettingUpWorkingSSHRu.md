# === Настройка и работа с SSH ===
## 1. Создание SSH ключа
Создавать ключи буду на основной машине (windows). Создадим ключ для пользователя "srvadmin" и "script runner" следующими способами:

1) Для "srvadmin":  
```powershell
ssh-keygen -t ed25519 -C "ed25519-srvadmin-key"
```

После вас попросят путь сохранения ключа. По умолчанию ключ сохраниться в ".ssh" папку того пользователя, кто создает ключ.

Далее вас попросят создать фразу-пароль. Вводим ее и наш ключ создан.

Весь процесс создания ключа будет выглядеть следующим образом:  
![{156DA4B4-7BCB-470D-B2DC-B0A2EED1DA37}](https://github.com/user-attachments/assets/67511328-b032-4517-b7db-808eef1e89ac)

2) Для "script-runner":  
```powershell
ssh-keygen -t ed25519 -C "ed25519-script-runner-key"
```

После вас попросят путь сохранения ключа. По умолчанию ключ сохраниться в ".ssh" папку того пользователя, кто создает ключ.

Далее вас попросят создать фразу-пароль. Вводим ее и наш ключ создан.

Весь процесс создания ключа будет выглядеть следующим образом:  
![{E3C13B65-7E7E-4079-B775-36AEC2D91084}](https://github.com/user-attachments/assets/9755bd0d-b9f0-40df-969b-6edac80da892)

## 2. Перенос публичного ключа с основной машины на виртуальную
Перенесем публичные ключи следующим образом:

1) Для "srvadmin":

Для начала в домашней дериктории "srvadmin" создадим дерикторию "/.ssh":  
```bash
mkdir ~/.ssh
chmod 700 ~/.ssh
```

Далее в "/.ssh" создаем файл "authorized_keys":  
```bash
touch ~/.ssh/authorized_keys
```

На основной машине прописываем следующее:  
```powershell
scp [путь до вашего pub ключа] srvadmin@192.168.56.100:~/.ssh/authorized_keys
```

Вывод должен быть следующим:  
![{3D7F1476-8A76-4650-9C80-8C0585EA57C4}](https://github.com/user-attachments/assets/77a4236f-539c-46fd-8c60-9f8d0069692f)

2) Для "script-runner"

Для начала в домашней дериктории "srvadmin" создадим дерикторию "/.ssh":  
```bash
mkdir ~/.ssh
chmod 700 ~/.ssh
```

Далее в "/.ssh" создаем файл "authorized_keys":  
```bash
touch ~/.ssh/authorized_keys
```

На основной машине прописываем следующее:  
```powershell
scp [путь до вашего pub ключа] script-runner@192.168.56.100:~/.ssh/authorized_keys
```

Вывод должен быть следующим:  
![{EBD7195E-D7E1-47CE-AEAB-C07D6B11EA7E}](https://github.com/user-attachments/assets/295ecbde-1d1e-49fa-9d60-43557fe104ed)

## 3. Проверка подключения
