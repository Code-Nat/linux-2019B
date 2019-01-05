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

### Local Variable
* Conventionally all upper-case
* Setting variable value:
```bash
anna@HP-Printer:~/Desktop$ X=8
anna@HP-Printer:~/Desktop$ echo $X
8
```
### Common Local Variables
* HISTFILESIZE determine how many command to be saved in the history file on logout
* COLUMN sets the width of the terminal
* LINES sets the height of terminals
* PS1 sets the prompt

### Environment variables
* Shell variables exist only in current shell instance
* Environment variables passed to subshells
* Shell variables can be exported into environment
```bash              
anna@Secondary:~$ A=/home/anna/         # A is a local variable                                                   
anna@Secondary:~$ bash                  # open a sub-priccess
anna@Secondary:~$ echo $HOME            # $HOME is an env variable - so it is can be accessed                                                                                
/home/anna                                                                                                      
anna@Secondary:~$ echo $A               # A is a local variable - so it is can't be accessed                                                                                                   
                                                                                                                
anna@Secondary:~$ exit                  # exit the sub-priccess, and return to the parent proccess                                                                                     
exit                                                                                                            
anna@Secondary:~$ export A              # now we are exporting the local variable - so we will be able to access it from the child proccess                                                                                   
anna@Secondary:~$ bash
anna@Secondary:~$ echo $A
/home/anna/
anna@Secondary:~$ echo $HOME
/home/anna
anna@Secondary:~$ set|head              #this is the way to print all local variable
A=/home/anna/
BASH=/bin/bash
```


### Common Environment variables
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




TODO-START
### write into files 
* `echo -e "/n/n" > a.txt`
* `echo -e "/n/n" >> a.txt`
### locate + updatedb
### ext-undelete
TODO-END

