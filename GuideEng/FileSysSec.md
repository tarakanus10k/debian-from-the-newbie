# === Configuring a secure file system ===

Before starting, we will use `nano /etc/fstab`, as we will write all the settings in this file. He can get sick as follows:  
![{98B10B01-3A3A-4728-9F5D-6F406D44654C}](https://github.com/user-attachments/assets/b87673bb-66ff-4a7b-be73-1ad9c171d86e)

## 1. Changing the "fstab" file
, we change this file as follows:  
![{5BE5DD06-B092-4EE9-B470-0E76A79164B2}](https://github.com/user-attachments/assets/fd7e1a67-913b-4a22-84fa-d91923d1acd4)

Let's go through the changes in more detail.:
- defaults: standard settings (rw, suid, dev, exec, auto, nouser, async)
- rw: write mode (read-write)
- nosuid: blocks SUID/SGID bits
- nodev: prohibits the use of devices ("/dev/...") in the
- noexec: prohibits the execution of programs in this section
- relatime: optimizes file access time recording
- size=2G: limits the size

After the changes, we save and use the `mount -o remount -a` command to apply the changes. After this command, we use the `systemctl daemon-reload` command so that the system uses the new version of the file system.

## 6. Checking the correctness of the file system configuration  
using the `mount -a` command, we check the correctness of the configuration:
![{A3CC3090-5883-4756-8083-2800E9E99E5D}](https://github.com/user-attachments/assets/41f82aaf-d45f-4aef-bbf0-4dc89e99e52d)

Since there is no output, it means that everything is configured correctly.
