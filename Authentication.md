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

## Lab 1

**Username enumeration via different responses**

<img width="1151" height="610" alt="Screenshot 2026-10-24 at 11 35 34" src="https://github.com/user-attachments/assets/acee7e77-9159-4737-8241-300ab3044893" />

for other usernames it was showing incorrect username and for **```ae```** it gave response length different with response "incorrect
password".

password brute forcing ::

<img width="1181" height="422" alt="Screenshot 2026-10-24 at 11 44 15" src="https://github.com/user-attachments/assets/2bdf98fc-05ca-4433-ac49-d5e87e38aae5" />

status code 302 :: redirected to another location.

correct password gives 302 cause as soon as entering correct creds you will be redirected to dashboard(kind off) page.here it is redirecting to /myaccount with id=ae.



## Lab 2

**Username enumeration via subtly responses**

<img width="1264" height="752" alt="Screenshot 2026-10-24 at 12 19 59" src="https://github.com/user-attachments/assets/7866db52-09a5-48e4-8384-39c0a4d35594" />

in intruder settings,

<img width="751" height="655" alt="Screenshot 2026-10-24 at 12 23 40" src="https://github.com/user-attachments/assets/d3000cde-248e-4e37-a237-f2c8ce1b65b8" />

here we added the response part that needs to be checked for finding difference in the username.

for the username **```autodiscover```** the response does not contain fullstop. in other response it is "invalid username or password.", but for this user it is "invalid username or password" this difference in response is enough. 

<img width="1470" height="879" alt="Screenshot 2026-10-24 at 12 21 13" src="https://github.com/user-attachments/assets/559d0b52-b871-4ef0-860a-bbd3bde182da" />
