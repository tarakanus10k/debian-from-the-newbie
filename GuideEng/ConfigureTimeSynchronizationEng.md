#=== Time synchronization ===
## 1. systemd-timesyncd
First, let's check if systemd-timesyncd is active and enabled:  
![{B467E79E-71A1-4588-B30A-FF948B1BFF5C}](https://github.com/user-attachments/assets/9b6a29c7-21d3-4d66-a709-8c8bfcd2a81f)

Let's check the settings of the NTP servers:  
![{43625596-13A2-474F-AB19-8378378404B1}](https://github.com/user-attachments/assets/f8987a35-352b-43b0-af29-b56e119b9b5b)  
(since all lines are commented out, the default settings are used)

To configure systemd-timesyncd, we will use NTP servers google.com . Open "timesyncd.config" and change it as follows:  
![{ADA6BD57-D3B5-419C-AFDD-1EFF7ED51871}](https://github.com/user-attachments/assets/76b0475c-a5a7-46e0-9836-72b86038c99f)

After the changes, we will restart the service using the `systemctl restart systemd-timesyncd` command. Let's check the NTP status:  
![{47FED7D6-372D-4948-924B-975531818209}](https://github.com/user-attachments/assets/ca1c707c-b5cf-4aaf-ac08-c1cf2afb4d47)

Let's check how NTP works:
- Current time synchronization status:  
![{F0A8697E-B3B7-45D6-9F06-18854F94E4FB}](https://github.com/user-attachments/assets/8cc0f5a3-46b8-4912-99e9-729202127454 )  
- We will find in the logs of the "system-timesyncd" a message about connecting to the NTP server time.google.com and successful synchronization:  
![{746B37CA-4176-4B4F-A593-E4398E46A116}](https://github.com/user-attachments/assets/c3cec868-423c-455c-887d-523c9b580bfe)
