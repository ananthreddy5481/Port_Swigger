# CSRF - Cross Site Request Forgery

CSRF is an attack where a malicious website causes a victim's browser to send authenticated requests to another website where the victim is
already logged in.

why this occurs ?

Web applications commonly use cookies to maintain user sessions because HTTP is a stateless protocol. Once a user logs in, the browser
stores a session cookie and automatically sends it with future requests. CSRF uses this behavior to either manipulate directly from the
user browser.

***The attacker is usually not interested in reading the response. Their goal is to cause the server to perform an action on behalf of the authenticated victim.***

## Architecture

```
Architecture :

                    ATTACKER
                        |
                        | Creates a malicious webpage,
                        | email, or hidden form
                        ▼
                MALICIOUS WEBSITE
                        |
                        | Victim unknowingly visits it
                        ▼
               VICTIM'S BROWSER
                        |
                        | Browser automatically sends
                        | authenticated request from the user browser
                        | in the name of user.
                        | (session cookies included)
                        ▼
                WEB APPLICATION
                        |
                        | Server validates the
                        | session cookie but does not
                        | verify the request origin
                        ▼
              Sensitive action performed
      (Transfer money / Change password / Delete account)
                        |
                        ▼
                  CSRF OCCURS

```

## CSRF Labs ::

### Lab 1

craft html that victim receives visiting it will send a request for change in the viewer's email address automatically for a vulnerable site.

```initial login : wiener:peter```

burpsuite  capture for the mail address change:

<img width="495" height="509" alt="Screenshot 2026-08-31 at 18 21 56" src="https://github.com/user-attachments/assets/a326b205-a652-4595-9ff9-abc559493190" />

```
html request payload:

<form action="https://0a6a009c049ee71b81cf5751006200d4.web-security-academy.net/my-account/change-email"
      method="POST">

    <input type="hidden"
           name="email"
           value="avengers@gmail.com">

</form>

<script>
document.forms[0].submit();
</script>
```

changes the mail to ```avengers@gmail.com```.




### Lab 2

email change functionality is vulnerable to CSRF. It attempts to block CSRF attacks, but only applies defenses to certain types of requests.

burpsuite  capture for the mail address change:

<img width="482" height="490" alt="Screenshot 2026-08-31 at 20 07 31" src="https://github.com/user-attachments/assets/5c543ece-d6a2-478e-b972-02cd991a0122" />


csrf token - verifies the authenticity of requests made by a user. Each CSRF token is unique to an individual user session and is embedded in web forms or requests.

the post request evaluates the request using the csrf token. to pass this we have two
ways.
i) get the csrf token of the victim to pass it in the attack payload.

ii) lab suggests that csrf defence is applied only on POST so use ```GET``` request to submit the form.

in this lab as the ```view exploit``` uses our session only so we can use the token we got in the burp capture. 

to ```deliver exploit to victim``` where port swigger runs on different session we should change the request method.

***for this kind of situation, in real life we cannot get the csrf token that easily so changing the request method is reliable.***
