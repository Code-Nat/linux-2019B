
### Permissions
* The Unix-like operating systems, such as Linux differ from other computing systems in that they are not only multitasking but also multi-user.
* Users
    * Every user of the system is assigned a unique User ID number (uid) 
    * User names and uid are stored in `/etc/passwd`
    * User names map to user ID numbers
    * To change your password, run `passwd`. Insecure passwords are rejected
    * User are assigned a home directory and a program that is run when they log in (usually shell)
    * Users cannot read, write or execute each other's files without  permission
* Groups
    * User’s are assigned to groups with unique group ID number (gid)
    * gids are stored in `/etc/group`
    * Group names map to group ID numbers 
    * Each user is given their own private group
    * They can also be added to other groups to gain additional access
    * All users in a group can share files that belong to the group
* Root user
    * The root user: a special administrative account
    * Sometimes called the superuser
    * root has complete control over the system
    * An unlimited capacity to damage the system!
    * You should not log in as root without a very good reason
    * Normal (“unprivileged”) users potential to do damage is limited
    * Server programs such as web or print servers typically run as unprivileged users, not as root (Examples: mail, lp) - Running programs in this way limits the amount of damage any single program can do to the system
    * Becoming The Superuser For A Short While - It is often necessary to become the superuser to perform important system administration tasks, but as you have been warned, you should not stay logged in as the superuser. In most distributions, there is a program that can give you temporary access to the superuser's privileges. This program is called su (short for substitute user) and can be used in those cases when you need to be the superuser for a small number of tasks. To become the superuser, simply type the su command. You will be prompted for the superuser's password. After executing the su command, you have a new shell session as the superuser. To exit the superuser session, type exit and you will return to your previous session.
* related Commands:
    * Find the gid and uid:
    ```bash
    anna@HP-Printer:~$ id
    uid=1000(anna) gid=1000(anna) groups=1000(anna),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
    anna@HP-Printer:~$ 
    ```
    * Find out who you are
    ```bash
    anna@HP-Printer:~$ whoami
    anna
    ```
     * Find out what groups you belong to
    ```bash
    anna@HP-Printer:~$ groups
    anna adm cdrom sudo dip plugdev lpadmin sambashare
    ```
     * Find out who is logged in 
    ```bash
    anna@HP-Printer:~$ users    #first way
    anna anna
    anna@HP-Printer:~$ who      #second way
    anna     :0           2019-01-12 09:33 (:0)
    anna     pts/0        2019-01-12 10:11 (H)
    anna@HP-Printer:~$ w        #third way
    10:44:06 up  1:10,  2 users,  load average: 0.36, 0.55, 0.61
    USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
    anna     :0       :0               09:33   ?xdm?   9:10   0.00s /usr/lib/gdm3/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu gnome-session --session=ubuntu
    anna     pts/0    H                10:11    6.00s  0.05s  0.01s w
    ```
     * Login / reboot history  
    ```bash
    anna@HP-Printer:~$ last
    anna     pts/0        H                Sat Jan 12 10:11   still logged in
    reboot   system boot  4.15.0-43-generi Sat Jan 12 09:33   still running

    wtmp begins Tue Jan  1 08:50:52 2019
    ```
* The Linux Security Model
    * Users and groups are used to control access to files and resources
    * Users log in to the system by supplying their user name and password
    * Every file on the system is owned by a user and associated with a group
    * Every process has an owner and group affiliation , and can only access the resources its owner or group  can access 
#### Linux File Security
* Every file and directory has permission set that determine who can access it
* Permission are set for:
    * The owner of the file (called “user”)
    * The group members
    * All others
* Permissions that are set are called read, write and execute permissions 
#### Linux Process Security
* When a process accesses a file the user and group of the process are compared with the user and group of the file
    * If the user matches, the user permissions apply
    * If the group matches, but the user doesn’t, the group permissions apply
    * If neither match, the other permission apply
* File permissions may be viewed using 
    ```bash
    anna@HP-Printer:~$ ls -l /bin/login
    -rwxr-xr-x 1 root root 52664 Jan 25  2018 /bin/login
    ```
