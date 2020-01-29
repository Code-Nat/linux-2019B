
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

### `{}` for range
```bash
anna@HP-Printer:~$ echo {a..c}
a b c
anna@HP-Printer:~$ echo {a..c}{1..2}
a1 a2 b1 b2 c1 c2
```

### wildcard (globs)
 * `*`   matches zero or more characters
 * `?`   matches any single character
 * `[a-z]`  matches a range of characters  
 * `[^a-z]` matches all except the range
Example where we use globs: `ls`

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