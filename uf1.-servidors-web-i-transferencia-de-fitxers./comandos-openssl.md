# Comandos OpenSSL

La necessitat d'encriptació de les comunicacions pot ser resolta amb aquesta llibreria, que dona suport als certificats i encriptacions assimètriques que s'utilitzen a la web segura \(https\).



**openssl** és un comando en línia per fer servir la llibreria OpenSSL crypto-library des de la consola.

Entre les seves funcions:

```text
 o  Creation and management of private keys, public keys and parameters
 o  Public key cryptographic operations
 o  Creation of X.509 certificates, CSRs and CRLs 
 o  Calculation of Message Digests
 o  Encryption and Decryption with Ciphers
 o  SSL/TLS Client and Server Tests
 o  Handling of S/MIME signed or encrypted mail
 o  Time Stamp requests, generation and verification
```

## Generació de certificats i claus

Generar una nova clau privada i un  Certificate Signing Request \(CSR\)

**`openssl req -out CSR.csr -new -newkey rsa:2048 -nodes keyout privateKey.key`**

Generar un  a certificat auto-signat \(mireu [How to Create and Install an Apache Self Signed Certificate](https://www.sslshopper.com/article-how-to-create-and-install-an-apache-self-signed-certificate.html) per més informació\)

**`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt`**

Generar un _certificate signing request_ \(CSR\) per a una clau privada existent

**`openssl req -out CSR.csr -key privateKey.key -new`**

Generar un CSR basat en certificat existent 

**`openssl x509 -x509 toreq -in certificate.crt -out CSR.csr -signkey privateKey.key`**

Eliminar  un passphrase d'una clau privada

**`openssl rsa -in privateKey.pem -out newPrivateKey.pem`**

## Certificats auto-signats \(sense CSR\)

Instal·lem Apache2

Habilitem SSL

**`a2enmod ssl`**

Creem el certificat auto-signat

Creem el directori **`/etc/apache2/ssl`** on deixar el certificat i la clau privada:

```text
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```







