# Level 7-8

LINK : http://overthewire.org/wargames/natas/natas8.html

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
<script>var wechallinfo = { "level": "natas8", "pass": "<censored>" };</script></head>
<body>
<h1>natas8</h1>
<div id="content">

<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>

<form method=post>
Input secret: <input name=secret><br>
<input type=submit name=submit>
</form>

<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
</html>
```

Here 
bin2hex(strrev(base64_encode($secret)) == "3d3d516343746d4d6d6c315669563362"

Let's reverse it 

```bash
ctf-elixir$ php -a
Interactive mode enabled

php > var_dump(hex2bin("3d3d516343746d4d6d6c315669563362"));
string(16) "==QcCtmMml1ViV3b"
php > var_dump(strrev(hex2bin("3d3d516343746d4d6d6c315669563362")));
string(16) "b3ViV1lmMmtCcQ=="
php > var_dump(base64_decode(strrev(hex2bin("3d3d516343746d4d6d6c315669
string(10) "oubWYf2kBq"
php > 

```

Which returns 

Access granted. The password for natas9 is 	W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl





