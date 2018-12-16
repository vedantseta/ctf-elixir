# Level 1-2

LINK : http://natas2.natas.labs.overthewire.org/

- It says  
  There is nothing on this page ![img](http://natas2.natas.labs.overthewire.org/files/pixel.png)

- Let's quickly search password, which gives nothing

- I believe the question, lets start analysing network, where there is strange files/pixel.png with Authorisation request header. But that's my header :|

- Let's look at 
  http://natas2.natas.labs.overthewire.org/files

- Bang, pixel.png and users.txt where the password is safely stored


```txt
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```

