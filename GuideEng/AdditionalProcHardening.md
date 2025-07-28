# Setting up additional process reinforcements
## 1. Random location of the address space
Set the following parameter to "/etc/sysctl.conf" or to the file in "/etc/sysctl.d/[filename].conf":  
```bash
printf "%s\n" "kernel.randomize_va_space = 2" >> /etc/sysctl.d/60-kernel_sysctl.conf
```

After that, run the following command to set the active kernel parameter:  
```bash
sysctl -w kernel.randomize_va_space=2
```

## 2. Restriction of "ptrace_scope"
Set the following parameter to "/etc/sysctl.conf" or to the file in "/etc/sysctl.d/[filename].conf":  
```bash
printf "%s\n" "kernel.yama.ptrace_scope = 1" >> /etc/sysctl.d/60-kernel_sysctl.conf
```

After that, run the following command to set the active kernel parameter:  
```bash
sysctl -w kernel.yama.ptrace_scope=1
```

## 3. Limiting memory dumps
