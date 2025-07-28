# Installing and configuring Auditd
## 1. Installing Auditd
Install "Auditd" with the command `apt install auditd`

## 2. Setting up Auditd

### 2.1 File monitoring rule "/etc/passwd", "/etc/shadow", "/etc/sudoers", "/etc/sudoers.d"
Create the rules as follows:  
```bash
auditctl -w /etc/passwd -p wa -k soc_passwd_rule
auditctl -w /etc/shadow -p wa -k soc_shadow_rule
auditctl -w /etc/sudoers -p wa -k soc_sudoers_rule
auditctl -w /etc/sudoers.d -p wa -k soc_sudoers_rule
```

Let's look at it in more detail:
- -w: specify the path to the monitoring file.
- -p wa: specify the access rights (w - record, a - change attributes).
- -k: we set the key for log filtering.

###2.2 Rule for monitoring the execution of the python interpreter
The rule is created as follows:  
```bash
auditctl -a always,exit -F arch=b32 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
```

Let's look at it in more detail:
- -a always,exit: always - always register an event, exit - catch the completion of a system call.
- -F arch=b32/64: filter for 64-bit systems.
- -S execve: monitors the "execve()" call.
- -F exe=/usr/bin/python3: the path to the executable file.

### 2.3 Rule for monitoring sudo usage
This rule will track the execution of programs using the UID (for example, the execution of programs via sudo).

The rule is created as follows:  
```bash
auditctl -a always,exit -F arch=b32 -C euid!=uid -F auid!=unset -S execve -k user_emul
auditctl -a always,exit -F arch=b64 -C euid!=uid -F auid!=unset -S execve -k user_emul
```

Let's look at it in more detail:
- -C euid!=uid: filter cases where the effective UID is not equal to the real UID
- -F auid!=unset: ignore processes without UID audit

### 2.4 Rules for monitoring time changes
The rules are created as follows:  
```bash
auditctl -a always,exit -F arch=b32 -S adjtimex,settimeofday -k time_change 
auditctl -a always,exit -F arch=b64 -S adjtimex,settimeofday -k time_change 
auditctl -a always,exit -F arch=b32 -S clock_settime -F a0=0x0 -k time_change 
auditctl -a always,exit -F arch=b64 -S clock_settime -F a0=0x0 -k time_change 
auditctl -w /etc/localtime -p wa -k time-change
```

## 3. Saving the rules
First, let's use the `auditctl -l` command to display all the created rules. The conclusion should be something like this:  
```bash
-w /etc/passwd -p wa -k soc_passwd_rule
-w /etc/shadow -p wa -k soc_shadow_rule
-w /etc/sudoers -p wa -k soc_sudoers_rule
-w /etc/sudoers.d -p wa -k soc_sudoers_rule
-a always,exit -F arch=b32 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
-a always,exit -F arch=b64 -S execve -F exe=/usr/bin/python3 -k python_exec_rule
-a always,exit -F arch=b32 -C euid!=uid -F auid!=unset -S execve -k user_emul
-a always,exit -F arch=b64 -C euid!=uid -F auid!=unset -S execve -k user_emul
-a always,exit -F arch=b32 -S adjtimex,settimeofday -k time_change 
-a always,exit -F arch=b64 -S adjtimex,settimeofday -k time_change 
-a always,exit -F arch=b32 -S clock_settime -F a0=0x0 -k time_change 
-a always,exit -F arch=b64 -S clock_settime -F a0=0x0 -k time_change 
-w /etc/localtime -p wa -k time-change
```

We will record files as follows:  
```bash
bash -c 'auditctl -l | head -n 4 > /etc/audit/rules.d/file-watch-rules.rules'
bash -c 'auditctl -l | sed -n 5,6p > /etc/audit/rules.d/python-exec-rules.rules'
bash -c 'auditctl -l | sed -n 7,8p > /etc/audit/rules.d/uid-change-rules.rules'
bash -c 'auditctl -l | tail -n 5 > /etc/audit/rules.d/time-change-rules.rules'
```

Restart "auditd` with the command `systemctl restart auditd'. Next, we repeat the `auditctl -l` command and if the output is identical, then everything is done correctly.
