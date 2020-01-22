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

