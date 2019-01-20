### tab key
* Type TAB key to complete command line: 
    * For the command name, it will complete a command name
    * For an argument, it will complete a file name 


### wildcard
 * `*`   matches zero or more characters
 * `?`   matches any single character
 * `[a-z]`  matches a range of characters  
 * `[^a-z]` matches all except the range



### ls
ls -  list directory contents
* Syntax 
   ```bash
   ls   [options]                               # show all directory contents
   ```
   or
      
   ```bash
   ls   [options]   wanted-path                 # show the directory contents of the given path
   ```
   or
   ```bash
   ls   [options]   regex-to-choose-files       # show all the regex matching contents in the directory 
   ```

### Change current user to `root`
```bash
anna@HP-Printer:/$ sudo i
```
NOTE:
* In `root` mode - the `$` in the prompt - changes to `#`
* To exit `root` mode - press `contreol+d` or type `exit`
```bash
anna@HP-Printer:/$ sudo i
[sudo] password for anna: 
sudo: i: command not found
anna@HP-Printer:/$ sudo -i
root@HP-Printer:~# pwd
/root
root@HP-Printer:~# exit
logout

```


### PS1 - Change the prefix in the prompt
PS1 - The value of this parameter is  used as the primary prompt string.
```bash
anna@HP-Printer:/$ echo $PS1
\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$
anna@HP-Printer:/$ echo $(whoami)
anna
anna@HP-Printer:/$ PS1=test
test
```
* To exit this mode - type `exit`

### pwd
pwd - print name of current/working directory
```bash
anna@HP-Printer:~$ pwd
/home/anna
```
* `pwd` uses under the hood the `env` variable:
```bash
anna@HP-Printer:~$ env|grep PWD
PWD=/home/anna
```

### relative pathnames
* Specifies  location relative to your current working directory
* Relative pathnames do not begin with a `/`
* It is optional to add to the start of a Relative pathnames:  `./` (best practice)

```bash
anna@HP-Printer:~$ mkdir test
anna@HP-Printer:~$ cd test
anna@HP-Printer:~/test$ ls -a
.  ..
```
* `.` - is current directory
* `..` - is one directory backwards


### Home directory
two ways to get the home directory:
```bash
anna@HP-Printer:/home$ echo ~
/home/anna
anna@HP-Printer:/home$ echo $HOME
/home/anna
```

### cd
cd - Change the shell working directory.
* `cd` Change the shell working directory to the home directory iof the current user
```bash
anna@HP-Printer:/home$ cd
anna@HP-Printer:~$ 
```
* To auto complete all the options in the current directory:
```bash
anna@HP-Printer:/home$ cd ../    # press tab+tab 
bin/        cdrom/      etc/        lib/        lost+found/ mnt/        proc/       run/        snap/       sys/        usr/        boot/       dev/        home/       lib64/      media/      opt/        root/       sbin/       srv/        tmp/        var/ 

anna@HP-Printer:~/test$ cd ../D  # press tab+tab
Desktop/   Documents/ Downloads/ 
```

* To move back to the last directory that we used:
```bash
anna@HP-Printer:/home$ cd -
/home/anna
anna@HP-Printer:~$ cd -
/home
anna@HP-Printer:/home$ cd -
/home/anna
```
under the hood, it uses the `env` variable:
```bash
anna@HP-Printer:~$ env| grep OLDPWD
OLDPWD=/home
anna@HP-Printer:~$ pwd
/home/anna
anna@HP-Printer:~$ cd $OLDPWD
anna@HP-Printer:/home$ pwd
/home
```

### mkdir  
mkdir  – make a directory
```bash
anna@HP-Printer:~/Desktop$ ls             # no content in this directory
anna@HP-Printer:~/Desktop$ mkdir test     # create new directory in this directory
anna@HP-Printer:~/Desktop$ ls
test
```

###  rmdir   
rmdir – remove an empty directory
```bash
anna@HP-Printer:~/Desktop$ mkdir test      # create new directory in this directory 
anna@HP-Printer:~/Desktop$ ls
test
anna@HP-Printer:~/Desktop$ rmdir test      # remove the directory test (empty directory)
anna@HP-Printer:~/Desktop$ ls              # no content in this directory
```

