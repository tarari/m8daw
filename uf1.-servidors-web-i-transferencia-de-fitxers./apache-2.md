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

Un servidor apache proveeix servei web potencialment a molts dominis d'internet \(ServerName\) 

