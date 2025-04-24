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

(Host-Only adapter нам нужен для того, чтобы основная машина могла иметь возможность подключиться к виртуальной машине и наоборот)

Сохраняем изменения и запускаем машину. Выплывет следующее окно: 
