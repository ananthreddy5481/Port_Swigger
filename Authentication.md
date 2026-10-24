# Authentication vs Authorization 

authentication is verifying their identity using credentials for giving him access to the resource that he is trying to access.

**authentication basically answers the question "who are you ?".**

authorization determines weather that user is allowed to perform a particular thing in the application.it is basically done by roles(user
or admin).

**authorization answers "What are you allowed to do?"**


Enumeration using Status code :

status code 200 : server responded correctly for the request made by the client browser.
status code 401 : authentication failure.

in some applications, status code 200 is returned for correct username and wrong password. 200 doesnt mean you will given the login but
instead of failure message, the application will return 200. but for both username and password wrong it will return 401. this difference
is useful to find the correct username using bruteforcing.

