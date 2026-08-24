## XSS - cross Site Scripting

XSS : web application vulnerability where attacker crafted malicious code gets interpreted and executed by the victim's browser. basically attacker's script running in the victim.

### Architecture :

```
          ATTACKER
              │
              │ Malicious input
              ▼
       WEB APPLICATION
              │ victim tries to load the malicious input of the attacker(unknowingly)
              ▼
       VICTIM'S BROWSER
              │ victim's browser will interpret that as a block of code that the web server sent it. and executes it.
              ▼
     Browser interprets
       input as code
              │ this execution will cause the output intended by the attacker.
              ▼
          XSS occurs
```

will the input that we give be stored in the application's files ? 

The attacker's payload does not modify application files. It is stored as user input (e.g., comments or usernames) in the database or parameter. The server/database treats it as data,
while the victim's browser may interpret it as code when loading the response.


### Types of XSS :

### Stored XSS :

Stored XSS occurs when malicious input is permanently stored by the application and later executed whenever users visit the affected page.

In a vulnerable blog, the attacker's payload is stored in the database as a comment. 
When another user opens the comments, the malicious comment is sent to their browser, which interpretsit as code and executes it. 

here the payload is stored permanently so it is called ```stored XSS```.

```
                    BLOG WEBSITE
                         │
                         ▼
              ┌─────────────────────┐
              │   Comment Section   │
              └─────────────────────┘
                         │
              Attacker enters a
              malicious comment
                         │
                         ▼
        <script>alert("XSS")</script>
                         │
                         ▼
              ┌─────────────────────┐
              │      Database       │
              │                     │
              │ Normal comment      │
              │ Malicious payload   │
              └─────────────────────┘
                         │
                 Victim opens blog
                         │
                         ▼
              Server retrieves
              stored comments
                         │
                         ▼
              Sends comments to
              victim's browser
                         │
                         ▼
              Browser interprets
              payload as JavaScript
                         │
                         ▼
                    XSS Executes
                         │
                         ▼
              alert("XSS") appears
```

### Reflected XSS :

Reflected XSS occurs when user input is immediately returned in the server response without proper validation or encoding. The payload is not stored permanently. The victim must interact with a crafted link or request each time for the attack to execute. 

for example ::
```
https://example.com/search?q=apple

Search results for: apple -- now imagine the q parameter's value is poorly treated, then attacker will craft url as 

example.com/search?q=[XSS payload]

it is forwarded to the victim and when he clicks that victim's browser treats it as a code.

executes that XSS payload as :
<h1>Search results for: [XSS payload]</h1>

```


### DOM Based XSS :

DOM - Document Object Model - It is a structured representation of a web page that allows developers to access, modify, and control its content and structure using JavaScript.

DOM-Based XSS occurs when attacker-controlled data reaches a dangerous DOM operation through client-side JavaScript, causing the browser to interpret the data as executable code.

```
Attacker-controlled input
        ↓
Client-side JavaScript
        ↓
DOM manipulation
        ↓
Browser interprets content
        ↓
XSS executes
```

example ::

suppose a site - ```https://example.com/welcome#Jhon```

#Jhon - URL fragment that is not sent to the server. It remains in the browser and can be used by the browser for page navigation or accessed by JavaScript through ```location.hash```.


server receives - GET /welcome

after the webserver responding the Js will search for the #Jhon in the response and if it is not handled then it can used for malicious input.

this looks similar to the Reflected XSS, but difference is 

```
the malicious code is sent to the server and the server reflects back that response with the malicious code in it, in reflected XSS. here the vulnerability is all executed in the client side only. malicious code is not sent to the server.
```
is DOM affected only by the DOM-based XSS ?

No, every XSS will affect the DOM structure. but this one is called DOM based because other two will affect indirectly, actually server will edit it, but here the malicious code directly affects the DOM.


