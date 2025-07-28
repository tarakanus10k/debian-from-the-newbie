# Configuring PAM
## 1. Configuring the PAM module "pam_nologin"
If you want no one to connect via ssh (except root), then you must configure this module. Go to `/etc/pam.d/sshd` and check if the "pam_nologin" module is connected. The connected module should look something like this:
![{1A51B5CF-6111-453D-AE3F-56BE8AE044AB}](https://github.com/user-attachments/assets/a7b4d847-2f21-4dcf-ab76-b384d411a244)

In order for the module to start working, you need to create a "nologin" file in "/etc".

Restart sshd and you're done. If you want to terminate the module, then simply delete the "nologin" file.

##2. Configuring the pam_access module
Suppose there is a group with users and for this group it is necessary to prohibit the possibility of ssh connection. To do this, go to `/etc/pam.d/sshd` and connect the "pam_access" module:  
```bash
account required pam_access.so
```

Next, in '/etc/security/access.conf` we write the following:  
``bash
-:[band name]:ALL
``

The following entry indicates that all users of the group you specified will be denied access when attempting to connect via ssh.

Restart "sshd" so that the changes start working.

## 3. Setting up the pam_time PAM module

For example, we need the user "appadmin" (creating the user "appadmin" [here](/GuideRu/InstAndConfSudo.md)) to be unable to connect via ssh on weekends, and we will use the "pam_time" module for this task. To do this, go to `/etc/pam.d/sshd` and connect the "pam_time" module:  
```bash
account required pam_time.so
```

Next, in `/etc/security/time.conf` we write the following:  
```bash
sshd;*;appadmin;!SaSu0000-2400
```

The following entry indicates that ssh connection via any source is prohibited for the "appadmin" user on Saturday and Sunday from 00:00 to 24:00.

Restart "sshd" so that the changes start working.
