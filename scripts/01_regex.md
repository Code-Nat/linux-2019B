
# REGEX
regex - A regular expression is simply a description of a pattern that describes a set of possible characters in an input string
* There is considerable variation from utility to utility
    * The shell is limited to fairly simple metacharacter substitution (*,?, […]) and doesn’t really support regex
    * Regex in vi are also fairly limited
    * Regex in sed are not exactly the same as regex in Perl, or Awk, or grep, or egrep
* This puts the onus on the user to examine the man page or other documentation for these utilities to determine which flavor of regex are supported
* Since many of the special characters used in regexs also have special meaning to the shell, it’s a good idea to get in the habit of single quoting your regexs
    * This will protect any special characters from being operated on by the shell
    * If you habitually do it, you won’t have to worry about when it is necessary
* Note the difference between the `*` in a regex and the shell’s usage
    * In a regex, a `*` only stands for zero or more occurrences of a single preceding character
    * In the shell, the `*` stands for any number of characters that may or may not be different 
* Ranges can also be specified in character classes
    * `[1-9]` is the same as `[123456789]`
    * `[abcde]` is equivalent to `[a-e]`
You can also combine multiple ranges
    * `[abcde123456789]` is equivalent to `[a-e1-9]`
Note that the `-` character has a special meaning in a character class BUT ONLY if it is used within a range
    * `[-123]` would match the characters `-`, `1`,`2` or `3`



#### grep vs egrep
*  In basic `grep` regular expressions the meta-characters:
```
?, +, {, |, (, and ) 
```
lose their special meaning. instead use the backslashed versions:
```
\?, \+, \{, \|, \(, and \)
```
* In `egrep` regular expressions the meta-characters:
```
?, +, {, |, (, and ) 
```
Do not lose their special meaning.
* `egrep` is the same as `grep -E`

#### Good online regex tester
https://regex101.com/





[[:alnum:]] – Alphanumeric characters.
[[:alpha:]] – Alphabetic characters
[[:blank:]] – Blank characters: space and tab.
[[:digit:]] – Digits: ‘0 1 2 3 4 5 6 7 8 9’.
[[:lower:]] – Lower-case letters: ‘a b c d e f g h i j k l m n o p q r s t u v w x y z’.
[[:space:]] – Space characters: tab, newline, vertical tab, form feed, carriage return, and space.
[[:upper:]] – Upper-case letters: ‘A B C D E F G H I J K L M N O P Q R S T U V W X Y Z’.

\< Match the empty string at the beginning of word
\> Match the empty string at the end of word.
\B	Matches the empty string provided it’s not at the edge of a word.
\b	Matches the empty string at the edge of a word.







```bash

anna@HP-Printer:~$ echo {A,b}{a,B,C}{1,2,3,&}.txt |tr ' ' '\n'>t.txt
anna@HP-Printer:~$ cat t.txt
Aa1.txt
Aa2.txt
Aa3.txt
Aa&.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt
AC1.txt
AC2.txt
AC3.txt
AC&.txt
ba1.txt
ba2.txt
ba3.txt
ba&.txt
bB1.txt
bB2.txt
bB3.txt
bB&.txt
bC1.txt
bC2.txt
bC3.txt
bC&.txt


anna@HP-Printer:~$ grep '^$' t.txt              #search for emty lines

anna@HP-Printer:~$ grep '^A' t.txt 
Aa1.txt
Aa2.txt
Aa3.txt
Aa&.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt
AC1.txt
AC2.txt
AC3.txt
AC&.txt


anna@HP-Printer:~$ grep '^A[aB]' t.txt 
Aa1.txt
Aa2.txt
Aa3.txt
Aa&.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt


anna@HP-Printer:~$ grep '^AB[1-3]' t.txt 
AB1.txt
AB2.txt
AB3.txt

anna@HP-Printer:~$ grep '^AB[^1-3]' t.txt 
AB&.txt


anna@HP-Printer:~$ grep '^A[a-cA-C]1' t.txt 
Aa1.txt
AB1.txt
AC1.txt


anna@HP-Printer:~$ grep '^AB1\.txt' t.txt 
AB1.txt


anna@HP-Printer:~$ grep '^AB.' t.txt 
AB1.txt
AB2.txt
AB3.txt
AB&.txt


anna@HP-Printer:~$ grep '^AB[[:alnum:]]' t.txt 
AB1.txt
AB2.txt
AB3.txt



1 anna@HP-Printer:~$ grep '^[[:upper:]]' t.txt 
Aa1.txt
Aa2.txt
Aa3.txt
Aa&.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt
AC1.txt
AC2.txt
AC3.txt
AC&.txt


anna@HP-Printer:~$ grep '^[[:lower:]]' t.txt 
ba1.txt
ba2.txt
ba3.txt
ba&.txt
bB1.txt
bB2.txt
bB3.txt
bB&.txt
bC1.txt
bC2.txt
bC3.txt
bC&.txt




anna@HP-Printer:~$ egrep '^A(a|B)1' t.txt
Aa1.txt
AB1.txt



anna@HP-Printer:~$ egrep "^[A-B]{1,2}" t.txt
Aa1.txt
Aa2.txt
Aa3.txt
Aa&.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt
AC1.txt
AC2.txt
AC3.txt
AC&.txt


anna@HP-Printer:~$ egrep "^[A-B]{2}" t.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt



anna@HP-Printer:~$ egrep "^[A-B]{2,}" t.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt



# `+` - The preceding item will be matched one or more times.
anna@HP-Printer:~$ egrep "AB+" t.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt


# `?` - The preceding item is optional and will be matched, at most, once.
anna@HP-Printer:~$ egrep "AB?" t.txt
Aa1.txt
Aa2.txt
Aa3.txt
Aa&.txt
AB1.txt
AB2.txt
AB3.txt
AB&.txt
AC1.txt
AC2.txt
AC3.txt
AC&.txt



# `*` - The preceding item will be matched zero or more times.
anna@HP-Printer:~$ egrep "AB1.*" t.txt
AB1.txt


anna@HP-Printer:~/Desktop/linux/test$ ls |grep -E documenta[0-9]+\.doc



```