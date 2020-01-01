# Test
```
anna@HP-Printer:~$ whatis test
test (1)             - check file types and compare values

```
## Note:
* if the status code of the result is `1` - it is false
* if the status code of the result is `0` - it is true
* `echo $?` is to print the status code of the last command

## Test for comparing two numbers 
* given the following configuration:
```
anna@HP-Printer:~$ a=3
anna@HP-Printer:~$ b=4
```
* test if `a` is *less than* `b`:
```
anna@HP-Printer:~$ test $a -lt $b ; echo $?
0
```
* test if `a` is *greater than* `b`:
```
anna@HP-Printer:~$ test $a -gt $b ; echo $?
1
```
* test if `a` is *less equale* `b`:
```
anna@HP-Printer:~$ test $a -le $b ; echo $?
0
```
* test if `a` is *greater equale* `b`:
```
anna@HP-Printer:~$ test $a -ge $b ; echo $?
1
```
* test if `a` is *equale* to `b`:
```
anna@HP-Printer:~$ test $a -eq $b ; echo $?
1
```
* test if `a` is *not equale* to `b`:
```
anna@HP-Printer:~$ test $a -ne $b ; echo $?
0
```
## Test for comparing two strings 
* given the following configuration:
```
anna@HP-Printer:~$ a="test"
anna@HP-Printer:~$ b="ok"
anna@HP-Printer:~$ c="ok"
anna@HP-Printer:~$ d=""
```
* test if `a` is *not equale* to `b`:
```
anna@HP-Printer:~$ test $a != $b ; echo $?
0
```
* test if `a` is *not equale* to `c`:
```
anna@HP-Printer:~$ test $b != $c ; echo $?
1
```
* test if `b` is *equale* to `c`:
```
anna@HP-Printer:~$ test $b = $c ; echo $?
0
```
* test if `a` is *equale* to `b`:
```
anna@HP-Printer:~$ test $a = $b ; echo $?
1
```
* test if `hello` is *equale* to `a`:
```
anna@HP-Printer:~$ test "hello"=$a; echo $?
0
```
* test if `d` contains *zero chars*:
```
anna@HP-Printer:~$ test -z $d ; echo $?
0
```
* test if `c` contains *zero chars*:
```
anna@HP-Printer:~$ test -z $c ; echo $?
1
```


## script to check if two script-parameters are equale
given the following script:
```bash
#!/bin/bash
if (test $1 -eq $2)
then
  echo "two parameters are equale"
else
  echo "two parameters are not eqale"
fi
```
test script:
```bash
anna@HP-Printer:~$ bash ./b.bash 8 4
two parameters are not eqale

anna@HP-Printer:~$ bash ./b.bash 8 8
two parameters are equale
```
## script that gets two file names and checks both contain the same content
given the following script:
```bash
#!/bin/bash
x=$(cat $1)
y=$(cat $2)
if (test $x = $y)
then
  echo "two files content are equale"
else
  echo "two files content are not eqale"
fi
```
test script:
```bash
anna@HP-Printer:~$ echo "hello" > a.txt
anna@HP-Printer:~$ echo "hello" > b.txt
anna@HP-Printer:~$ echo "hi" > c.txt
anna@HP-Printer:~$ bash ./b.bash a.txt b.txt
two files content are equale
anna@HP-Printer:~$ bash ./b.bash a.txt c.txt
two files content are not eqale
```

## script that gets a file name and a word - and prints if the word exisits in the file
given the following script:
```bash
x=$(cat $1)
y=$2
c=$(echo $x|grep -c "$y")
if (test $c -gt 0)
then
  echo "$y exists in file $1"
else
  echo "$y does not exist in file $1"
fi
```

test script:
```bash
anna@HP-Printer:~$ echo "hello and bye" > a.txt

anna@HP-Printer:~$ bash ./b.bash a.txt "hello"
hello exists in file a.txt

anna@HP-Printer:~$ bash ./b.bash a.txt "hi"
hi does not exist in file a.txt

anna@HP-Printer:~$ bash ./b.bash a.txt "and"
and exists in file a.txt

```