---
description: Estudiem nginx a través d'un exemple
---

# Servidors nginx

Per configurar dos llocs web amb nginx, un de nom "library.local" que doni suport a una aplicació PHP amb php-fpm i un altre de nom "rapid.local" que doni suport a una aplicació Java amb proxy, es pot utilitzar la següent configuració:

```
server {
    listen 80;
    server_name library.local;

    root /var/www/library;
    index index.php;

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}

server {
    listen 80;
    server_name rapid.local;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

```

En aquesta configuració, s'estableixen dos blocs de servidor, un per a cada lloc web. El primer servidor escolta el port 80 i estableix el nom de servidor com "library.local". La ubicació de l'arrel del lloc web és "var/www/library" i l'arxiu d'índex és "index.php". Aquest servidor també configura una ubicació per a arxius PHP que utilitza un passador fastcgi per a php-fpm. El segon servidor també escolta el port 80 i estableix el nom de servidor com "rapid.local". Aquest servidor configura una ubicació que utilitza proxy\_pass per redirigir les sol·licituds a una aplicació Java en execució en el servidor local.

Nota: Aquesta configuració és un exemple bàsic, i es pot modificar segons les necessitats específiques de la aplicació.

### Balanceig de càrrega

Per afegir balanceig de càrrega i protocols HTTPS a la configuració anterior, es pot fer el següent:

* Utilitzar un equilibrador de càrrega, com ara nginx o HAProxy, per distribuir les sol·licituds entre diferents servidors backend. Per fer això, es pot afegir una nova ubicació per al balancejador de càrrega i configurar-lo per a que redirigeixi les sol·licituds a diferents servidors backend.

```
http {
    upstream backend {
        server backend1.example.com;
        server backend2.example.com;
    }

    server {
        listen 80;
        server_name example.com;

        location / {
            proxy_pass http://backend;
        }
    }
}

```

* Configurar un certificat SSL per a cada nom de domini i habilitar el protocol HTTPS per al servidor. Això pot ser fet afegint una nova ubicació per al protocol HTTPS i configurant-lo per a que redirigeixi les sol·licituds a un certificat i una clau privada específics.

```
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /etc/nginx/ssl/example.com.crt;
    ssl_certificate_key /etc/nginx/ssl/example.com.key;

    location / {
        proxy_pass http://backend;
    }
}

```

1. Utilitzar una extensió com a Let's Encrypt per obtenir i renovar automàticament els certificats SSL.

Nota: Aquesta configuració és un exemple bàsic, i es pot modificar segons les necessitats específiques de la aplicació.