### touch
touch  – create empty files or change file timestamps (if file exists)
```bash
anna@HP-Printer:~/Desktop$ ls -l           # no content in this directory
anna@HP-Printer:~/Desktop$ touch a.txt
anna@HP-Printer:~/Desktop$ ls -l           # create new file in this directory
-rw-rw-r-- 1 anna anna 0 Jan  5 11:10 a.txt
anna@HP-Printer:~/Desktop$ touch a.txt     # update the timestamp of the existing file 
anna@HP-Printer:~/Desktop$ ls -l
-rw-rw-r-- 1 anna anna 0 Jan  5 11:11 a.txt
```

### cp
cp - copy files and directories
* If the destination exists and is a directory, the copy is placed there with the same name
* If the destination exist and is a file, the copy overwrites the destination file 
* If the destination does not exist, the copy is created with that name
```bash
anna@HP-Printer:~$ mkdir testing
anna@HP-Printer:~$ cd testing
anna@HP-Printer:~/testing$ touch a.txt
anna@HP-Printer:~/testing$ echo "I love linux">a.txt
anna@HP-Printer:~/testing$ cat a.txt
I love linux
anna@HP-Printer:~/testing$ cp a.txt ../Desktop/
anna@HP-Printer:~/testing$ cd ../Desktop/
anna@HP-Printer:~/Desktop$ tree
.
├── a.txt   
anna@HP-Printer:~/Desktop$ cp ../testing ../Desktop/ -r  #-r is to copy directory 
anna@HP-Printer:~/Desktop$ tree
.
├── a.txt
└── testing
    └── a.txt

```


### mv
mv - move (rename) files
* rm    [options]   filenames
    * -i	interactive 
    * -r	recursive 
    * -f	force 
```bash
anna@HP-Printer:~$ mkdir testmv
anna@HP-Printer:~$ cd testmv
anna@HP-Printer:~/testmv$ echo "test 1">>a.txt
anna@HP-Printer:~/testmv$ echo "test 2">>b.txt
anna@HP-Printer:~/testmv$ tree
.
├── a.txt
└── b.txt

0 directories, 2 files
anna@HP-Printer:~/testmv$ mv a.txt ../Desktop/
anna@HP-Printer:~/testmv$ tree
.
└── b.txt

0 directories, 1 file
anna@HP-Printer:~/testmv$ ls ../Desktop/
a.txt
anna@HP-Printer:~/testmv$ cd ..
anna@HP-Printer:~$ mv testmv/ Desktop/
anna@HP-Printer:~$ tree Desktop/
Desktop/
├── a.txt
└── testmv
    └── b.txt

```
### rm
rm - remove files or directories
* Move file and folder:
```bash
anna@HP-Printer:~$ mkdir testrm
anna@HP-Printer:~$ cd testrm
anna@HP-Printer:~/testrm$ echo "test 1">>a.txt
anna@HP-Printer:~/testrm$ echo "test 2">>b.txt
anna@HP-Printer:~/testrm$ echo "test 3">>c.txt
anna@HP-Printer:~/testrm$ tree
.
├── a.txt
├── b.txt
└── c.txt

0 directories, 3 files

anna@HP-Printer:~/testrm$ rm  c.txt
anna@HP-Printer:~/testrm$ tree
.
├── a.txt
└── b.txt

0 directories, 2 files
anna@HP-Printer:~/testrm$ cd ..
anna@HP-Printer:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  snap  Templates  Videos testrm
anna@HP-Printer:~$ rm -r testrm  # -r - to remove directory with content
anna@HP-Printer:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  snap  Templates  Videos

```
* Rename file and folder:
```
anna@HP-Printer:~/Desktop$ tree
.
├── a.txt
└── testmv
    └── b.txt
anna@HP-Printer:~/Desktop$ mv a.txt aa.txt
anna@HP-Printer:~/Desktop$ tree
.
├── aa.txt
└── testmv
    └── b.txt

3 directories, 5 files
anna@HP-Printer:~/Desktop$ mv testmv/ t
anna@HP-Printer:~/Desktop$ tree
.
├── aa.txt
├── t
│   └── b.txt
```
* Move multiple files with one command:
```bash
anna@HP-Printer:~/Desktop$ tree
.
├── aa.txt
├── t
│   └── b.txt

anna@HP-Printer:~/Desktop$ cd t
anna@HP-Printer:~/Desktop/t$ tree
.
└── b.txt

0 directories, 1 files
anna@HP-Printer:~/Desktop/t$ echo "test 1">>a.txt
anna@HP-Printer:~/Desktop/t$ tree
.
├── a.txt
└── b.txt

0 directories, 2 files
anna@HP-Printer:~/Desktop/t$ mv a.txt b.txt ../
anna@HP-Printer:~/Desktop/t$ tree
.
0 directories, 0 files
anna@HP-Printer:~/Desktop/t$ tree ../
../
├── aa.txt
├── a.txt
├── b.txt
├── t

```

