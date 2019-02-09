# Check HSTS list

_Context: Browser is determining how to fetch (what protocol?) the desired resource._
_OSI Layer(s): 7_

* The browser checks its "preloaded HSTS ([HTTP Strict Transport Security](https://tools.ietf.org/html/rfc6797))" list. This is a list of websites that have requested to be contacted via HTTPS only.

* If the website is in the list, the browser sends its request via HTTPS instead of HTTP. Otherwise, the initial request is sent via HTTP.
    * If in the HSTS list the *initial* request will be ``HTTPS`` even though we specified ``HTTP`` as the protocol.

_Demonstration Step:_
  * View HSTS config for google.com in Chrome
    * Launch Chrome net-internals hsts config page.
    ``chrome://net-internals/#hsts``
    * Search for google.com domain in the "Query HSTS/PKP domain" field

[Next: DNS Lookup](./3-DNSlookup.md)