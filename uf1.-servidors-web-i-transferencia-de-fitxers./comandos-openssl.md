# Comandos OpenSSL

La necessitat d'encriptació de les comunicacions pot ser resolta amb aquesta llibreria, que dona suport als certificats i encriptacions assimètriques que s'utilitzen a la web segura \(https\).

## Generació de certificats i claus

Generar una nova clau privada i un  Certificate Signing Request \(CSR\)

**`openssl req -out CSR.csr -new -newkey rsa:2048 -nodes keyout privateKey.key`**

Generar un  a certificat auto-signat \(mireu [How to Create and Install an Apache Self Signed Certificate](https://www.sslshopper.com/article-how-to-create-and-install-an-apache-self-signed-certificate.html) per més informació\)

**`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt`**

Generar un _certificate signing request_ \(CSR\) per a una clau privada existent

* openssl req -out CSR.csr -key privateKey.key -new

Generate a certificate signing request based on an existing certificate

* openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key

Remove a passphrase from a private key

* openssl rsa -in privateKey.pem -out newPrivateKey.pem
