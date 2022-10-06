# In process
# Adding Users in Linux with Add Users Command 
Linux is a multi-user system, which means that more than one person can interact with the same system at the same time. As a system administrator, you have the responsibility to manage the system’s users and groups by creating and removing users and assign them to different groups .

## useradd Command
The general syntax for the useradd command is as follows:

```useradd [OPTIONS] USERNAME```

Only root or users with sudo privileges can use the useradd command to create new user accounts.

When invoked, useradd creates a new user account according to the options specified on the command line and the default values set in the `/etc/default/useradd` file.


The variables defined in this file differ from distribution to distribution, which causes the useradd command to produce different results on different systems.


useradd also reads the content of the `/etc/login.defs` file. This file contains configuration for the shadow password suite such as password expiration policy, ranges of user IDs used when creating system and regular users, and more.

How to Create a New User in Linux
To create a new user account, invoke the useradd command followed by the name of the user.

For example to create a new user named username you would run:

`sudo useradd username`  

When executed without any option, useradd creates a new user account using the default settings specified in the /etc/default/useradd file.
The command adds an entry to the /etc/passwd, /etc/shadow, /etc/group and /etc/gshadow files.

To be able to log in as the newly created user, you need to set the user password. To do that run the passwd command followed by the username:

`sudo passwd username`  

You will be prompted to enter and confirm the password. Make sure you use a strong password.

Changing password for user username.  
    ```New password:```  
    ```Retype new password:   ```  
```passwd: all authentication tokens updated successfully.```  

How to Add a New User and Create Home Directory
On most Linux distributions, when creating a new user account with useradd, the user’s home directory is not created.
Use the -m (--create-home) option to create the user home directory as /home/username:

```sudo useradd -m username```

The command above creates the new user’s home directory and copies files from /etc/skel directory to the user’s home directory. If you list the files in the /home/username directory, you will see the initialization files:

```ls -la /home/username/``

```drwxr-xr-x 2 username username 4096 Dec 11 11:23 .```  
```drwxr-xr-x 4 root     root     4096 Dec 11 11:23 ..```  
```-rw-r--r-- 1 username username  220 Apr  4  2018 .bash_logout``` 
```-rw-r--r-- 1 username username 3771 Apr  4  2018 .bashrc```
```-rw-r--r-- 1 username username  807 Apr  4  2018 .profile```

Within the home directory, the user can write, edit and delete files and directories.


Creating a User with Specific Home Directory
By default useradd creates the user’s home directory in /home. If you want to create the user’s home directory in other location, use the d (--home) option.

Here is an example showing how to create a new user named username with a home directory of /opt/username:

`sudo useradd -m -d /opt/username username`

Creating a User with Specific User ID
In Linux and Unix-like operating systems, users are identified by unique UID and username.


User identifier (UID) is a unique positive integer assigned by the Linux system to each user. The UID and other access control policies are used to determine the types of actions a user can perform on system resources.

By default, when a new user is created, the system assigns the next available UID from the range of user IDs specified in the login.defs file.


Invoke useradd with the -u (--uid) option to create a user with a specific UID. For example to create a new user named username with UID of 1500 you would type:


`sudo useradd -u 1500 username`

You can verify the user’s UID, using the id command:

`id -u username 1500`

Creating a User with Specific Group ID
Linux groups are organization units that are used to organize and administer user accounts in Linux. The primary purpose of groups is to define a set of privileges such as reading, writing, or executing permission for a given resource that can be shared among the users within the group.

When creating a new user, the default behavior of the useradd command is to create a group with the same name as the username, and same GID as UID.

The -g (--gid) option allows you to create a user with a specific initial login group. You can specify either the group name or the GID number. The group name or GID must already exist.
The following example shows how to create a new user named username and set the login group to users type:

`sudo useradd -g users username`

To verify the user’s GID, use the id command:

`id -gn username users`

Creating a User and Assign Multiple Groups
There are two types of groups in Linux operating systems Primary group and Secondary (or supplementary) group. Each user can belong to exactly one primary group and zero or more secondary groups.

You to specify a list of supplementary groups which the user will be a member of with the -G (--groups) option.

The following command creates a new user named username with primary group users and secondary groups wheel and docker.


`sudo useradd -g users -G wheel,developers username`

You can check the user groups by typing

`id username`

```uid=1002(username) gid=100(users) groups=100(users),10(wheel),993(docker)```

Creating a User with Specific Login Shell
By default, the new user’s login shell is set to the one specified in the /etc/default/useradd file. In some distributions the default shell is set to /bin/sh while in others it is set to /bin/bash.

The -s (--shell) option allows you to specify the new user’s login shell.

For example, to create a new user named username with /usr/bin/zsh as a login shell type:

`sudo useradd -s /usr/bin/zsh username`

Check the user entry in the /etc/passwd file to verify the user’s login shell:

`grep username /etc/passwd`

```username:x :1001:1001::/home/username:/usr/bin/zsh```

Creating a User with Custom Comment
The -c (--comment) option allows you to add a short description for the new user. Typically the user’s full name or the contact information are added as a comment.

In the following example, we are creating a new user named username with text string Test User Account as a comment:

```sudo useradd -c "Test User Account" username```

The comment is saved in /etc/passwd file:

`grep username /etc/passwd`

```username:x :1001:1001:Test User Account:/home/username:/bin/sh```  

The comment field is also known as GECOS.

Creating a User with an Expiry Date
To define a time at which the new user accounts will expire, use the -e (--expiredate) option. This is useful for creating temporary accounts.

The date must be specified using the YYYY-MM-DD format.

For example to create a new user account named username with an expiry time set to January 22 2019 you would run:

`sudo useradd -e 2019-01-22 username`

Use the chage command to verify the user account expiry date:

`sudo chage -l username`

The output will look something like this:

```Last password change					: Dec 11, 2018```
```Password expires					: never```
```Password inactive					: never```
```Account expires						: Jan 22, 2019```
```Minimum number of days between password change		: 0``
```Maximum number of days between password change		: 99999```
```Number of days of warning before password expires	: 7```

Creating a System User
There is no real technical difference between the system and regular (normal) users. Typically system users are created when installing the OS and new packages.

Use the -r (--system) option to create a system user account. For example, to create a new system user named username you would run:

`sudo useradd -r username`

System users are created with no expiry date. Their UIDs are chosen from the range of system user IDs specified in the login.defs file, which is different than the range used for normal users.


Changing the Default useradd Values
The default useradd options can be viewed and changed using the -D, --defaults option, or by manually editing the values in the /etc/default/useradd file.

To view the current default options type:

`useradd -D`

The output will look something like this:

```GROUP=100```  
```HOME=/home```  
```INACTIVE=-1```  
```EXPIRE=```  
```SHELL=/bin/sh```  
```SKEL=/etc/skel```  
```CREATE_MAIL_SPOOL=no```

Let’s say you want to change the default login shell from /bin/sh to /bin/bash. To do that, specify the new shell as shown below:

`sudo useradd -D -s /bin/bash`

You can verify that the default shell value is changed by running the following command:

`sudo useradd -D | grep -i shell`

```SHELL=/bin/bash```