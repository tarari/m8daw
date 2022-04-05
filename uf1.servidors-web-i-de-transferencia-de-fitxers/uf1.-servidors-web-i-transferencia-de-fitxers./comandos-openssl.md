# Comandos OpenSSL

La necessitat d'encriptació de les comunicacions pot ser resolta amb aquesta llibreria, que dona suport als certificats i encriptacions assimètriques que s'utilitzen a la web segura (https).



**openssl** és un comando en línia per fer servir la llibreria OpenSSL crypto-library des de la consola.

Entre les seves funcions:

```
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

Generar una nova clau privada i un  Certificate Signing Request (CSR)

**`openssl req -out CSR.csr -new -newkey rsa:2048 -nodes keyout privateKey.key`**

Generar un  a certificat auto-signat (mireu [How to Create and Install an Apache Self Signed Certificate](https://www.sslshopper.com/article-how-to-create-and-install-an-apache-self-signed-certificate.html) per més informació)

**`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt`**

Generar un _certificate signing request_ (CSR) per a una clau privada existent

**`openssl req -out CSR.csr -key privateKey.key -new`**

Generar un CSR basat en certificat existent&#x20;

**`openssl x509 -x509 toreq -in certificate.crt -out CSR.csr -signkey privateKey.key`**

Eliminar  un passphrase d'una clau privada

**`openssl rsa -in privateKey.pem -out newPrivateKey.pem`**

## Certificats auto-signats (sense CSR)

Instal·lem Apache2

Habilitem SSL

**`a2enmod ssl`**

Creem el certificat auto-signat

Creem el directori **`/etc/apache2/ssl`** on deixar el certificat i la clau privada:

Generem clau privada en primer lloc:\


```bash
/etc/apache2/ssl> sudo openssl genrsa -aes128 -out domini.key 2048
Generating RSA private key, 2048 bit long modulus
......+++
....................................................................+++
e is 65537 (0x010001)
Enter pass phrase for server.key:              # password
Verifying - Enter pass phrase for server.key:  # confirma
```

Eliminem passphrase:

```
/etc/apache2/ssl> openssl rsa -in domini.key -out domini.key
Enter pass phrase for server.key:     # passphrase set above
writing RSA key
```

Creem el CSR, pas previ al certificat, és el fitxer que enviem a l'entitat certificadora CA.

```bash
/etc/apache2/ssl > openssl req -new -days 3650 -key server.key -out server.csr
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:ES   # pais
State or Province Name (full name) [Some-State]:BCN   # state
Locality Name (eg, city) []:Castelldefels  # ciutat
Organization Name (eg, company) []: Company   # companyia
Organizational Unit Name (eg, section) []:Informatica   # departament
Common Name (e.g. server FQDN or YOUR name) []:domini.com   # FQDN (ServerName)
Email Address []:webmaster@domini   # admin email

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:

```

Crear CRT a partir del CSR i de la clau privada

```bash
/etc/apache2/ssl > openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 3650
Signature ok
subject=C = ES, ST = BCN, L = Castelldefels, O = Company, OU = Informatica, CN = domini.com, emailAddress = webmaster@domini
Getting Private key
```

