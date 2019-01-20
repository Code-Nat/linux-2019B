# Bash
* bash is “Bourne Again shell “
* Developed  for GNU project 
* bash is compatible with Bourne shell (sh) – the original (standard) UNIX shell.
    * Bourne shell (sh) –original UNIX shell written by Steven Bourne at AT&T
* Shell Script is series of commands written in plain text file. 
* Shell Script is interpreted line by line


### How to Run Shell Scripts
* Use the filename of the script as a parameter to `bash`
```bash
anna@HP-Printer:~$ echo 'echo "hello tset"' > test1
anna@HP-Printer:~$ cat test1
echo "hello tset"
anna@HP-Printer:~$ bash test1
hello tset
```

* Because of security of files, in Linux, the creator of Shell Script does not get execution permission by default. So if we wish to run shell script we have to do two things as follows 
   * Use chmod command as follows to give execution permission to our script 

   ```
   chmod    +x    shell-script-name 
   ```
   OR Syntax: 
   ```
   chmod    777    shell-script-name 
   ```
   * Run our script as 
   ```
   ./your-shell-program-name 
   ```
    '.'(dot) is command, and used in conjunction with shell script. The dot(.) indicates to current shell that the command following the dot(.) has to be executed in the same shell.

For example
```
anna@HP-Printer:~$ echo "#!/bin/bash" >> mytest
anna@HP-Printer:~$ echo 'echo "hello tset"' >> mytest
   

anna@HP-Printer:~$ cat mytest

echo "hello tset"

anna@HP-Printer:~$ ./mytest
bash: ./mytest: Permission denied

anna@HP-Printer:~$ chmod 777 mytest

anna@HP-Printer:~$ ./mytest
hello tset

```
### PS4
```bash
#!/bin/bash
set -x              # for debugging - to show what is running 
PS4='${LINENO}:'    # set the value that is printed before each command bash displays during an execution trace (the default is + and here we set it to show the line numbers)
echo 'test1'
echo $0
```
run this script:
```
anna@HP-Printer:~/Desktop/linux$ bash a.bash
```
Output:
```
4:echo test1
test1
5:echo a.bash
a.bash
```


### Shell Startup Script
* NOTE: when you run this command:
```bash
anna@HP-Printer:~$ echo $0
/bin/bash
```
you always get the name of the program executable
 
* The shell program, for example Bash, uses a collection of startup scripts to create an environment. Each script has a specific use and affects the login environment differently. Every subsequent script executed can override the values assigned by previous scripts.

Startup is configured differently for Login shells and Non login shells.
   * Login shells
   * Non login shells

##### Login shells
A Login shell is started after a successful login, using `/bin/login`, by reading the `/etc/passwd` file. Login shell is the first process that executes under our user ID when we log in to a session. The login process tells the shell to behave as a login shell with a convention: 
   * If the output of `echo $0` is the name of our shell, prepended by a dash, then it is a login shell.
   For example -bash, -su etc.
   * If the output of `echo $0` is the name of our shell, does not prepend by a dash, then it is a Non login shell.
   For example bash, su etc.
When Bash is invoked as a Login shell;
   * Login process calls /etc/profile
   * /etc/profile calls the scripts in /etc/profile.d/
   * Login process calls ~/.bash_profile
   * ~/.bash_profile calls ~/.bashrc
   * ~/.bashrc calls /etc/bashrc
   Note:
      * every time when we have the prefix `~` - it refers to a file that the current user can edit
      * only the root can edit the content of `etc`
Login shells include the following.
   * Shells created by explicitly telling to login. examples: 
   ```bash

   # all the 3 following commans are the same - and they are running the full login proccess:
   su -   
   su -l
   su --login

   # all the 3 following commans are the same - and they are used to log as a differnt user:
   su USERNAME -
   su -l USERNAME 
   su --login USERNAME 

   # this command is to get a login shell (the login shell is of the root)
   sudo -i

   ```
   * Shells created at login, including X login. (X is the GUI)

##### Non Login shells
A Non login shell is started by a program without a login. In this case, the program just passes the name of the shell executable. For example, for a Bash shell it will be simply bash.

When bash is invoked as a Non login shell;
   * Non-login process(shell) calls ~/.bashrc
   * ~/.bashrc calls /etc/bashrc
   * /etc/bashrc calls the scripts in /etc/profile.d/

Non login shells include the following.
   * Shells created using the below examples: 
   ```bash
   # switch to  the super user without login
   su 

   # switch to a differnt user without login
   su USERNAME
   ```
   * Graphical terminals
   * Executed scripts
   * Any other bash instances




### select
create a file a.bash with this content:
```bash
#!/bin/bash
select varname in {1..5};
do
   case $varname in
      1)  echo one;;
      2)  echo two;;
      *)  echo "bigger that two";;  # all other cases
   esac
done
```
run this script:
```
anna@HP-Printer:~/Desktop/linux$ bash a.bash
```
Examle of output:
```
1) 1
2) 2
3) 3
4) 4
5) 5
#? 5
bigger that two
#? 1
one
#? 2
two
#? 4
bigger that two
```