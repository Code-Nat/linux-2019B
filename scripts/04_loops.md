
## Note:
when we run a script - the current path in the script will be according to the path that runs the script.   
For example:
```bash
anna@HP-Printer:~$ cat > b.bash
#!/bin/bash
echo "Hello script"
pwd

anna@HP-Printer:~$ ./b.bash 
Hello script
/home/anna

anna@HP-Printer:~$ cd ..
anna@HP-Printer:/home$ ./anna/b.bash 
Hello script
/home
```

# For Loop


### Basic for loop

```bash 
#!/bin/bash

for i in a b c
do
echo "hello" $i
done
```

Output
```
hello a
hello b
hello c
```


### for loop that prints the lines of all the files in current directory

```bash 
#!/bin/bash

files=$(ls -l | grep -E "^-" | cut -d":" -f2 | cut -d" " -f2)
for i in $files 
do
wc -l $i
done
```

### a script that prints the content of the file with the max length in the directory


```bash 
#!/bin/bash

files=$(ls -l | grep -E "^-" | cut -d":" -f2 | cut -d" " -f2)
max=0
file=""

for i in $files 
do
if ( test $(wc -l $i | grep -o "[0-9] ") -ge $max)
then
 max=$(wc -l $i | grep -o "[0-9] ")
 file=$i
fi
done

echo $file " contains " $max " lines: "
cat $file
```


### Print sum of all parameters that you got to script

```bash 
#!/bin/bash

sum=0
for i in $*
do
sum=$[sum + i] 
done

echo $sum
```

running example:
```
anna@HP-Printer:~$ ./b.bash 1 2 3 4
10
```


# While Loop

### simple while loop
```bash
#!/bin/bash
i=2
while test $i -lt 5
do
echo $i
i=$[i + 1]
done
```
Output:
```
2
3
4
```


# Until Loop

### simple while loop
```bash
#!/bin/bash
i=2
until test $i -gt 5
do
echo $i
i=$( expr $i + 1 )
done
```
Output:
```
2
3
4
5
```


### loops task
* Craete a script that gets from the user a number
* Loop over the number that you got in the previous step
    * each time get from the user a file name - and sum all the lines in the files