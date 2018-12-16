# Level 0

LINK : http://overthewire.org/wargames/natas/natas0.html

- Open http://natas0.natas.labs.overthewire.org/

- Login with given username/password

- It say  
  You can find the password for the next level on this page.

- First Rule of web testing is Open up DevTools and check network requests, which gives nothing

- Second Rule is check Console, where we see current user name & password. 

- Let's see where it is logged from 

- Simple JS, which gives nothing however wechallinfo see global, let's search for that `wechallinfo`

- Here is the password commented in html :|

  ```html
  <!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
  
  ```
