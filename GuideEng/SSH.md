# === Configuring and working with SSH ===
##1. Creating an SSH key
I will create keys on the main machine (windows). Create a key for the user "srvadmin" and "script runner" using the following methods:

1) For "srvadmin":  
```powershell
ssh-keygen -t ed25519 -C "ed25519-srvadmin-key"
```

After that, you will be asked for the way to save the key. By default, the key is saved to the ".ssh" folder of the user who creates the key.

Next, you will be asked to create a passphrase. We enter it and our key is created.

The entire key creation process will look like this:  
![{156DA4B4-7BCB-470D-B2DC-B0A2EED1DA37}](https://github.com/user-attachments/assets/67511328-b032-4517-b7db-808eef1e89ac)

2) For the "script-runner":  
```powershell
ssh-keygen -t ed25519 -C "ed25519-script-runner-key"
```

After that, you will be asked for the way to save the key. By default, the key is saved to the ".ssh" folder of the user who creates the key.

Next, you will be asked to create a passphrase. We enter it and our key is created.

The entire key creation process will look like this:  
![{E3C13B65-7E7E-4079-B775-36AEC2D91084}](https://github.com/user-attachments/assets/9755bd0d-b9f0-40df-969b-6edac80da892)

## 2. Transferring a public key from the primary machine to the virtual one
Transfer the public keys as follows:

1) For "srvadmin":

To begin with, we will create a "/.ssh" directory in the "srvadmin" home directory:  
```bash
mkdir ~/.ssh
chmod 700 ~/.ssh
```

Next, create the "authorized_keys" file in "/.ssh":  
```bash
touch ~/.ssh/authorized_keys
```

On the main machine, we prescribe the following:  
```powershell
scp [path to your pub key] srvadmin@192.168.56.100 :~/.ssh/authorized_keys
```

The output should be as follows:  
![{3D7F1476-8A76-4650-9C80-8C0585EA57C4}](https://github.com/user-attachments/assets/77a4236f-539c-46fd-8c60-9f8d0069692f)

2) For the "script-runner"

To begin with, we will create a "/.ssh" directory in the "srvadmin" home directory:  
```bash
mkdir ~/.ssh
chmod 700 ~/.ssh
```

Next, create the "authorized_keys" file in "/.ssh":  
```bash
touch ~/.ssh/authorized_keys
```

On the main machine, we prescribe the following:  
```powershell
scp [path to your pub key] script-runner@192.168.56.100 :~/.ssh/authorized_keys
```

The output should be as follows:  
![{EBD7195E-D7E1-47CE-AEAB-C07D6B11EA7E}](https://github.com/user-attachments/assets/295ecbde-1d1e-49fa-9d60-43557fe104ed)

## 3. Checking the connection
Let's check the SSH connection in two ways.

The first way. We introduce the following:  
```powershell
ssh srvadmin@192.168.56.100
```

After entering the command, you should be asked for the password of the user "srvadmin" and after entering the correct password, you should be allowed into the shell. It should look like this:  
![{23B57C36-121C-464C-87B4-8FC1C9F442D4}](https://github.com/user-attachments/assets/0c7e7ea6-8d2b-4c5f-aae0-7fdb3ac5d9d3)

The second way. We introduce the following:  
```powershell
ssh -i [path to your key] srvadmin@192.168.56.100
```

After entering the command, you should be asked for the passphrase that we wrote when creating the key, and after entering the passphrase correctly, you should be allowed into the shell. It should look like this:  
![{5065D163-39A0-4FB4-9956-F753735C540D}](https://github.com/user-attachments/assets/dbadd810-25b1-4527-9938-6a180ea2f7bf)

## 3. Script execution on connection
Let's make sure that when we connect to the "script runner", the script is executed and the connection is completed.

In the "script-runner" home directory, create the "access.bash", open it and write in it:  
```bash
#!/bin/bash
echo "[+] Logged at $(date) by $LOGGEDUSER"
```

Save and write the command `chmod +x ~/access.bash` to make the script executable.

Open the "authorized_keys" file and write in front of the line that is there:  
```bash
environment="LOGGEDUSER=script-runner",command="~/access.bash"
```

Now let's try to connect via SSH:  
![{BDAD1297-FC59-4A2B-99E7-8F39E3A7EF61}](https://github.com/user-attachments/assets/a66dfb61-c7b1-4426-ab7a-32b84f59b250)

As you can see, the script was executed upon connection and the connection was closed after the script was executed. But we see that after "by" nothing was output. To fix this, open the file "sshd_config" ("/etc/ssh/sshd_config") and look for the string "PermitUserEnvironment". We look for it and remove the "#" sign in front of it and change "no" to "yes". Save and restart sshd with the command `systemctl restart sshd'.

Now let's try to connect via SSH:  
![{B6F873A2-A486-44C2-A48A-86EA0B69DDA6}](https://github.com/user-attachments/assets/ad1a1195-6673-465e-bad4-845b3664de37)

##4. Setting up sshd_config
We will make it so that you can connect via ssh only with a passphrase, and we will also prohibit root from connecting via ssh. To do this, open "sshd_config", find the "PasswordAuthentication" and "PermitRootLogin" parameters in it, and write "no" next to these parameters. It should look like this:  
```bash
PasswordAuthentication no
PermitRootLogin no
```

Restart "sshd" and you're done.
