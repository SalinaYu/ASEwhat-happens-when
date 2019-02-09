# HTTP Server Request Handling

The HTTPD (HTTP Daemon) server handles the requests/responses on the server side. The most common HTTPD servers are Apache or nginx for Linux and IIS for Windows.

* The HTTPD (HTTP Daemon) receives the request.
* The server breaks down the request to the following parameters:
   * HTTP Request Method (either ``GET``, ``HEAD``, ``POST``, ``PUT``,``DELETE``, ``CONNECT``, ``OPTIONS``, or ``TRACE``). In the case of a URL entered directly into the address bar, this will be ``GET``.
   * Domain, in this case - google.com.
   * Requested path/page, in this case - / (as no specific path/page was requested, / is the default path).
* The server verifies that there is a Virtual Host configured on the server that corresponds with google.com.
* The server verifies that google.com can accept GET requests.
* The server goes to pull the content that corresponds with the request, in our case it will fall back to the index file, "/".
* Assuming this is not static content, the web server parses the file according to the handler (CGI, PHP, Java Servlets, JSP, etc.). 


The response is pushed back down the OSI model -- chunked, encrypted against the sesion key (if TLS), split into TCP packets, IP encapsulated, split into frames and sent down the data link and physical layers, and ultimately arrives back at your machine's network stack. From there the frames are reassembled into packets, buffered and ordered as TCP, and then interpretted as HTML, CSS, JS, etc. by your browser.

_Demonstration Steps:_

[Response to the Browser.md](./11-Browser.md)