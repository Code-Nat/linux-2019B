# Bash
* bash is “Bourne Again shell “
* Developed  for GNU project 
* bash is compatible with Bourne shell (sh) – the original (standard) UNIX shell.
    * Bourne shell (sh) –original UNIX shell written by Steven Bourne at AT&T
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


###

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