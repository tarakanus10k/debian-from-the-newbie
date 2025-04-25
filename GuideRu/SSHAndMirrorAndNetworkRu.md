# === Установка SSH, настройка зеркала, настройка сети ===
## 1. Настройка сети
Чтобы мы могли что-либо скачивать или иметь возможность связаться с основной машиной нужно правильно настроить сеть, а именно настроить enp0s3 и enp0s8.

Для начала воспользуемся командой ip a, чтобы посмотреть все сетевые интерфейсы: ![{E7C33FED-00CA-49B7-9885-A0E461EE9884}](https://github.com/user-attachments/assets/181b1c49-5cfa-4478-ae4d-668bc9d60bd4)

Для настройки интерфейсов нужно воспользоваться "nano /etc/network/interfaces": ![{0A635D53-FC1C-49AC-8B8E-3F22FAC0197A}](https://github.com/user-attachments/assets/69334d1a-ce3e-45fa-8915-95a62858ad6a)

Изменяем этот файл следующим образом:  
![{1CD6DDF7-E719-434E-BBDE-34B9EFD19CEC}](https://github.com/user-attachments/assets/cae1c80f-7560-41fc-acf8-7611cfa4d429)

И перезапускаем сервис после данных изменений командой "systemctl restart networking"
