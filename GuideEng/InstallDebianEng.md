# === Installing Debian on a Virtual Machine ===
## 1. Installing a virtual machine and an iso file
First you need to download a virtual machine ([link to the virtual machine](https://www.virtualbox.org/wiki/Downloads )).

We will use Oracle VirtualBox. After installing the VM, download the ios file of our Debian ([link to the ios file](https://www.debian.org/download )).

## 2. Creating a virtual machine
Let's go to Oracle VirtualBox and create a new machine. We specify the name of the machine, the folder for storing the machine, the type and version of the OS:  
![{E1633849-079D-47B6-98D3-2C20FC5ECFA1}](https://github.com/user-attachments/assets/fbb67a83-cc7d-4355-b3a6-7b8256e1e46b)

Next, we allocate RAM and cores for our virtual machine: ![{6550EE04-4C29-481C-8124-6BE158A2B5FC}](https://github.com/user-attachments/assets/77b6087b-11f8-4ae6-8bb4-e489e515bb9a)

Next, specify the storage location for the machine's hard disk: ![{E35EF6A4-65E1-4103-8CF2-C90731AB7257}](https://github.com/user-attachments/assets/a43d8588-da73-4adf-ad88-9b32c99df06a)

Create a machine and go to "Tools/Network". There we click on "Create" and get the following (we look at the VirtualBox Host-Only Enthernet Adapter):  
![{D7E83F8C-4090-46CB-9ED4-A2B5C96155F7}](https://github.com/user-attachments/assets/8ca1db09-44bc-4e36-a529-6e50b0506ef4)

We turn on the DHCP server and save the changes.

Go to the settings of the created machine and go to the "Network" tab there. We make the following settings: ![{D5235A89-D469-43BB-BA5C-0710B5CADEE2}](https://github.com/user-attachments/assets/22c78c16-90fc-4a89-b8c1-e57cba86fdef )  
![{7EC4E036-D58B-4175-9B99-CA488C1C275E}](https://github.com/user-attachments/assets/a535cd95-6168-43f3-bdc8-9ab2b4145a8d)  
(We need the "Host-Only adapter" in order for the main machine to be able to connect to the VM and vice versa)

Save the changes and start the machine. The following window will pop up: ![{AD082118-426E-4B5D-86D6-AA31BB9A6C24}](https://github.com/user-attachments/assets/0799a8a2-bcb7-450c-b11b-c87c2bb2da30)

We specify the path to our iso file, mount and restart the machine.

## 3. Installing Debian
Select "Graphic Install". Select the language, your "location" and the keyboard layout.

Next, in "Configuration of the network", select enp0s8 (then I'll explain why): ![{230FC1DC-1AA6-442F-888B-CE22A3D2A224}](https://github.com/user-attachments/assets/34d63528-1f79-439b-85dc-fe47b43a85c5)

Configure "Configuration of the network" as follows: ![{CC144728-0981-44A1-A3C2-E1B3C39B9902}](https://github.com/user-attachments/assets/69e9e3bd-b081-45a9-b781-0ca663000284)  
![{74E2EF95-0A33-4182-A127-F3682D736CE0}](https://github.com/user-attachments/assets/5d0fb0e7-8738-41c0-9b32-9425ffb43c37)  
![{42B3001F-DEEE-4042-A23B-B2A38B6C8D75}](https://github.com/user-attachments/assets/de6290d7-f935-4983-9e12-32aedd22fffc)

Specifies the host name:  
![{9B1DAFB5-076E-4644-A0E2-063D3A1EBFD5}](https://github.com/user-attachments/assets/445e3dd9-6145-4fc0-bde5-8f58a36a1af8)

(You can skip the domain)

We specify the password for the root:  
![{31E271DF-ECA9-4511-A7F3-1BEEEBB18051}](https://github.com/user-attachments/assets/093d2b26-fee7-4382-9111-ad97297507a3)

We specify the user's name and password for this user. ![{52F6640A-5235-4C6B-A8E6-BE72DE5DF3CF}](https://github.com/user-attachments/assets/42d99ea5-80e8-481f-b90d-4327bf0cea96)  
![{91FD77BC-CCB1-425B-A0E3-C748865F49E6}](https://github.com/user-attachments/assets/201e3192-0152-4caa-9a76-47aa3898e967)  
(the user's password does not exactly match the root password :))

Now the most interesting thing is the disk layout. It is advisable to be careful here, as we will mark up the disk manually.

Choosing our disk:  
![{8F3C5397-D8FD-4A85-9963-B9119336A016}](https://github.com/user-attachments/assets/95ca8da7-aa3c-4ac3-bb80-51a229b731ad)

Creating a new empty markup:  
![{42D13A43-545A-4FA2-ADA2-A4D3F64E740D}](https://github.com/user-attachments/assets/c5dc81f1-1dc6-4b5c-91a9-4ea9f451ade5)

First, let's create a "/boot" partition. Click on "create new partition", select a place for this partition (1 GB), select primary partition type, create a partition at the beginning of the disk. In "mount point", select "/boot" and we can finish with this section. You should get the following:  
![{70E053E8-38EC-4B5D-B779-5B692EF9A35B}](https://github.com/user-attachments/assets/b22f2880-3db0-49d9-b00f-a0c5344b9d35)

Next, select "configure the Logical Volume Manager" and then click "create volume group". We give our group a name: ![{873D5DE8-5840-4B49-98F3-FAEDF3B3C184}](https://github.com/user-attachments/assets/32ecb3d7-eaa1-4a00-a246-2065f0bd180c)

Selecting a device for the group: ![{68648589-9A9B-453C-9536-F2E442E21C70}](https://github.com/user-attachments/assets/3a27fd97-9e32-4456-98a3-b9a104ba43c2 )  
![{DA873D96-1271-4FC6-9EB2-38F0E431537B}](https://github.com/user-attachments/assets/3c1a8af0-7536-4961-a4c2-bf32e1a8a89a)

Now we can start creating logical partitions. Click on "create logical volume". We set a name for our section, for example, "vg-home":  
![{920E0331-2EB1-47A6-85F9-C12D282DA30C}](https://github.com/user-attachments/assets/71bc0688-4f32-4ed0-a219-2f0443638f80)

We allocate memory for a logical partition: ![{607FD455-7240-43DF-9D97-4357BA88A560}](https://github.com/user-attachments/assets/28d3e73b-7dc6-4406-b89e-8344f505c6b9)

And we do this procedure for the following sections:
- "vg-root", 4GB
- "vg-var", 2GB
- "vg-var-log", 2GB
- "vg-var-tmp", 2GB
- "vg-opt", 2GB
- "vg-tmp", 2GB

The result should be the following:  
![{EC86DA2C-C3BC-49FE-AF3A-EA46ABA70E19}](https://github.com/user-attachments/assets/4c9f79ee-cd2e-4cbe-a417-05af7e40f4fc)

Now, as for the "/boot" partition, we will configure the file system for each partition (for all ext4) and the mount point (look at the partition names). The result should be the following:  
![{34315B2E-F6F3-43D1-82CF-8FFBD4155206}](https://github.com/user-attachments/assets/c8ffa21d-5e90-4f79-926b-693f4683b764)

So, during the markup, the following picture should be obtained: ![{B0D2F0A4-3C24-4BF0-A3C2-D95EB954A5B1}](https://github.com/user-attachments/assets/445a1052-36f7-48bb-90f9-a8138c286358)

Here we select "no":  
![{5752E85E-DC8F-4EEF-A5A4-A28DFF68497A}](https://github.com/user-attachments/assets/cc7f252c-0c18-422a-9af0-706148ffd53b)

Next, they ask you to select "Network mirror", but for now we will continue without it. And here it is worth saying why I do this. let's remember that we chose enp0s8 instead of enp0s3, I did this because when choosing enp0s3, when it came to choosing a mirror, neither mirror wanted to load and, in principle, I could not proceed to other steps, as there was an error that I did not know how to deal with. In the end, I decided to try using enp0s8 instead of enp0s3. Because of this choice, after installing Debian, you will have to manually install a mirror and download some programs/utilities that can be said during the installation of debian, but this is better than not being able to install debian at all.

In the "software selection" item, select "standard system utilities" (we are not given anything else :)). When asked "Install the GRUB loader?" we answer "yes" and the installation comes to an end.
