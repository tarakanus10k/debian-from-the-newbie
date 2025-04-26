# === Настройка Time Synchronization ===
## 1. systemd-timesyncd
Для начала проверим активен ли и включен ли systemd-timesyncd:  
![{B467E79E-71A1-4588-B30A-FF948B1BFF5C}](https://github.com/user-attachments/assets/9b6a29c7-21d3-4d66-a709-8c8bfcd2a81f)

Проверим настройки NTP-серверов: ![{43625596-13A2-474F-AB19-8378378404B1}](https://github.com/user-attachments/assets/f8987a35-352b-43b0-af29-b56e119b9b5b)  
(так как все строки закомментированны, то используются настройки по умолчанию)

Чтобы настройть systemd-timesyncd, будем использовать NTP сервера google.com. Откроем "timesyncd.config" и изменим его следующим образом: ![{ADA6BD57-D3B5-419C-AFDD-1EFF7ED51871}](https://github.com/user-attachments/assets/76b0475c-a5a7-46e0-9836-72b86038c99f)

После изменений перезапустим сервис c помощщью команды `systemctl restart systemd-timesyncd`. Проверим статус NTP: ![{47FED7D6-372D-4948-924B-975531818209}](https://github.com/user-attachments/assets/ca1c707c-b5cf-4aaf-ac08-c1cf2afb4d47)
