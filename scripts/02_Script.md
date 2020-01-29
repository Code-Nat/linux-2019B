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
anna@HP-Printer:~$ echo $($(cat test1))
"hello tset"
anna@HP-Printer:~$ bash test1
hello tset
```

* Because of security of files, in Linux, the creator of Shell Script does not get execution permission by default. So if we wish to run shell script we have to do two things as follows 
   * Use chmod command as follows to give execution permission to our script 

   ```
   chmod   +x    shell-script-name 
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


