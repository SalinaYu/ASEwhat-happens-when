# TLS handshake

_Context: Once the 3WH is complete, the source and destination start passing substantive traffic._

Our initial request was HTTPS which means its encrypted using TLS (earlier version were called ``SSL``). We now need to negotiate a TLS connection which will be used for the duration of the session.

![TLS Handshake](https://www.ibm.com/support/knowledgecenter/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10660a.gif)

* The client computer sends a ``ClientHello`` message to the server with its Transport Layer Security (TLS) version, list of cipher algorithms, and compression methods available.

* The server replies with a ``ServerHello`` message to the client with the TLS version, selected cipher, selected compression methods and the server's public certificate signed by a CA (Certificate Authority). The certificate contains a public key that will be used by the client to encrypt the rest of the handshake until a symmetric key can be agreed upon.

* The client verifies the server digital certificate against its list of trusted CAs. If trust can be established based on the CA, the client generates a string of pseudo-random bytes and encrypts this with the server's public key. These random bytes can be used to determine the symmetric key.

* The server decrypts the random bytes using its private key and uses these bytes to generate its own copy of the symmetric master key.

* The client sends a ``Finished`` message to the server, encrypting a hash of the transmission up to this point with the symmetric key.

* The server generates its own hash, and then decrypts the client-sent hash to verify that it matches. If it does, it sends its own ``Finished`` message to the client, also encrypted with the symmetric key.

* From now on the TLS session transmits the application (HTTP) data encrypted with the agreed symmetric key -- and we can't look at the application data in Wireshark unless we decrypt the capture with the session key.

_Demostration Steps:_
* Show the steps of the TLS handshake in the Wireshark capture.

[HTTP Protocol](./9-HTTPproto.md)