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


### LAB - 3 

DOM Based XSS

``` user input in search field -> location.search function handles input -> forwards it to document.write function -> this directly writes to the response -> forwarded to browser```

```payload : "><script>alert(5);</script>```

"> because this input will be going into the DOM code directly instead of travelling to the server this should close the existing fields for example :

<input value="YOUR_INPUT">  -- it should first close the existing html line and then this script will be written in between in the user browser.

the above parsing technique is not exclusive to DOM here the input in handled inside the <""> so it is used. even in stored and reflected xss if the input is handled like this then we
should first try to close the existing symbols.


### LAB - 4

DOM Based XSS (innerHTML)

innerHTML ::a property of the DOM that allows you to get or set the HTML content inside a specific web page element

Syntax: element.innerHTML = "new content";

Action: The browser takes the string on the right side of the equals sign, reads it as HTML code, deletes all old child elements inside that element, and builds the new elements right
there.

***user input will be directly used to manipulate the html DOM but the limitation is js engine will not run new scripts inside the innerHTML property.(cannot write new script)***

``` payload :: <img src=x onerror=alert(1)> ```

this is an html payload which can be used for before labs also instead of writing the new javascript.


### LAB - 1 (P)

DOM based xss

<img width="1650" height="688" alt="image" src="https://github.com/user-attachments/assets/5c8ccb7c-5ef1-422c-ba8e-8dae4be169cb" />

the above image confirms that user input is handled by the document.write which directly writes into the js code.

but in the url parameter is missing so find it here and add it manually it.

location.search is taking input from ```storeId``` so that is the parameter that we need to use to make the css exploit.

craft the final url ::
```
https://0adc002003ee04b580036756009b00d1.web-security-academy.net/product?productId=2&storeId=%3Cimg%20src=x%20onerror=alert(1)%3E
```


### LAB - 2 (P)

Angular JS - handles features like dynamic content presentation and user interface actions.

AngularJS Steps In (The Front Door Opens)

AngularJS acts like a second compiler inside your browser. It scans down the DOM tree looking for things to compute.

It spots the {{ and }} markers. To AngularJS, these markers mean: "Stop treating this as text. Treat everything inside here as code and execute it immediately."

```
payload :: {{constructor.constructor('alert(1)')()}}
```


