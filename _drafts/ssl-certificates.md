# Information here

## Tools

- openssl
- cfssl (cloudflare)

## OpenSSL

Homepage: xxx

#### Certificate Authority Keys

1) Generate private key: ca.key
````bash
$ openssl genrsa -out ca.key 2048
````
Recommended: Add "-des3" to encrypt the key with a password

2) Generate self-signed certificate: ca.pem (ca.crt)
````bash
openssl req -x509 -new -nodes -key ca.key -sha256 -days 1825 -out ca.pem
````
- "-x509" : output x509
- "-new" : new request
- "-nodes" : no des-encryption (password)
- "-key" : private key for creating certificate
- "-sha256" : private key format
- "-days" : how long is the certificate valid for
- "-out" : filename for output

Answer at minimum the following question(s):
- Common Name (Example: contoso.org)

This public root-certificate (ca.pem) should be installed on all devices that will use your self-signed certificates

#### Server Keys

1) Generate private key: example.key
````bash
$ openssl genrsa -out example.key 2048
````

2) Generate certificate-signing-request: server.csr
````bash
openssl req -new -key example.key -out example.csr
````
NOTE: This contains public key (derived from private key) and required information

!SAN replaces CN!

3) Create SAN configuration file example.cnf

4) Sign server.csr with ca.key & ca.crt: server.crt / server.pem
````bash
openssl x509 -req -extensions v3_req -days 365 -in example.csr -CAkey ca.key -CA ca.pem -CAcreateserial -out example.crt -sha256 -extfile example.cnf
````
## CFSSL

Homepage:

#### Certificate Authority
...
