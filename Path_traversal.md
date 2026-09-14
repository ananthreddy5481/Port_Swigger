## Path Traversal

In general, a web application stores files on a server and loads a particular file based on the user's request.

If the application does not properly restrict which files can be accessed, an attacker may be able to access unauthorized files that were
not intended to be accessible to them, potentially exposing sensitive information.

This can happen by manipulating the file path or filename supplied to the application, causing the server to access a different file than
the developer intended.

### LAB - 1

***Path Traversal - /etc/passwd in img file source***
