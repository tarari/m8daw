---
description: >-
  En aquesta unitat formativa, analitzarem els procesos de transferència de
  fitxers a través de servies FTP i  estudiarem els protocols HTTP que donen
  suport als servidors web.
---

# UF1. Servidors web i transferència de fitxers.

## Servidors web

Un servidor web és un servidor especialitzat de fitxers **html**. S'afegeixen mòduls que permeten donar caracterítiques addicionals, com ara preprocessar PHP.

### Servidor Apache2

#### Instal·lar Apache

Apache està disponible dins dels repositoris de programari per defecte de Debian, el que permet instal·lar-utilitzant eines convencionals d'administració de paquets.

Comencem actualitzant l'índex de paquets locals perquè reflecteixin els canvis anteriors:

```
sudo apt update
```

A continuació, instal el paquet `apache2`:

```
sudo apt install apache2
```

Un cop confirmada la instal·lació, `apt`s'instal·larà Apache i totes les dependències necessàries.

#### Comprovar el seu servidor web

Al final del procés d'instal·lació, Debian inicia Apache. El servidor web ja hauria d'estar en funcionament.

Fem una verificació amb el sistema `systemd init` per saber si es troba en execució el servei escrivint el següent:

```bash
sudo systemctl status apache2
```

```bash
Output● apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2018-09-05 19:21:48 UTC; 13min ago
 Main PID: 12849 (apache2)
   CGroup: /system.slice/apache2.service
           ├─12849 /usr/sbin/apache2 -k start
           ├─12850 /usr/sbin/apache2 -k start
           └─12852 /usr/sbin/apache2 -k start

Sep 05 19:21:48 apache systemd[1]: Starting The Apache HTTP Server...
Sep 05 19:21:48 apache systemd[1]: Started The Apache HTTP Server.
```

Com pot veure en aquest resultat, sembla que el servei es va iniciar correctament. No obstant això, la millor manera de comprovar-ho és sol·licitar una pàgina d'Apache.

Es pot accedir a la pàgina de destinació per defecte d'Apache per confirmar que el programari funcioni correctament mitjançant la seva IP: Si no coneix l'adreça IP del seu servidor, pot obtenir-la de diverses formes des de la línia d'ordres.

Proveu escriure això en la línia d'ordres del seu servidor:

```bash
hostname -I
```

Obtindrem algunes adreces separades per espais. Podeu provar cadascuna d'elles en el seu navegador web per veure si funcionen.

Una alternativa és utilitzar l'eina `curl`, que hauria de proporcionar la seva adreça IP pública tal com es veu des d'una altra ubicació a Internet.

Primer, instal `curl`utilitzant `apt`:

```
sudo apt install curl
```

Després, utilitzeu `curl`per recuperar icanhazip.com mitjançant IPv4:

```
curl -4 icanhazip.com
```

Quan tinguem l'adreça IP del seu servidor, introduim  a la barra d'adreces del  navegador:

```
http://IP
```

Hauria de veure la pàgina web per defecte d'Apache de Debian.

#### Administrar el procés de Apache

Ara el servidor web funciona, repassem alguns **comandaments d'administració bàsics**.

Per aturar el servidor web, escrivim el següent:

```
sudo systemctl stop apache2
```

Per iniciar el servidor web quan s'aturi, escrivim el següent:

```
sudo systemctl start apache2
```

Per aturar i després iniciar el servei de nou, escrivim el següent:

```
sudo systemctl restart apache2
```

Si només realitza canvis de configuració, Apache sovint pot recarregar sense tancar connexions. Per fer-ho, utilitzem aquesta comanda:

```
sudo systemctl reload apache2
```

Per defecte, Apache està configurat per a iniciar-se automàticament quan el servidor ho fa. Si no és el que vol, desactivem aquest comportament escrivint el següent:

```
sudo systemctl disable apache2
```

Per tornar a habilitar el servei de manera que es carregui en l'inici, escrivim el següent:

```
sudo systemctl enable apache2
```

Ara, Apache hauria d'iniciar de forma automàtica quan el servidor ho faci de nou.

#### Configurar hosts virtuals

