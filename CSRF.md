## CSRF - Cross Site Request Forgery

CSRF is an attack where a malicious website causes a victim's browser to send authenticated requests to another website where the victim is
already logged in.

why this occurs ?

Web applications commonly use cookies to maintain user sessions because HTTP is a stateless protocol. Once a user logs in, the browser
stores a session cookie and automatically sends it with future requests. CSRF uses this behavior to either manipulate directly from the
user browser.

***The attacker is usually not interested in reading the response. Their goal is to cause the server to perform an action on behalf of the authenticated victim.***

### Architecture

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

### CSRF Labs ::

