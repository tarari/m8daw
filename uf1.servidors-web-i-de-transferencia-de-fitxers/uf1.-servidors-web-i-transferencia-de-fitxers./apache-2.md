---
description: Servidor HTTP
---

# Apache 2

## Instal·lació

Com a `sudoer`

```text
 apt -y install apache2
```

La configuració resultant del servidor Apache es troba en diferents arxius, sent el principal a **`/etc/apache2/apache2.conf`**

### Concepte de VirtualHost o equip Virtual.

Un servidor apache proveeix servei web potencialment a molts dominis d'internet. Només cal crear un fitxer de "site" al directori `/etc/apache2/sites-available` i configurar adequadament unes quantes línies de directives.

Mirem com quedaria si per exemple creem un fitxer p**rova.conf** que dona servei a un hipotètic domini **prova.local**:

```text
<VirtualHost *:80>
    ServerName prova.local
    ServerAdmin webmaster@prova.local
    DocumentRoot /var/www/prova/public_html
    ErrorLog /var/log/apache2/prova.local.error.log
    CustomLog /var/log/apache2/prova.local.access.log combined
    LogLevel warn
</VirtualHost>
```

Caldria després habilitar el nou virtualhost

```text
a2ensite prova.conf
```

i reiniciar o recarregar la nova configuració

```text
systemctl restart apache2
-o-
systemctl reload apache2
```

Edita, si vols per provar una pàgina de prova index.html al directori que marca el **DocumentRoot `(/var/www/prova/index.html)`**

```markup
<html>
<body>
<div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
Virtual Host Prova
</div>
</body>
</html>
```

Modifiqueu, per provar,  afegint la següent línia al fitxer **`/etc/hosts`**, això ens permet resoldre diversos noms DNS amb la mateixa IP,  provem en local \(127.0.0.1\)

```markup
127.0.0.1     localhost
127.0.0.1     prova.local
```

Al teu navegador local introdueix l'adreça **`http://prova.local`** i comprova.

## Redireccionament cap a lloc segur

Si volem que el noste site ens reenviï cap a lloc segur https, si el tenim implementat, seria ficar aquesta directiva dins la configuració del VirtualHost:

```markup
Redirect permanent / https://domini.com
```

També es pot fer a través de fitxers .htaccess, en cas que no podem modificar el VirtualHost, si habilitem la reescriptura de URL:

```markup
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://domini.com/$1 [L,R=301]
```





