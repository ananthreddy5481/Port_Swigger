### LAB - 1

Reflected XSS 

A) search bar - do not store the things we search. 

B) it is sent to webserver by using url(parameters) and then for that specific request the server will respond.

C) in this response it will reflect back the search parameter value to the browser.

D) browser now interprets that as executible code.

``` payload : <script>alert("error");</script> ```

this triggers the alert pop up message in the browser.

here we can see that the payload is going as a parameter value in the request:

<img width="429" height="111" alt="Screenshot 2026-08-25 at 14 43 37" src="https://github.com/user-attachments/assets/ef83906f-3153-4de7-bd1a-0b4191c5a317" />

### LAB - 2

Stored XSS

A) there are some blog posts and commenting feature which is vulnerable to xss.

B) users will comment -> store in database -> again get those comments whenever others open that blog post's comment section -> at that time the attacker's malicious code will be
retrieved from database and will be sent to browser and it execute that as a code.

``` payload : <script>alert("error");</script>```

here we can see that the payload is being sent in the request header unlike in the reflected it sent as user parameter value: 

<img width="1027" height="92" alt="Screenshot 2026-08-25 at 15 09 04" src="https://github.com/user-attachments/assets/50b2e3a8-418f-4939-89c1-c9309423d2c4" />




