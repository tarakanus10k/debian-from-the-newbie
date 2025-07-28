# Installing and configuring sudo
## 1. Installing sudo
To install sudo, enter the following command:  
```bash
apt install sudo
```

## 2. Configuring sudo for the "viromant" user
Run the following command:  
```bash
sudo visudo -f /etc/sudoers.d/viromant
```

And in the opened file we write:  
```bash
viromant ALL=(ALL:ALL) NOPASSWD:ALL
```

We save it and now the user "viromant" can use the "sudo" command without entering a password.

## 3. Configuring sudo for the "srvadmin" user
Run the following command:  
```bash
sudo visudo -f /etc/sudoers.d/srvadmin
```

And in the opened file we write:  
```bash
srvadmin ALL=(ALL:ALL) ALL
```

We save it and now the user "srvadmin" can use the command "sudo", but when using it he will need to enter a password.

## 3. Configuring sudo for the "appadmin" user
First, let's create an "appadmin" user. Open the "passwd" file and specify the following:  
```bash
appadmin:x:1003:1001:appadmin:/home/appadmin:/bin/bash
```

Let's add the user "appadmin" to the "admins" group (to create the "admins" group, see ["Group and User Settings"](/GuideRu/ConfigureGroupsAndUsers.md)).

Create a home directory and set a password for the new user:  
```bash
mkdir /home/appadmin
chown appadmin /home/appadmin
chmod 700 /home/appadmin
passwd appadmin
```

Create a directory "/var/log/sudo" with access rights of 750. In this directory, we will create the file "appadmin.log".

Run the following command:  
```bash
sudo visudo -f /etc/sudoers.d/appadmin
```

In the open file, we will configure logging of all commands in json format to the file "/var/log/sudo/appadmin.log":  
```bash
Defaults:appadmin logfile="/var/log/appadmin.log"
Defaults:appadmin log_format="json"
```

Now run the `sudo visudo` command and write an alias in it that will allow the user to use the 'systemctl' command:  
```bash
Cmnd_Alias SERVICE_CMD=/bin/systemctl
```

Using the command `sudo visudo -f /etc/sudoers.d/appadmin`, we return to the file to configure the rights for the user "appadmin" and connect our alias:  
```bash
appadmin ALL=(ALL:ALL) NOPASSWD:SERVICE_CMD
```

After saving, the message `Cmnd_Alias "SERVICE_CMD" referenced but not defined` may appear, then use the command `sudo -U appadmin -l` and if after `appadmin ALL=(ALL:ALL) NOPASSWD: if "/bin/systemctl" is located, then everything is fine :)

Let's make it so that the "appadmin" user can execute bash scripts that are located in the "/opt/scripts" directory. Run the command `sudo visudo` and write the following alias there:  
```bash
Cmnd_Alias BASH_USE=/usr/bin/bash /opt/scripts/*.bash
```

And in the file "/etc/sudoers.d/appadmin" we connect alias:  
```bash
appadmin ALL=(ALL:ALL) NOPASSWD:SETENV:SERVICE_CMD,BASH_USE
```

"SETENV" is needed so that scripts can be executed with the following command:  
```bash
sudo -u appadmin sudo LOGGEDUSER=appadmin bash /opt/scripts/access.bash
```

As we remember in the script "access.bash" has a variable "$LOGGEDUSER". If we hadn't used "LOGGEDUSER=appadmin", we wouldn't get the correct script output. "SETENV" allows us to do this.

We will prohibit the user "appadmin" from using the commands `sudo su` and `sudo -i'. `sudo visudo` and prescribe the alias:  
```bash
Cmnd_Alias FORBIDDEN_CMD=/bin/sudo su, /bin/sudo -i
```

And in the file "/etc/sudoers.d/appadmin" we connect alias:  
```bash
appadmin ALL=(ALL:ALL) !FORBIDDEN_CMD
```

We will prohibit the user from executing the system shell login commands in the "vim/less/more" utilities. `sudo visudo` and prescribe the alias:  
```bash
Cmnd_Alias EDITORS=/usr/bin/vim, /usr/bin/vim.tiny, /usr/bin/less, /usr/bin/more
```

And in the file "/etc/sudoers.d/appadmin" we connect alias:  
```bash
appadmin ALL=(ALL:ALL) !EDITORS
```

## 4. Checking the correctness of access

If you use the command `sudo visudo -c`, you have the following output:  
![{E56C0D7F-A772-4416-8882-82990764FC74}](https://github.com/user-attachments/assets/50441757-726f-49a4-8ee9-ad314a734941)

Then we use the command `sudo chmod 0440 /etc/sudoers.d/*`.
