# POST PRACTICE

LINK : https://ctflearn.com/problems/114

# My Approach
- As this question says These website requires authentication, via POST, let's curl the given page

```sh
$ curl -X POST 'http://165.227.106.113/post.php'

<h1>This site takes POST data that you have not submitted!</h1><!-- username: admin | password: 71urlkufpsdnlkadsf -->%
```

- We have user name & password, Let's pass this in form data 

```sh
$  curl -X POST 'http://165.227.106.113/post.php' -H "Content-Type: application/x-www-form-urlencoded" -d "username=admin&password=71urlkufpsdnlkadsf"

YOUR FLAG IS HERE
```

