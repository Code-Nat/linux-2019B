## Create a function that gets 2 numbers and prints their sum
```bash
#!/bin/bash
f1() {
 echo "$1 + $2 = $[ $1 + $2 ]"
}
echo "enter first mum:"
read num1
echo "enter second num:"
read num2
f1 $num1 $num2
```
example of running:

```
enter first mum:
2
enter second num:
3
2 + 3 = 5
```

## Create a function that gets 2 numbers and prints their mul (without "*" or loop)

```bash
#!/bin/bash

f1() {
if [ $2 -eq 1 ]
then
 echo $[ $3 + $1 ]
else
 mul=$( expr $3 + $1 )
 next=$( expr $2 - 1 )
 f1 $1 $next $mul
fi
}
f1 6 3 0
```
example of running:
```
18
```


## Create a function that get a name of a folder and prints the max depth of this folder

for example:
if we path "a" as a folder name, and a has the following content:
```
anna@HP-Printer:~$ tree a
a
├── b
│   ├── e
│   │   └── g
│   └── f
└── d

```
we will get `4` as output



```bash
#!/bin/bash

f1() {
ls $1$2/* >> file.log
if [ $? -ne 0 ]
then 
 len=${#2}
 echo "depth of $1 is $[len/2] ($2)"
else
 f1 $1 "$2/*"
fi
}
f1 "Database-2019A-II" "/*" 
```


