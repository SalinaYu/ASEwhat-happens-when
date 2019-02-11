# HTTP protocol

_Context: Our TCP connection has been established. We've successfully negotiated a TLS session. Now the browser sends the initial request to the web server (likely followed by many subsequent GET requests for resources on the page being retrieved)._

_OSI Layer(s): 7_

## HTTP/2 Aside
It's possible your browser is using something other than HTTP/1.1. HTTP2 (based on Google's SPDY protocol) is starting to become more popular. 

![HTTP/2 Advantages](https://blog.cloudflare.com/content/images/2015/12/image_1.png)

For the sake of this exercise we will assume the request is HTTP/1.1. 

## Initial GET request

```html
    GET / HTTP/1.1
    Host: google.com
    Connection: close
    [other headers]
```

where ``[other headers]`` refers to a series of colon-separated key-value pairs formatted as per the HTTP specification and separated by single new lines.

HTTP/1.1 defines the "close" connection option for the sender to signal that the connection will be closed after completion of the response. For example,

```html
    Connection: close
```

HTTP/1.1 applications that do not support persistent connections MUST include the "close" connection option in every message.

After sending the request and headers, the web browser sends a single blank newline to the server indicating that the content of the request is done.

## HTTP response

The server responds with a response code denoting the status of the request, response headers, and a response body:

```html
    200 OK
    [response headers]

    [Response Body Content]
```

Response headers are followed by a single newline, and then the payload of the HTML content of ``www.google.com``. The server may then either close the connection, or if headers sent by the client requested it, keep the connection open to be reused for further requests.

## Caching
If the HTTP headers sent by the web browser included sufficient information for the web server to determine if the version of the file cached by the web browser has been unmodified since the last retrieval (ie. if the web browser included an ``ETag`` header), it may instead respond with a request of the form::

```html
    304 Not Modified
    [response headers]
```

and no payload, and the web browser instead retrieves the HTML from its cache.

## Additional Resources

After parsing the HTML, the web browser (and server) repeats this process for every resource (image, CSS, favicon.ico, etc) referenced by the HTML page, except instead of ``GET / HTTP/1.1`` the request will be
``GET /$(URL relative to www.google.com) HTTP/1.1``.

If the HTML referenced a resource on a different domain than ``www.google.com``, the web browser goes back to the steps involved in resolving the other domain, and follows all steps up to this point for that domain. The ``Host`` header in the request will be set to the appropriate server name instead of ``google.com``.

_Demonstration Step:_
* Open Chrome Dev Tools, Network Tab. Walk through Requests and Reponses.

[Next: HTTP Server](./10-HTTPserver.md)