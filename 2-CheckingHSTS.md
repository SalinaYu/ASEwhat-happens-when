# Check HSTS list

* The browser checks its "preloaded HSTS ([HTTP Strict Transport Security](https://tools.ietf.org/html/rfc6797))" list. This is a list of websites that have requested to be contacted via HTTPS only.

* If the website is in the list, the browser sends its request via HTTPS instead of HTTP. Otherwise, the initial request is sent via HTTP.

_Demo: View HSTS config for google.com in Chrome_
* Launch Chrome net-internals hsts config page.
``chrome://net-internals/#hsts``
* Search for google.com domain in the 'Query HSTS/PKP domain' field

[DNS Lookup](./3-DNSlookup.md)