This output shows the follwing details:
* The file "/bin/login" is owned by user "root"
* The superuser has the right to read, write, and execute this file
* The file is owned by the group "root"
* Members of the group "root" can also read and execute this file
* Everybody else can read and execute this file
* In the `-rwxr-xr-x`, we see how the first portion of the listing is interpreted. It consists of a character indicating the file type (`-` in our case), followed by three sets of three characters that convey the reading, writing and execution permission for the owner (`rwx` in our case), group (`r-x` in our case), and everybody else (`r-x` in our case).
* File permissions are established for each of three user categories. Each category also has a one-letter symbol:
    * `u` - the file’s owners (user)
    * `g` - other users in the file’s group
    * `o` - everyone else (others)
* Four symbols are used when displaying permission:
    * `r` - permission to read a file or list a directory’s content
    * `w` - permission to write to a file or create, rename and remove files from a directory
    * `x` -  permission to execute a program file or change into a directory and do long listing of the directory (for example: if we don't have a `x` to a folder - we can't run `cd` to this folder)
    * `-` -  no permission (in place of the r, w, or  x)

### chmod
* The chmod command is used to change the permissions of a file or directory. 
* To use it, you specify the desired permission settings and the file or files that you wish to modify. 
* There are two ways to specify the permissions:
    * octal notation method
    * char notation method
* octal notation method
    * It is easy to think of the permission settings as a series of bits (which is how the computer thinks about them). 
    * Here's how it works:
    ```
    rwx rwx rwx = 111 111 111
    rw- rw- rw- = 110 110 110
    rwx --- --- = 111 000 000
    ```
    * The bits are translated to decimal base:
    ```
    rwx = 111 in binary = 7
    rw- = 110 in binary = 6
    r-x = 101 in binary = 5
    r-- = 100 in binary = 4
    ```
    * Now, if you represent each of the three sets of permissions (owner, group, and other) as a single digit
    * For example, if we wanted to set some_file to have read and write permission for the owner, but wanted to keep the file private from others, we would:
    ```bash
    anna@HP-Printer:~$ touch w.txt
    anna@HP-Printer:~$ ls -l w.txt
    -r--r--r-- 1 anna anna 0 Jan 12 11:48 w.txt
    anna@HP-Printer:~$ chmod 777 w.txt
    anna@HP-Printer:~$ ls -l w.txt
    -rwxrwxrwx 1 anna anna 0 Jan 12 11:48 w.txt
    ```
* char notation method

* Special permissions - a fourth permission set (in addition to user/group/other),Applicable in four cases:
    * SUID (set user ID) for an executable, Processes are granted access to system resources based on user who owns the file.
        * When you login, your login shell process’ values are your user ID and group ID
        * E.g., if you run passwd (owned by root), THE user ID is your ID, not root; 
        * how can it update /etc/passwd file owned by root ? SUID bit enables this functionality
        * When an executable file with set user ID (SUID) permission is executed, command run with permission of the owner of the command, not executor of the command 
    * SGID (set group ID) for and executable, Same with SUID except group is affected.
    * SGID a directory:  Files created in that directory will have their group set to the directory's group.
    * Sticky bit for a directory, If set on a directory, then a user may only delete files that he owns or for which he has explicit write permission granted, even when he has write access to the directory. (e.g. /tmp )
    * For example:
    ```bash
    anna@HP-Printer:~$ touch x.txt
    anna@HP-Printer:~$ ls -l x.txt
    -r--r--r-- 1 anna anna 0 Jan 12 11:49 x.txt
    anna@HP-Printer:~$ chmod 7777 x.txt
    anna@HP-Printer:~$ ls -l x.txt
    -rwsrwsrwt 1 anna anna 0 Jan 12 11:49 x.txt
    ```

### umask
umask - set file mode creation mask
* The default permissions are:  0666
* Then we use the `not`(`~`) umask value with an `And`(`&`) operator. for example: 0666 & ~022 = 0644
```bash
anna@HP-Printer:~$ touch a.txt      # create a new file - will get the umask permissions
anna@HP-Printer:~$ ls -l ?.txt      # view the permissions of all files that start with 1 char and continue with ".txt"
-rw-rw-r-- 1 anna anna 5 Jan 12 11:23 a.txt
anna@HP-Printer:~$ umask            # get the current umask (this is the default value)
0002
anna@HP-Printer:~$ umask 222        # set the value of the umask  
anna@HP-Printer:~$ touch z.txt      # create a new file - will get the umask permissions
anna@HP-Printer:~$ ls -l ?.txt      # view the permissions of all files that start with 1 char and continue with ".txt"
-rw-rw-r-- 1 anna anna 5 Jan 12 11:23 a.txt
-r--r--r-- 1 anna anna 0 Jan 12 11:24 z.txt
```