### file
file - determine file type
* Syntax 
   ```
   file   [options]   filename (s)
   ```
   or
   ```
   file   [options]   regex-to-choose-files
   ```

* View file type
```bash
anna@HP-Printer:~/Desktop$ echo '#!/bin/bash' > file.sh
anna@HP-Printer:~/Desktop$ cat file.sh 
#!/bin/bash
anna@HP-Printer:~/Desktop$ echo '#!/bin/bash' > file.py
anna@HP-Printer:~/Desktop$ cat file.py
#!/bin/bash
anna@HP-Printer:~/Desktop$ file *
file.py: Bourne-Again shell script, ASCII text executable
file.sh: Bourne-Again shell script, ASCII text executable
anna@HP-Printer:~/Desktop$ mv file.py file1
anna@HP-Printer:~/Desktop$ file *
file1:   Bourne-Again shell script, ASCII text executable
file.sh: Bourne-Again shell script, ASCII text executable
anna@HP-Printer:~/Desktop$ echo 'hello' > file.js
anna@HP-Printer:~/Desktop$ cat file.js
hello
anna@HP-Printer:~/Desktop$ file *
file1:   Bourne-Again shell script, ASCII text executable
file.js: ASCII text
file.sh: Bourne-Again shell script, ASCII text executable
anna@HP-Printer:~/Desktop$ echo '<html></html>' > file.txt
anna@HP-Printer:~/Desktop$ file *
file1:    Bourne-Again shell script, ASCII text executable
file.js:  ASCII text
file.sh:  Bourne-Again shell script, ASCII text executable
file.txt: HTML document, ASCII text
```
* View hidden file type
```bash
anna@HP-Printer:~/Desktop$ echo 'hello' > .file.html
anna@HP-Printer:~/Desktop$ cat .file.html 
hello
anna@HP-Printer:~/Desktop$ file .*
.:          directory
..:         directory
.file.html: ASCII text
```


### cat and tac
* cat - concatenate files and print on the standard output
* tac- concatenate and print files in reverse
```bash
anna@HP-Printer:~/Desktop$ echo "line1">>b.txt
anna@HP-Printer:~/Desktop$ echo "line2">>b.txt
anna@HP-Printer:~/Desktop$ echo "line3">>b.txt
anna@HP-Printer:~/Desktop$ cat b.txt 
line1
line2
line3
anna@HP-Printer:~/Desktop/t$ tac b.txt 
line3
line2
line1

```
* Note: you can create a new file and write into it with the `cat` command:
```bash
anna@HP-Printer:~$ cat > first
echo "hello"                    # Press Ctrl + D to save and exit write mode
anna@HP-Printer:~$ cat first
echo "hello"
```
### eval
eval- Execute arguments as a shell command.
```bash
anna@HP-Printer:~/Desktop/t$ echo ls
ls
anna@HP-Printer:~/Desktop/t$ eval ls
a.txt  b.txt  file1  file.js  file.sh  file.txt
```