Quan fem servir el servidor web **Apache**, és recomanable utilitzar **`_hosts virtuals`** \_ (similars als blocs de servidor de Nginx) per encapsular detalls de configuració i **allotjar més d'un domini des d'un únic servidor**. Configurarem un domini anomenat **exemple.com** , però haurem de **canviar-lo pel  propi nom de domini DNS** .&#x20;

Per defecte, Apache 2 en Debian  té habilitat un bloc de servidor que està configurat per a proporcionar documents de directori `/var/www/html`. Si bé, això funciona bé per a un sol lloc, pot ser difícil de manejar si allotgem diversos dominis (hosting compartit). En comptes de modificar `/var/www/html`, crearem una estructura de directori dins `/var/www`per al nostre lloc **exemple.com** i deixarem `/var/www/html`com a directori per defecte que es proveirà si una sol·licitud de client no coincideix amb altres llocs.

Creem el directori per **exemple.com** , utilitzant l'indicador `-p`per crear qualsevol directori principal necessari si no està construit:

```
sudo mkdir -p /var/www/exemple.com/html
```

A continuació, assignem la propietat de directori amb la variable d'entorn `$USER`:

```
sudo chown -R $USER:$USER /var/www/example.com/html
```

Els permisos de les seves _root web_ han de ser correctes sinó hem canviat el seu valor `unmask`, però podem comprovar-escrivint el següent:

```
sudo chmod -R 755 /var/www/exemple.com
```

A continuació, creem una pàgina d'exemple `index.html`utilitzant `nano o pico`o el vostre editor favorit:

```
pico /var/www/exemple.com/html/index.html
```

Dins d'ella, afegim el següent exemple d'HTML:/var/www/exemple.com/html/index.html

```
<html>
    <head>
        <title>Welcome!</title>
    </head>
    <body>
        <h1>OK!  Tot correcte!</h1>
    </body>
</html>
```

Desem i tanquem el fitxer quan acabi.

Perquè Apache proporcioni aquest contingut, cal crear un arxiu de host virtual amb les directives correctes. En lloc de modificar el fitxer de configuració per defecte situat a `/etc/apache2/sites-available/000-default.conf`directament, crearem un de nou a :`/etc/apache2/sites-available/exemple.com.conf`

```
sudo pico /etc/apache2/sites-available/exemple.com.conf
```

Enganxem en el següent bloc de configuració, similar a l'predeterminat, però actualitzat per al nostre nou directori i nom de domini:/etc/apache2/sites-available/exemple.com.conf

```
<VirtualHost *:80>
    ServerAdmin admin@exemple.com
    ServerName exemple.com
    ServerAlias www.exemple.com
    DocumentRoot /var/www/exemple.com/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Recordem que vam canviar **`DocumentRoot`**pel nostre nou directori i _`ServerAdmin`_per un correu electrònic a què pugui accedir l'administrador de el lloc **exemple.com** . També afegim dues directives: **`ServerName`**, que estableix el domini de base que hauria de coincidir per a aquesta definició d'amfitrió virtual, i **ServerAlias**, que defineix més noms que haurien de coincidir com si fossin el nom de base.

Desem i tanquem el fitxer quan acabem.

Habilitarem l'arxiu amb l'eina **`a2ensite`**:

```bash
sudo a2ensite exemple.com.conf
```

Deshabilitem el lloc predeterminat definit en `000-default.conf`:

```bash
sudo a2dissite 000-default.conf
```

A continuació, farem una prova per veure que no hi hagi errors de configuració:

```
sudo apache2ctl configtest
```

Hauríem de veure el següent resultat:

```
OutputSyntax OK
```

Reiniciem Apache per implementar els seus canvis:

```
sudo systemctl restart apache2
```

Amb això, Apache2 hauria de ser el servidor del teu nom de domini. Podem provar això visitant . Allà, hauria de veure alguna cosa com el següent:`http://exemple.com`\


{% hint style="info" %}
Atenció. En cas de ser prova local, cal configurar **`/etc/hosts`** per tal que reconegui el ServerName. Afegim la línia:

**`127.0.1.1      exemple.com`**
{% endhint %}

##
