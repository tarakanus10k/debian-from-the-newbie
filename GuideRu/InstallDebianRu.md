# === Установка Debian на Виртуальную машину ===
## 1. Установка виртуальной машины и iso файла
Для начала нужно скачать виртуальную машину ([ссылка на виртуальную машину](https://www.virtualbox.org/wiki/Downloads)).

Будем использовать Oracle VirtualBox. После установки ВМ скачаем ios файл нашего Debian ([ссылка на ios файл](https://www.debian.org/download)).

## 2. Создание виртуальной машины
Перейдем в Oracle VirtualBox и создаем новую машину. Указываем имя машины, папку для хранения машины, тип и версию ОС: ![{E1633849-079D-47B6-98D3-2C20FC5ECFA1}](https://github.com/user-attachments/assets/fbb67a83-cc7d-4355-b3a6-7b8256e1e46b)

Далее выделяем оперативную память и ядра для нашей виртуальной машины: ![{6550EE04-4C29-481C-8124-6BE158A2B5FC}](https://github.com/user-attachments/assets/77b6087b-11f8-4ae6-8bb4-e489e515bb9a)

Далее указываем место для хранения жесткого диска машины: ![{E35EF6A4-65E1-4103-8CF2-C90731AB7257}](https://github.com/user-attachments/assets/a43d8588-da73-4adf-ad88-9b32c99df06a)

Создаем машину и переходим в "Tools/Network". Там нажимаем на "Create" и получаем следующее (смотрим на VirtualBox Host-Only Enthernet Adapter):  
![{02B6DF0B-422A-4912-B5D7-1197467F3F07}](https://github.com/user-attachments/assets/4038e77c-c0ad-49dc-9edb-293d4f8edbd2)

Включаем DHCP сервер и сохраняем изменения.

Переходим в настройки созданой машины и там переходим во вкладку "Network". Делаем следующие настройки: ![{5810BDB7-E402-4ED2-BDC3-7CA91A46EA0A}](https://github.com/user-attachments/assets/238548a7-6f23-44dd-862b-083fc03b5ade)  ![{0464D68B-6647-48FF-B29C-01DF87F3FF0D}](https://github.com/user-attachments/assets/87fe03f5-29e3-451b-988f-1d4c5ac39750)

("Host-Only adapter" нам нужен для того, чтобы основная машина могла иметь возможность подключиться к виртуальной машине и наоборот)

Сохраняем изменения и запускаем машину. Выплывет следующее окно: ![{AD082118-426E-4B5D-86D6-AA31BB9A6C24}](https://github.com/user-attachments/assets/0799a8a2-bcb7-450c-b11b-c87c2bb2da30)

Указываем путь до нашего iso файла, монтируем и перезапускаем машину.

## 3. Установка Debian
Выбираем "Graphic Install". Выбираем язык, вашу "локацию" и раскладку клавиатуры.

Далее в "Configuration the network" выбираем enp0s8 (потом объясню почему): ![{230FC1DC-1AA6-442F-888B-CE22A3D2A224}](https://github.com/user-attachments/assets/34d63528-1f79-439b-85dc-fe47b43a85c5)

Настроим "Configuration the network" следующим образом: ![{52ED3226-22A7-444B-859A-AD7F7CE7DD8A}](https://github.com/user-attachments/assets/5ce3cbdf-a387-496d-81a6-4b606a52dc45)  ![{646B8B20-186B-4C3D-9ED4-5249EB42A455}](https://github.com/user-attachments/assets/fed99cc6-4cab-412f-96ad-3ce551f12bb3)  ![{AAC91043-B776-4C16-AD4B-10AB4DC025A9}](https://github.com/user-attachments/assets/f316a1c8-5feb-40e9-a9d0-8ba5de2e0bca)

Указывает имя хоста: ![{9B1DAFB5-076E-4644-A0E2-063D3A1EBFD5}](https://github.com/user-attachments/assets/445e3dd9-6145-4fc0-bde5-8f58a36a1af8)

(Домен можно пропустить)

Указываем пароль для рута: ![{31E271DF-ECA9-4511-A7F3-1BEEEBB18051}](https://github.com/user-attachments/assets/093d2b26-fee7-4382-9111-ad97297507a3)

Указываем имя юзера, и пароль для этого юзера. ![{52F6640A-5235-4C6B-A8E6-BE72DE5DF3CF}](https://github.com/user-attachments/assets/42d99ea5-80e8-481f-b90d-4327bf0cea96)  ![{91FD77BC-CCB1-425B-A0E3-C748865F49E6}](https://github.com/user-attachments/assets/201e3192-0152-4caa-9a76-47aa3898e967)  (пароль юзера точно не совпадает с паролем рута:))

