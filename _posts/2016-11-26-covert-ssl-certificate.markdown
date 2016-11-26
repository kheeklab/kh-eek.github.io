---
published: true
title: covert SSL certificate 
layout: post
---
#### get private key from PK12 certificate 
```openssl pkcs12 -in DOMAIN.p12 -out DOMAIN.key.pem -nocerts -nodes```

##### remove passprase from private key
```openssl rsa -in DOMAIN-pass.key.pem -out DOMAIN.key.pem```

#### get certificate DER from PK12
```openssl pkcs12 -in DOMAIN.p12 -out DOMAIN.crt.pem -clcerts -nokeys``` 
```openssl x509 -inform der -in DOMAIN.crt.pem -out DOMAIN.pem```