Changing File Ownership
You can change the owner of a file by using the chown command. Here's an example: Suppose I wanted to change the owner of some_file from "me" to "you". I could:

[me@linuxbox me]$ su
Password:
[root@linuxbox me]# chown you some_file
[root@linuxbox me]# exit
[me@linuxbox me]$
Notice that in order to change the owner of a file, you must be the superuser. To do this, our example employed the su command, then we executed chown, and finally we typed exit to return to our previous session.

chown works the same way on directories as it does on files.

Changing Group Ownership
The group ownership of a file or directory may be changed with chgrp. This command is used like this:

[me@linuxbox me]$ chgrp new_group some_file
In the example above, we changed the group ownership of some_file from its previous group to "new_group". You must be the owner of the file or directory to perform a chgrp.




### Grep
* grep comes from the ed search command `global regular expression print`
* This was such a useful command that it was written as a standalone utility
* There are two other variants, egrep and fgrep that comprise the grep family
    * grep - uses regular expressions for pattern matching
    * fgrep - file grep, does not use regular expressions, only matches fixed strings but can get search strings from a file
    * egrep - exponential grep, uses a more powerful set of regular expressions
Syntax
grep [-hilnw] [-e expression] [filename]
egrep [-hiln] [-e expression] [-f filename] [expression] [filename]
fgrep [-hilnx] [-e string] [-f filename] [string] [filename]
-h - Do not display filenames
-i  - Ignore case
-l  - List only filenames containing matching lines
-n - Precede each matching line with its line number
-w - Search for the expression as a word (grep only)
-x - Match whole line only (fgrep only)




### SYNOPSIS
* `grep [OPTIONS] PATTERN [FILE...]` - we can pass several files
    * we can use pipe in order to send to grep the file content (then we dont need to pass to grep the file name as a parameter).   
    for example:
    ```bash
    anna@HP-Printer:~/Desktop$ echo "abcd" | grep "a"
    abcd
    ```
    or: 
    ```bash
    anna@HP-Printer:~/Desktop$ echo "abcd" > a.txt
    anna@HP-Printer:~/Desktop$ cat a.txt
    abcd
    anna@HP-Printer:~/Desktop$ cat a.txt | grep "a"
    abcd
    ```
    * we can use only grep command - and then we will send a file (or several files).
    for example:
    ```bash
    anna@HP-Printer:~/Desktop$ echo "abcd" > a.txt
    anna@HP-Printer:~/Desktop$ cat a.txt
    abcd
    anna@HP-Printer:~/Desktop$ grep "a" a.txt
    abcd
    anna@HP-Printer:~/Desktop$ 
    ```
* `grep [OPTIONS] -e PATTERN ... [FILE...]` - with `-e` param - we can pass several patterns
    for examle:

    ```bash
    grep -e ab -e cf  #find all matching to "ab" or to "cf"
    ```
           -e PATTERN, --regexp=PATTERN
              Use PATTERN as the pattern.  If this option is used multiple times or is combined with the -f (--file) option, search for all patterns given.  This option can be used  to  protect  a  pattern
              beginning with “-”.


* `grep [OPTIONS] -f FILE ... [FILE...]` - with `-f` param - we must send at least 1 file.
    the `-f` option is to obtain  patterns  from  FILE,  one  per line.  If this option is used multiple times or is combined with the -e (--regexp) option, search for all patterns given.  The empty file contains zero patterns, and therefore matches nothing.

    for example:
    ```bash
    anna@HP-Printer:~/Desktop$ echo "abcd" > a.txt
    anna@HP-Printer:~/Desktop$ cat a.txt
    abcd
    anna@HP-Printer:~/Desktop$ echo "abcdefg" > b.txt
    anna@HP-Printer:~/Desktop$ cat b.txt
    abcdefg
    anna@HP-Printer:~/Desktop$ grep -f a.txt b.txt
    abcdefg
    anna@HP-Printer:~/Desktop$ grep -f b.txt a.txt
    ```


 find ~ -type f -name ".*"

### Sort
To  sort file on the basis of 2nd field , numerically: 


sort -t"," -k2n,2 file

### find

### wc

### tr

TODO-START
### write into files 
* `echo -e "/n/n" > a.txt`
* `echo -e "/n/n" >> a.txt`
### locate + updatedb
### ext-undelete
TODO-END

