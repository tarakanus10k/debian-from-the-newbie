# === Configuring a secure file system ===

Before starting, we will use `nano /etc/fstab`, as we will write all the settings in this file. He can get sick as follows:
![{156D2D82-AED8-473C-B53C-E1A47EDFAEEF}](https://github.com/user-attachments/assets/49412adc-372a-424d-8d21-2d433d4559b1)  
(You may not have a swap if you didn't do it)

##1. Setting up "/tmp"
First, let's check if "/tmp" is mounted as a separate file system using the `df -h /tmp` command: ![{C3A52B59-3BDD-4573-8768-8C3C8BC64ECF}](https://github.com/user-attachments/assets/54b0e89d-fb99-4ce4-8fd1-c6ec61a8df4e)  
Since the specific file partition "/dev/mapper/vg-srv-vg-tmp" is specified, we can say that our "/tmp" is mounted as a separate file system.

Now using the command `mount | grep "/tmp"` let's check what needs to be configured for our "/tmp": ![{DA9D70AF-E349-43BA-A150-1E1F07568B34}](https://github.com/user-attachments/assets/c30ad69a-78c5-4366-94e0-43244715b892 )  
(We are looking at "/tmp", not "/var/tmp")

We return to "fstab" and, according to the Debian 12 CIS Benchmark, change our "/tmp": ![{F6DBC6D3-013C-480A-98CB-66BACD1715E0}](https://github.com/user-attachments/assets/23a2b1ea-bb60-4b19-a8b7-07a426b1caa0)

Let's go through the changes to "/tmp" in more detail:
- rw: allow reading and writing
- nosuid: Prohibits the execution of files with SUID bits (programs running with the rights of the owner).
- nodev: Prohibits the creation and use of device files (for example, /dev/sda) in /tmp.
- noexec: Prohibits the launch of executable files (binaries, scripts) from /tmp.
- relatime: Optimizes the recording of the last access time (atime) to files. Instead of constantly updating atime (as in strictatime), it records it only if the previous value is older than 24 hours or the file has been changed.
- Changing the pass from two to zero: tells the fsck utility not to check the /tmp partition when booting.

After all the changes, save the file and use the command `moint -o remount /tmp` to remount "/tmp" so that our changes apply:  
![{00E07354-89BD-45C7-AF71-F5267F1A0B1F}](https://github.com/user-attachments/assets/e4c49f25-f4ab-49bd-8ad4-6d3b5ac5efe5)

Use the `mount' command | grep "/tmp"` to check if our changes have applied: ![{7885D39D-A6B2-450B-8E85-9177D9411644}](https://github.com/user-attachments/assets/626e1872-ac41-46a5-bc95-de6e931e3f17 )  
(We are looking specifically at "/tmp", and not at "/var/tmp")

## 2. Setting up "/home"
First, let's check if "/home" is mounted as a separate file system using the `df -h /home` command: ![{9570ED85-9D50-4A21-B6CF-097B7E65BE31}](https://github.com/user-attachments/assets/31e873c0-6063-42c9-9f57-ea9e1a9235cc)  
Since the specific file partition "/dev/mapper/vg-srv-vg-home" is specified, we can say that our "/home" is mounted as a separate file system.

Now using the command `mount | grep "/home"` let's check what needs to be configured for our "/home": ![{63307B5F-6D79-41AD-8A2C-A8D787822349}](https://github.com/user-attachments/assets/071a00a9-d83d-4829-ac42-b53e1a107246)

We return to "fstab" and, according to the Debian 12 CIS Benchmark, change our "/home": ![{D6332C8D-E0B6-4A94-A9A3-360C8B3AB405}](https://github.com/user-attachments/assets/3d835c58-7ae4-4173-8ac8-1c897ce7371a)

Let's go through the "/home" changes in more detail:
- rw: allow reading and writing
- nosuid: Prohibits the execution of files with SUID bits (programs running with the rights of the owner).
- nodev: Prohibits the creation and use of device files (for example, /dev/sda) in /home.
- noexec: Prohibits the launch of executable files (binaries, scripts) from /home.
- relatime: Optimizes the recording of the last access time (atime) to files. Instead of constantly updating atime (as in strictatime), it records it only if the previous value is older than 24 hours or the file has been changed.
- Changing the pass from two to zero: tells the fsck utility not to check the /home partition when booting.

After all the changes, save the file and use the command `moint -o remount /home` to remount "/home" so that our changes apply:  
![{F9D2B6CD-B63D-4AEF-898A-A7E1EDA538D3}](https://github.com/user-attachments/assets/42ccd9ab-d92a-4c23-ab19-cc96ff46974a)

Use the `mount' command | grep "/home"` to check if our changes have applied: ![{72FFD82E-C6DC-452A-ABBC-AE046A656C5A}](https://github.com/user-attachments/assets/398cc146-43df-4209-8b0e-0073ec91cfbc)

## 3. Setting up "/var"
First, let's check if "/var" is mounted as a separate file system using the `df -h /var` command: ![{F62CD681-2D1B-41ED-89BB-B89974DD96A2}](https://github.com/user-attachments/assets/fe3d6fe5-c0d6-4142-9757-d88d55df5b67)  
Since the specific file partition "/dev/mapper/vg-srv-vg-var" is specified, we can say that our "/var" is mounted as a separate file system.

Now using the command `mount | grep "/var"` let's check what needs to be configured for our "/var":  
![{DEB4DFE1-C615-4F63-84B2-C4CBC8DE5E53}](https://github.com/user-attachments/assets/264e5270-7c47-4ad5-b4df-9efd737cb2d5 )  
(we are looking at "/var", not "/var/log" and "/var/tmp")

We go back to "fstab" and according to Debian 12 CIS Benchmark we change our "/var": ![{825098EA-01D4-4EFA-98AA-4ABFCD92182E}](https://github.com/user-attachments/assets/5662076a-9add-40eb-b8f9-78c79673f2de)

Let's go through the changes to "/var" in more detail:
- rw: allow reading and writing
- nosuid: Prohibits the execution of files with SUID bits (programs running with the rights of the owner).
- nodev: Prohibits the creation and use of device files (for example, /dev/sda) in /var.
- noexec: Prohibits the launch of executable files (binaries, scripts) from /var.
- relatime: Optimizes the recording of the last access time (atime) to files. Instead of constantly updating atime (as in strictatime), it records it only if the previous value is older than 24 hours or the file has been changed.
- Changing the pass from two to zero: tells the fsck utility not to check the /var partition when booting.

After all the changes, save the file and use the command `moint -o remount /var` to remount "/var" so that our changes apply:  
![{6C4F9E73-263B-4226-915B-4814CA03CA22}](https://github.com/user-attachments/assets/1d12f719-872e-4350-ba83-c8ee6dd3f326)

Use the `mount' command | grep "/var"` to check if our changes have applied: ![{9946A285-68E5-4978-BEBC-477FF0FF1FD3}](https://github.com/user-attachments/assets/0cf55763-8ab8-44a9-a282-2dfec32d90c7)

##4. Setting up "/var/tmp" and "/var/log"
Check if these file systems are mounted.:  
![{F79E63E9-EC30-445B-ADCE-664A9EBCD74D}](https://github.com/user-attachments/assets/d0c0a349-38e1-4970-afd7-24c7cb2f0eb6)

Let's check what changes need to be made to the file systems: ![{A05DE693-5EF2-4978-9ED3-E2AFC3593ACB}](https://github.com/user-attachments/assets/4e4e02aa-23e0-469f-884d-274a08ffc5cf)

We return to fstab and, according to Debian 12 CIS Benchmark, change our "/var/tmp" and "/var/log": ![{2F1DBCB1-4776-4820-BF50-06524D431E58}](https://github.com/user-attachments/assets/64c17c44-f5d9-4295-92b6-9fb7b102422b)

Saving and remounting these file systems:  
![{DBC716CE-242E-4D3A-955D-F56AC39C5E45}](https://github.com/user-attachments/assets/aa146fb9-939c-4c66-a9f0-7bc9cda209a1)

##5. Setting up "/dev/shm"
Enter the command `findmnt -kn /dev/shm` to check the current configuration:  
![{E9C26C60-A0AC-4129-843E-13656D129C9A}](https://github.com/user-attachments/assets/4478fd74-1a2c-4773-9588-b636c724267d)

Since "/dev/shm" is missing from "fstab", we will add it ourselves: ![{4BC6B66B-E7B7-4E6D-B94A-9CAD9339D2A5}](https://github.com/user-attachments/assets/e2aa8b70-a703-4058-9800-30c5c4545722)

Remount "/var/shm":  
![{00E2C381-93F3-4A86-82C4-615C88102F5C}](https://github.com/user-attachments/assets/2220bd75-3a1a-461d-8e6f-1ffce294e8f9)

Checking if the changes have been applied:  
![{AB5DE180-0E0B-48E2-B7EE-5F72F3819952}](https://github.com/user-attachments/assets/b56ef35b-f30f-4826-acb5-744b73bce7a7)

## 6. Checking the correctness of the file system configuration
using the `mount -a` command, we check the correctness of the configuration:  
![{A3CC3090-5883-4756-8083-2800E9E99E5D}](https://github.com/user-attachments/assets/41f82aaf-d45f-4aef-bbf0-4dc89e99e52d)

Since there is no output, it means that everything is configured correctly.
