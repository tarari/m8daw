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