### bash history
bash stores a history of commands you’ve entered, which can be used to repeat commands
* Use the up and down arrow keys to scroll through previous commands
* Type `CTRL+R` to search for  a command in command history 
```bash
anna@HP-Printer:~/Desktop$ # press CTRL+R
(reverse-i-search):
# now start to type your command - and you will get the auto-completetation of the previous command (reverse search - from the latest to the first)

# if you press tab - this will add the current text to the prompt for editing
# if you press enter - this will run the current text
```
* To recall last argument from previous command:
   `ESC + .`  Or   `ALT + .`
* Use history command to see a list of “remembered” commands: 
    ```bash
    anna@HP-Printer:~/Desktop$ history   # Display or manipulate the history list
    ```
* Use bang character !
    * !x  execute last command begin with x
    * !2  execute  command no 2
    * !!  execute the last command again
        ```bash
        anna@HP-Printer:~/Desktop$ echo "hello"
        hello
        anna@HP-Printer:~/Desktop$ !!
        echo "hello"
        hello
        ```


### Rules for Naming variable name 
* Variable name must begin with Alphanumeric character or underscore character (`_`), followed by one or more Alphanumeric character. 
* Don't put spaces on either side of the equal sign when assigning value to variable. 
* Variables are case-sensitive
* You can define NULL variable as follows (NULL variable is variable which has no value at the time of definition):
```bash
anna@HP-Printer:~$ x=
anna@HP-Printer:~$ echo $x

anna@HP-Printer:~$ x=""
anna@HP-Printer:~$ echo $x

```

### Local Variable
* To access all the local variables - run this command
```bash
anna@HP-Printer:~$ set
```
* UDV (User defined variables) - Setting variable value:
```bash
anna@HP-Printer:~$ mybestname=3
anna@HP-Printer:~$ echo $mybestname
3
anna@HP-Printer:~$ set | grep mybestname   # access the local variable via the `set` 
mybestname=3
```
### Common Local Variables
* HISTFILESIZE determine how many command to be saved in the history file on logout
* COLUMNS sets the width of the terminal
* LINES sets the height of terminals
* PS1 sets the prompt
* SHELL Our shell name
* OSTYPE Our o/s type 
* USERNAME - User name who is currently login to this PC
* LOGNAME - Our logging name
You can print any of the above variables contain as follows
```bash
anna@HP-Printer:~$ echo $PS1
\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$
```
or:
```bash
anna@HP-Printer:~$ set | grep PS1
PS1='\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
```
### Environment variables
* Shell variables exist only in current shell instance
* Environment variables passed to subshells
* Shell variables can be exported into environment
```bash              
anna@Secondary:~$ a=/home/anna/         # a is a local variable                                                   
anna@Secondary:~$ bash                  # open a sub-priccess
anna@Secondary:~$ echo $HOME            # $HOME is an env variable - so it is can be accessed                                                                                
/home/anna                                                                                                      
anna@Secondary:~$ echo $a              # a is a local variable - so it is can't be accessed                                                                                                   
                                                                                                                
anna@Secondary:~$ exit                  # exit the sub-priccess, and return to the parent proccess                                                                                     
exit                                                                                                            
anna@Secondary:~$ export a              # now we are exporting the local variable - so we will be able to access it from the child proccess                                                                                   
anna@Secondary:~$ bash
anna@Secondary:~$ echo $a
/home/anna/
anna@Secondary:~$ echo $HOME
/home/anna
anna@Secondary:~$ set|head              #this is the way to print all local variable
A=/home/anna/
BASH=/bin/bash
```


### Common Environment variables
* You can print any of the Environment variables contain as follows
```bash
anna@HP-Printer:~/Desktop$ env
```
* HOME Path to user’s home directory
* LANG  Identification of default language program should use
* PWD User’s current working directory
* EDITOR default editor program
* LESS options to pass to the command less
* TERM terminal type
* PATH colon separated list of locations where commands can be found
* which command (not variable) showing path of executable
    ```bash
    anna@HP-Printer:~/Desktop$ which ls
    /bin/ls
    ```


