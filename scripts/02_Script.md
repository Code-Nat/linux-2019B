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
### select
create a file a.bash with this content:
```bash
echo -n "Enter number:"
read num
case $num in

  1)
    echo -n "One"
    ;;

  2)
    echo -n "TWO"
    ;;

  3|4)
    echo -n "THREE OR FOUR"
    ;;

  *)
    echo -n "unknown"
    ;;
esac
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