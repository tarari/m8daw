# Administració de servidors web

L'administració de servidors web és fonamental per a garantir el rendiment, la seguretat i l'eficiència d'aplicacions i serveis web. Veiem alguns aspectes relacionats amb la seva configuració i gestió.

### 1.Configuració avançada del servidor web

La configuració avançada inclou optimitzacions per a millorar el rendiment, la seguretat i la disponibilitat. Alguns exemples són:

* **Tuning del rendiment**: Ajustar paràmetres com la mida de les memòries cau, la compressió de continguts, i l'optimització dels recursos del sistema.
* **Configuració de seguretat**: Implementar mesures com el desactivament de mòduls no necessaris, la configuració de límits de connexió, i la protecció contra atacs DDoS.
* **Alta disponibilitat**: Configurar el servidor per treballar amb balancejadors de càrrega i sistemes de failover.

### 2. Mòduls: instal·lació, configuració i ús

Els servidors web com Apache i Nginx permeten l'extensió de les seves funcionalitats mitjançant mòduls.

* **Apache**: Mòduls com `mod_rewrite` per a la reescriptura d'URL, `mod_security` per a la seguretat, i `mod_ssl` per a suport SSL/TLS.
* **Nginx**: Mòduls com `ngx_http_rewrite_module`, `ngx_http_ssl_module`, i `ngx_http_cache_purge_module`.

### 3 Hosts virtuals. Creació, configuració i utilització

Els hosts virtuals permeten que un sol servidor web pugui servir múltiples llocs web.

* **Apache**: Definir els hosts virtuals en arxius de configuració separats, utilitzant la directiva `VirtualHost`.
* **Nginx**: Utilitzar blocs `server` per definir els diferents llocs web servits pel mateix servidor.

### 4. Autenticació i control d'accés

Aquests mecanismes asseguren que només usuaris autoritzats poden accedir a certs recursos.

* **Apache**: Utilitzar `.htaccess` amb directives com `AuthType`, `AuthName`, `AuthUserFile`, i `Require`.
* **Nginx**: Utilitzar blocs `location` amb directives `auth_basic` i `auth_basic_user_file`.

### 5. El protocol HTTPS

HTTPS és una extensió de HTTP que utilitza SSL/TLS per a xifrar la comunicació.

* **Configuració SSL/TLS**: Generar i configurar els certificats SSL, configurar protocols segurs, i utilitzar directives com `SSLEngine`, `SSLCertificateFile`, i `SSLCertificateKeyFile` en Apache, i `ssl_certificate` i `ssl_certificate_key` en Nginx.

### 6. Certificats. Servidors de certificats

Els certificats són necessaris per establir connexions segures.

* **Tipus de certificats**: Certificats autosignats, certificats emesos per autoritats de certificació (CA), i certificats wildcard.
* **Servidors de certificats**: Configurar i mantenir un servidor de certificació intern, com ara OpenSSL per a generar i gestionar certificats.

### 7. Documentació

Documentar totes les configuracions i canvis és essencial per a la gestió eficient del servidor.

* **Arxius de configuració**: Mantenir-los ben comentats.
* **Procediments**: Documentar passos per a tasques comunes com l'actualització del servidor, la instal·lació de mòduls, i la gestió de certificats.

### 8. Desplegament d'aplicacions sobre servidors web

Els servidors web poden allotjar diferents tipus d'aplicacions.

* **Frameworks i llenguatges**: Configurar suport per a aplicacions PHP, Python (Django, Flask), Ruby (Rails), etc.
* **Desplegament**: Utilitzar eines com `git`, `rsync`, o sistemes de CI/CD com Jenkins per automatitzar el desplegament.

### 9. Desplegament de servidors web mitjançant tecnologies de virtualització al núvol i en contenidors

L'ús de tecnologies de virtualització permet una gestió més flexible i escalable.

* **Virtualització**: Utilitzar hipervisors com VMware, Hyper-V o KVM.
* **Núvol**: Utilitzar serveis com AWS, Google Cloud, o Azure per desplegar servidors web.
* **Contenidors**: Utilitzar Docker per crear i gestionar contenidors que allotgen els servidors web, amb eines com Kubernetes per l'orquestració.

### 10. Conjunts d'eines de gestió de logs. Instal·lació, configuració i utilització, per a l'ajuda a la presa de decisions: Big Data

La gestió de logs és essencial per a la monitorització i anàlisi del rendiment i la seguretat.

* **Eines de logs**: Utilitzar eines com ELK Stack (Elasticsearch, Logstash, Kibana) per a recollir, processar i visualitzar logs.
* **Configuració**: Configurar els servidors web per enviar logs a aquestes eines.
* **Anàlisi de dades**: Utilitzar tècniques de Big Data per a extreure informació valuosa dels logs i ajudar en la presa de decisions.

Cada un d'aquests punts és fonamental per a una administració eficient i segura dels servidors web, assegurant que els serveis siguin fiables, ràpids i segurs per als usuaris finals.
