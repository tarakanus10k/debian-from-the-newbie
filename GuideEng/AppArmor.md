# Setting up AppArmor
## 1. Is AppArmor installed
Enter the following command to check if AppArmor is installed:  
```bash
dpkg-query -s apparmor &>/dev/null && echo "apparmor is installed"
```

If the output is "apparmor is installed", then AppArmor is installed.

Let's also check if ApppArmor utilities are installed.:  
```bash
dpkg-query -s apparmor-utils &>/dev/null && echo "apparmor-utils is installed"
```

If the output is "apparmor-utils is installed", then ApppArmor-utilities is installed. If the output is empty, then download the ApppArmor utilities with the command:  
```bash
apt install apparmor apparmor-utils
```

## 2. Is AppArmor enabled in the loader configuration?
Let's check that apparmor=1:  
```bash
grep "^\s*linux" /boot/grub/grub.cfg | grep -v "apparmor=1"
```

If there is a conclusion, then go to "/etc/default/grub" and add "apparmor=1":  
```bash
GRUB_CMDLINE_LINUX="apparmor=1"
```

Let's check that security=apparmor:  
```bash
grep "^\s*linux" /boot/grub/grub.cfg | grep -v "security=apparmor"
```

If there is a conclusion, then go to "/etc/default/grub" and add "security=apparmor":  
```bash
GRUB_CMDLINE_LINUX="ecurity=apparmor"
```

As a result, "GRUB_CMDLINE_LINUX" should look like this:  
```bash
GRUB_CMDLINE_LINUX="apparmor=1 security=apparmor"
```

Next, use the `update-grub` command to apply the changes.

## 3. Are they in a coercive or complaining mode
Let's check which profiles are uploaded and are in the forced or complaint mode.:  
```bash
apparmor_status | grep profiles
```

Let's check if there are unlimited processes.:  
```bash
apparmor_status | grep processes
```

Enter one of the following commands to set all profiles to coercion/complaint mode:  
- coercion:  
```bash
aa-enforce /etc/apparmor.d/*
```
- complaints:  
```bash
aa-complain /etc/apparmor.d/*
```
