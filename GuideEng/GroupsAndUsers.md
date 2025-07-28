# === Setting up groups and users ===
##1. Creating groups
To create groups, open the "group" file using the `nano /etc/group` command. At the end of the file we write `admins:x:1001:`. Let's go through this entry in more detail.:
- admins: group name
- x: password (no password specified)
- 1001: GID (unique numeric group identifier)
- After the GID, the users who belong to this group are indicated (there are no users in this group yet)

## 2. Creating Users
To create users, open the "passwd" file using the `nano /etc/passwd` command. Create a user by writing `viromant' to the end of the file.:x:1001:1001:x:/home/viromant:/bin/bash`. Let's go through this entry in more detail.:
- viromant: user name (if anything, the user name is random and unrelated to nothing)
- x: password (password not specified)
- 1001: UID (unique numeric user ID)
- 1001: GID (ID of the main user group)
- x: additional information (for example, phone number or full name)
- /home/viromant: The path to the user's home directory
- /bin/bash: A shell that starts when you log in

Let's add a new user to the "admins" group. To do this, change the string `admins:x:1001:` on `admins:x:1001:viromant`.

Creating a home directory for the new user:
```bash
mkdir /home/viromant
chown viromant /home/viromant 
chmod 700 /home/viromant
```

Setting the password for the new user:
![{367266A1-B71F-4B25-98CF-17F720526710}](https://github.com/user-attachments/assets/074f65f9-0c5c-4b5d-999a-3f2e13aaacd1)

#3. Creating the "script-runners" group and the "script-runner" user
Let's create the "script-runners" group in the same way as the "admins" group:
``bash
script-runners:x:1002:
``

Now let's create the "script-runner" user in the same way as the "viromant" user, but change the home directory for the new user.:
```bash
script-runner:x:1002:1002:x:/opt/scripts:/bin/bash
```

Adding a new user to the "script-runners" group.

Creating a home directory for the new user:
```bash
mkdir /opt/scripts
chown script-runner:script-runners /opt/scripts
chmod 750 /opt/scripts
```

Setting a password for the new user:  
![{1EF7688C-7736-4690-B8E5-B57D4D960012}](https://github.com/user-attachments/assets/28c330e2-b628-43dd-9ed7-c00de6daf654)
