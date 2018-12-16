# Level 2-3

LINK : http://overthewire.org/wargames/natas/natas3.html

- Again It says  
  There is nothing on this page ![img](http://natas2.natas.labs.overthewire.org/files/pixel.png)

  ```html
  <!-- This stuff in the header has nothing to do with the level -->
  ```


```html
<!-- No more information leaks!! Not even Google will find it this time... -->
```

- After a good night sleep, I was back to the question. Still trying things. Gave up and started looking for writeups.

- Back to the main page, http://overthewire.org/wargames/natas/
  Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. **All passwords are also stored in /etc/natas_webpass/**. E.g. the password for natas5 is stored in the file /etc/natas_webpass/natas5 and only readable by natas4 and natas5.

- Tried fiddling around to get this file, but failed

- Get a peek at a writeup, which said robots.txt :|

- ALWAYS LOOK AT `robots.txt` file , POINT NOTED 

- There is the the url, were `user.txt` is secretly hiding with

  ```html
  natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
  ```
