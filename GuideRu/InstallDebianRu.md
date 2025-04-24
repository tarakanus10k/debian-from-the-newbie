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

Указывает имя хоста:  
![{9B1DAFB5-076E-4644-A0E2-063D3A1EBFD5}](https://github.com/user-attachments/assets/445e3dd9-6145-4fc0-bde5-8f58a36a1af8)

(Домен можно пропустить)

Указываем пароль для рута:  
![{31E271DF-ECA9-4511-A7F3-1BEEEBB18051}](https://github.com/user-attachments/assets/093d2b26-fee7-4382-9111-ad97297507a3)

Указываем имя юзера, и пароль для этого юзера. ![{52F6640A-5235-4C6B-A8E6-BE72DE5DF3CF}](https://github.com/user-attachments/assets/42d99ea5-80e8-481f-b90d-4327bf0cea96)  ![{91FD77BC-CCB1-425B-A0E3-C748865F49E6}](https://github.com/user-attachments/assets/201e3192-0152-4caa-9a76-47aa3898e967)  
(пароль юзера точно не совпадает с паролем рута:))

Теперь самое интересное - разметка диска. Здесь желательно быть осторожным, так как мы будем размечивать диск вручную.

Выбираем наш диск:  
![{8F3C5397-D8FD-4A85-9963-B9119336A016}](https://github.com/user-attachments/assets/95ca8da7-aa3c-4ac3-bb80-51a229b731ad)

Создаем новую пустую разметку:  
![{42D13A43-545A-4FA2-ADA2-A4D3F64E740D}](https://github.com/user-attachments/assets/c5dc81f1-1dc6-4b5c-91a9-4ea9f451ade5)

Для начала создадим раздел "/boot". Нажимаеи на "create new partition", выделяем место для этого раздела (1 GB), тип раздела выбираем primary, создаем раздел в начале диска. В "mount point" выбираем "/boot" и можем заканчиваь с этим разделом. Должно получиться следующее:  
![{70E053E8-38EC-4B5D-B779-5B692EF9A35B}](https://github.com/user-attachments/assets/b22f2880-3db0-49d9-b00f-a0c5344b9d35)

Далее выбираеи "configure the Logical Volume Manager" и потом нажимаем "create volume group". Задаем имя нашей группе: ![{873D5DE8-5840-4B49-98F3-FAEDF3B3C184}](https://github.com/user-attachments/assets/32ecb3d7-eaa1-4a00-a246-2065f0bd180c)

Выбираем устройство для группы: ![{68648589-9A9B-453C-9536-F2E442E21C70}](https://github.com/user-attachments/assets/3a27fd97-9e32-4456-98a3-b9a104ba43c2)  
![{DA873D96-1271-4FC6-9EB2-38F0E431537B}](https://github.com/user-attachments/assets/3c1a8af0-7536-4961-a4c2-bf32e1a8a89a)

Теперь можем приступить к созданию логических разделов. Нажимаем на "create logical volume". Задаем имя нашему разделу, например "vg-home":  
![{920E0331-2EB1-47A6-85F9-C12D282DA30C}](https://github.com/user-attachments/assets/71bc0688-4f32-4ed0-a219-2f0443638f80)

Выделяем память под логический раздел: ![{607FD455-7240-43DF-9D97-4357BA88A560}](https://github.com/user-attachments/assets/28d3e73b-7dc6-4406-b89e-8344f505c6b9)

И такую процедуру проделываем для следующих разделов:
- "vg-root", 4GB
- "vg-var", 2GB
- "vg-var-log", 2GB
- "vg-var-tmp", 2GB
- "vg-opt", 2GB
- "vg-tmp", 2GB

В итоге должно получиться следующее:  
![{EC86DA2C-C3BC-49FE-AF3A-EA46ABA70E19}](https://github.com/user-attachments/assets/4c9f79ee-cd2e-4cbe-a417-05af7e40f4fc)

Теперь, как для раздела "/boot" настроим для каждого раздела файловую систему (для всех ext4) и точку монтирования (смотрим на название разделов). В итоге должно получиться следующее: ![{34315B2E-F6F3-43D1-82CF-8FFBD4155206}](https://github.com/user-attachments/assets/c8ffa21d-5e90-4f79-926b-693f4683b764)
