# === SSH installation, mirror setup, network setup ===
## 1. Configuring network interfaces
In order for us to have Internet access or be able to communicate with the main machine, we need to configure the network correctly, namely, configure enp0s3 and enp0s8.

First, use the ip a command to view all network interfaces:  
![{7683B33E-4EC4-4C31-8991-D25BB1FFEDDD}](https://github.com/user-attachments/assets/b216b7c7-4489-419c-97b3-777a684b823c)

To configure the interfaces, use `nano /etc/network/interfaces`:  
![{EC9DD3C1-0C7B-43A7-97F4-4A4E93987593}](https://github.com/user-attachments/assets/d980de4e-4c49-47c9-a82c-36f8ecdfd1d6)

We change this file as follows:  
![{E574894B-EBF2-4F2E-86EC-5C95829E4FA2}](https://github.com/user-attachments/assets/607c85c4-c670-4a7f-854e-a7993f666434)

And restart the service after these changes with the command `systemctl restart networking'.

##2. Mirror Setup
If you selected enp0s8 when installing debian, you will need to set up a mirror after installation.

Let's use the command `nano /etc/apt/sources.list` and see that there is only one line in this file, comment it out (you need to put a # in front of this line). After that, we go to the Debian mirrors website and copy the mirrors we need from there ([link](https://www.debian.org/mirror/list )). I got the following (your result may vary depending on your place of residence and your own preferences):  
![{9BA48F61-78DE-42D3-879A-DE8731179CFE}](https://github.com/user-attachments/assets/383fab1b-a35a-4e6a-a103-ee56643e73ae)

## 3. Installing SSH
We need SSH in order, roughly speaking, to remotely manage the server (i.e. to our VM) via ssh. It is worth saying that this protocol provides not just a connection, but a secure connection.

So, to install ssh, use the command `apt install openssh-server -y'. After installation, using the `systemctl ssh status` command, we check the ssh operation: ![{FA26A85E-8A80-46FB-93C4-15C7EB8FC823}](https://github.com/user-attachments/assets/e165c051-ac70-4742-868d-e8543dd9495b)