### Aliases
* Aliases let you create shortcuts to command
```bash
anna@Secondary:~$ alias hi="echo hello"
anna@Secondary:~$ hi
hello
```
This will add it only to the local [prompt, in order to add it to all ot the prompt, run:
```
anna@Secondary:~$ echo 'alias hi="echo hello"' >> ~/.bashrc
```
* To remove an alias, run:
```bash
anna@Secondary:~$ alias hi="echo hello"
anna@Secondary:~$ hi
hello
anna@Secondary:~$ unalias hi
anna@Secondary:~$ hi

Command 'hi' not found
```
* Use `alias` to see all set aliases 
* To see specific alias value: 
```bash
anna@Secondary:~$ alias hi="echo hello"
anna@Secondary:~$ alias hi
alias hi='echo hello'
```


### Commands and Arithmetic

* Command output: `` or `$()` - substitute output from a command in a command line
    ```bash
    anna@HP-Printer:~/Desktop$ echo "date"
    date
    anna@HP-Printer:~/Desktop$ echo $(date)
    Sat Jan 5 13:21:07 IST 2019
    anna@HP-Printer:~/Desktop$ echo `date`
    Sat Jan 5 13:21:15 IST 2019
    ```
* Arithmetic: `$[ ]` - Substitute result of arithmetic expression in a command line
    ```bash
    anna@HP-Printer:~/Desktop$ echo $[5 + 5]
    10
    anna@HP-Printer:~/Desktop$ echo $[5 - 5]
    0
    anna@HP-Printer:~/Desktop$ echo $[5 * 5]
    25
    anna@HP-Printer:~/Desktop$ echo $[5 / 5]
    1
    anna@HP-Printer:~/Desktop$ echo $[5 % 5]
    0
    anna@HP-Printer:~/Desktop$ echo $[5 + 5.4]  #bash can run only int or string
    bash: 5 + 5.4: syntax error: invalid arithmetic operator (error token is ".4")

    # use with variables
    anna@HP-Printer:~/Desktop$ x=2
    anna@HP-Printer:~/Desktop$ y=4
    anna@HP-Printer:~/Desktop$ echo $[x + y]
    6

    ```
*  Arithmetic: `expr` - arithmetic expression

    * Note: `expr` can work only with integer argument
    ```bash
    anna@HP-Printer:~$ expr 2 * 3
    expr: syntax error
    ```

    * Note: to Multiplication use `\*` and not `*`
    ```bash
    anna@HP-Printer:~$ expr 2 + 3
    5
    anna@HP-Printer:~$ expr 2 / 3
    0
    anna@HP-Printer:~$ expr 2 \* 3
    6
    anna@HP-Printer:~$ expr 2 - 3
    -1
    anna@HP-Printer:~$ expr 2 % 3
    2
    ```



anna@HP-Printer:~$ expr 2.5 + 3.5
expr: non-integer argument
```
### Protecting from Expansion
* Backslash `( \ )`  is the escape character and makes the next character literal
```bash
anna@HP-Printer:~/Desktop/t$ x=4
anna@HP-Printer:~/Desktop$ echo $x
4
anna@HP-Printer:~/Desktop$ echo \$x
$x
```
* Single quotes (‘)  inhibit all expansion
```bash
anna@HP-Printer:~/Desktop/t$ x=4
anna@HP-Printer:~/Desktop$ echo $x
4
anna@HP-Printer:~/Desktop$ echo '$x'
$x
anna@HP-Printer:~/Desktop$ echo "$x"
4
```
note: there is a diference between `$` to `''`:
```bash
anna@Secondary:~$ echo \$\$\$\$\$
$$$$$
anna@Secondary:~$ echo '$$$$$'
$$$$$
```
* Double quotes usage:
```bash
anna@Secondary:~$ var=123
anna@Secondary:~$ VAR="o $var"
anna@Secondary:~$ echo $VAR
o 123
anna@Secondary:~$ VAR='o $var'
anna@Secondary:~$ echo $VAR
o $var
```
### usage of {}
```bash
anna@Secondary:~$ echo 123_456
123_456
anna@Secondary:~$ var1=123
anna@Secondary:~$ var2=456
anna@Secondary:~$ echo $var1_$var2
456
anna@Secondary:~$ echo ${var1}_${var2}
123_456
```
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







 



TODO-START
### write into files 
* `echo -e "/n/n" > a.txt`
* `echo -e "/n/n" >> a.txt`
### locate + updatedb
### ext-undelete
TODO-END

