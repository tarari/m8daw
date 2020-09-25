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

```text
sudo apt update
```

A continuació, instal el paquet `apache2`:

```text
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

```text
sudo apt install curl
```

Després, utilitzeu `curl`per recuperar icanhazip.com mitjançant IPv4:

```text
curl -4 icanhazip.com
```

Quan tinguem l'adreça IP del seu servidor, introduim  a la barra d'adreces del  navegador:

```text
http://IP
```

Hauria de veure la pàgina web per defecte d'Apache de Debian.

#### Administrar el procés de Apache

Ara el servidor web funciona, repassem alguns **comandaments d'administració bàsics**.

Per aturar el servidor web, escrivim el següent:

```text
sudo systemctl stop apache2
```

Per iniciar el servidor web quan s'aturi, escrivim el següent:

```text
sudo systemctl start apache2
```

Per aturar i després iniciar el servei de nou, escrivim el següent:

```text
sudo systemctl restart apache2
```

Si només realitza canvis de configuració, Apache sovint pot recarregar sense tancar connexions. Per fer-ho, utilitzem aquesta comanda:

```text
sudo systemctl reload apache2
```

Per defecte, Apache està configurat per a iniciar-se automàticament quan el servidor ho fa. Si no és el que vol, desactivem aquest comportament escrivint el següent:

```text
sudo systemctl disable apache2
```

Per tornar a habilitar el servei de manera que es carregui en l'inici, escrivim el següent:

```text
sudo systemctl enable apache2
```

Ara, Apache hauria d'iniciar de forma automàtica quan el servidor ho faci de nou.

## Servidors ftp

Un servidor ftp és també un servidor de fitxers, de qualsevol fitxer.

## PureFTPd

## Avantatges del servidor PureFTPd

Algunes de les seves característiques més notables són:

* Usuaris virtuals
* Gestió de l'ample de banda i d'espai en disc per usuari
* Directoris personals chroot\(\)
* Estadístiques en temps real a Text, HTML o XML
* autentificació d'usuaris amb MySQL, PostgreSQL, LDAP , ...
* Opcions avançades de seguretat

Podríem citar que s'utilitza molt, per exemple en el FTP públic de RedIris\(ftp://ftp.rediris.es\).

## Instal·lació del servidor FTP PureFTPd

### **Descàrrega i instal·lació de l'aplicació**

[Pàgina Oficial de PureFTPd](http://www.pureftpd.org/project/pure-ftpd)

_\# Instal·lació de l'aplicació_  


```text
apt install pure-ftpd
```

### **Rutes i fitxers de configuració**

```bash
# Directori de configuracions del servidor
/etc/pure-ftpd/conf
# Fitxer de contrasenyes d'usuaris virtuals.
/etc/pure-ftpd/pureftpd.pdb
# Fitxer de configuració de funcionament del PureFTPd
/etc/default/pure-ftpd-common
```

### **Accés Anònim**

Per donar accés anònim al FTP haurem de tenir un compte del sistema anomenada 'ftp'. No li donarem cap shell vàlid, simplement un directori home de treball. Aquest directori serà el que es farà servir com a directori anònim. Vegeu també les directives **NoAnonymous** i **AnonymousOnly** en el directori _`/etc/pure-ftpd/conf`._

```bash
# Creem un usuari anomenat ftp sense shell i amb directori /var/ftp.
# El directori home d'aquest usuari, serà el directori dels anònims.
adduser ftp --shell /sbin/nologin --home /var/ftp
# Revisarem les directives:
/etc/pure-ftpd/conf/AnonymousOnly
# Si està a yes només permet accessos anònims.
/etc/pure-ftpd/conf/NoAnonymous
# Si està a yes només permet accés a usuaris autenticat.
# Si està a no permetrà l'accés a usuari anònims també.
# Per accelerar la connexió al servidor, podem desactivar la resolució inversa
# Per a això vam crear una directiva DontResolve
echo "yes"> /etc/pure-ftpd/conf/DontResolve
```

\_\_

### **Directives de configuració**

* Per introduir les directives de configuració es poden crear una a una en la carpeta **/etc/pure-ftpd/conf** creant un _fitxer amb el nom de la directiva_ \( començament de cada paraula en majúscules\) i el contingut corresponent.
* Una altra opció és ficar la directiva dins del fitxer **/etc/default/**pure-ftpd-common. La directiva haurà d'anar en majúscules i amb el valor correponent. Per exemple: **DONTRESOLVE = true**

#### **Autenticació**

Al servidor pureftpd podrem configurar els modes d'autenticació disponibles per accedir-hi. Una cosa que hem de fer és configurar si volem fer servir els **usuaris virtuals** \(usuaris del servei però no del sistema\)**,** i per a això hem de indicar-li que utilitzi en autenticació el fitxer de base de dades que conté aquests usuaris.

_\# Atenció: aquesta configuració la farem quan anem a treballar amb usuaris virtuals._  
_\# Si no hem creat usuaris virtuals la base de dades no existirà i donarà error a l'arrencar pureftpd._

_\# Accedim al directori d'autenticació:_  
cd /etc/pure-ftpd/auth

_\# Creem un enllaç simbòlic a la informació d'on es troba la base de dades._  
_\# En indicar 50 ... estem indicant la prioritat en l'autenticació._  
ln -s ../conf/PureDB 50pure

#### **Altres directives**

Directives de configuració més importants que utilitzarem.

Les directives de configuració, són fitxers que es troben al directori:

/etc/pure-ftpd/conf  


Si alguna de les directives esmentades a continuació no existeix, hi haurem de crear un fitxer amb el nom d'aquesta directiva i emmagatzemar dins d'ell, els paràmetres corresponents a aquesta directiva.

Una de les característiques que volem, és que els usuaris no puguin sortir del seu directori home:

**ChrootEveryone yes**  
  
_\# Si aquesta directiva no està creada la crearem amb:_  
nano /etc/pure-ftpd/conf/ChrootEveryone

_\# I com a contingut del fitxer escriurem :_  
yes

_\# O tambiém podem fer el mateix amb les instrucció:_  
echo "yes"&gt;/etc/pure-ftpd/conf/ChrootEveryone

Una altra de les característiques que ha de posseir el servidor ftp és que disposi d'una zona de descàrrega pública \(usuaris anonymous\). Per a això hem d'acceptar connexions anònimes, amb el que hi ha d'haver la següent línia: **NoAnonymous no**

echo "no"&gt; /etc/pure-ftpd/conf/NoAnonymous  


Si volem que només permeti l'accés a usuaris anònims haurem de posar també la directiva:

echo "yes"&gt; / etc / pure-ftpd / conf / AnonymousOnly  


Si volem tenir **usuaris virtuals** \(seran usuaris registrats, però que no tenen compte de shell en el sistema\), hem d'assegurar que la línia a continuació existeix i no està comentada.

Aquesta línia indica la localització del fitxer d'usuaris PureDB:

more /etc/pure-ftpd/conf/PureDB

_\# Mostrarà la ruta de la base de dades d'usuaris virtuals:_  
/etc/pure-ftpd/pureftpd.pdb

Per evitar que algun usuari per distracció \(o maliciosament\) ens pugui omplir el servidor de fitxers, activarem uns **límits** màxims:

per exemple podríem posar una Quota límit de 400 fitxers i 50 MB:

echo "400 50"&gt;/etc/pure-ftpd /conf/Quota  


Si volem que automàticament es creuen els directoris home dels usuaris, la primera vegada que es loguean ho farem amb:

echo "yes"&gt; /etc/pure-ftpd/conf/CreateHomeDir  


Per posar màscares per defecte s'utilitza la directiva **umask.**En aquesta directiva s'indica mitjançant dos nombres **separats per un espai** els permisos per a fitxers i per directoris.

Per calcular-es resta a **777-umask = permisos finals**

Per exemple:

_\# 220 -&gt; umask per a fitxers_  
_\# 444 -&gt; umask per directoris_  
echo "220.444"&gt; /etc/pure-ftpd /conf /umask

_\# Ens dóna per defecte:_  
Fitxers: -r-xr-xrwx  
Directoris: d-wx-wx-wx

**Més Directives de configuració**

Es mostren aquí dos enllaços a pàgines amb informació de directives de configuració per Pure-FTPd:

* [directives configuració en Wiki de Pure-FTPd](http://wiki.openwrt.org/doc/uci/pure-ftpd)
* [Una altra pàgina amb directives de configuració](http://praxis.edoceo.com/howto/pure-ftpd)

### **usuaris**

Els usuaris virtuals és un simple mecanisme que ens permetrà emmagatzemar una llista d'usuaris, les seves contrasenyes, noms, uid, directoris, etc. És com el fitxer /etc/passwd de Linux, però en aquest cas, és només per a l'ús del servei FTP.

Això vol dir que fàcilment podem crear comptes de FTP, sense barrejar-les amb els usuaris del sistema.

Addicionalment, els usuaris virtuals poden disposar de quotes individuals, ràtios, ample de banda, etc. Els comptes del sistema no permeten fer això.

Podem tancar els usuaris virtuals en la seva gàbia : chroot, per fer-ho editem el fitxer **/etc/default/pure-ftpd-common**

**VIRTUALCHROOT= true**

#### **Creació d'usuaris virtuals**

Quan vam crear un usuari virtual haurem de associar-li un uid: identificador d'usuari en el sistema, i per això el millor és crear un compte d'usuari que sigui compartida per tots els usuaris virtuals. Una bona pràctica per fer això, abans de crear usuaris virtuals, és crear un usuari del sistema, com ara **ftpuser** que no tingui accés al mateix:

Per crear aquest compte ho farem de la següent manera:

_\# Primer crearem un grup ftpgroup per als usuaris FTP:_  
groupadd ftpgroup

_\# a continuació vam crear el compte ftpuser:_  
useradd -g ftpgroup -d /dev/null -s /bin/nologin ftpuser

a partir d'ara quan afegim usuaris al pure-ftpd, li podrem indicar que l'usuari del sistema associat és ftpuser, i dir-li que faci la carpeta d'aquest usuari dins de /home/ftpuser/.

Haurem crear la carpeta / home / ftpuser / prèviament. Les carpetes de cada usuari individual es crearan automàticament si tenim la directiva **CreateHomedir a yes.**

_\# Creem la carpeta per als usuaris virtuals:_  
mkdir /home/ftpuser

_\# Li posem com a usuari i propietari ftpuser.ftpgroup:_  
chown ftpuser.ftpgroup /home/ftpuser

_\# Donem permisos perquè pure-ftpd pugui escriure en aquest directori i crear els home :_  
chmod 777 /home/ftpuser

La gestió dels usuaris es realitza amb la comanda **pure-pw.**Aquest ens permet crear, modificar, esborrar i mostrar els usuaris virtuals. També es pot fer el mateix editant directament el fitxer **/etc/pure-ftpd/pureftpd.passwd,**però es recomana l'ús de la comanda per la seva major senzillesa.

Per veure tots els paràmetres disponibles, executarem:

pure-pw --help  


Per exemple podríem crear un usuari "adolfo" el directori fos / home / adolfo:

_\# -u: per indicar el uid d'aquest usuari_  
_\# -d: indica la carpeta home d'aquest usuari_  
pure-pw useradd adolfo -u ftpuser -d /home/ftpuser/adolfo

_\# Haurem d'escriure el password per a aquest usuari adolfo 2 cops._

_\# Amb el paràmetre -d l'usuari adolfo estarà chrooted._  
_\# Si volem que tingui accés a tot el sistema escriurem -D en lloc de -d._

Recordar-vos que no cal crear el directori d'aquest usuari si tenim la directiva **CreateHomeDir** a **yes** en la configuració de pure-ftpd.

Cal recordar que després d'haver realitzat qualsevol canvi relatiu als usuaris, haurem **d'aplicar ells canvis a la base de** dades.Per a això executarem:

pure-pw mkdb  


#### **Modificació d'usuaris virtuals**

Un cop tenim els usuaris virtuals creats, podrem editar la seva informació. Per exemple modificar-seu ample de banda, canviar quota, la seva ràtio, nom complet, etc.

La comanda pure-pw usermod funciona com pure-pw useradd, excepte que modifica la informació existent d'un compte en lloc de crear una altra nueva.Por exemple, volem afegir-li a adolfo 1 quota. Adolfo va tenir limitat a 30 fitxers i 10 megabytes de capacitat.

_\# -n: nombre màxim de fitxers_  
_\# N: espai màxim en MBytes_  
pure-pw usermod adolfo -n 30 -N 10  


#### **resetejat d'atributs**

To disable file quotes, utilitzeu pure-pw usermod &lt;user&gt; -n ''  
To disable size quotes, utilitzeu pure-pw usermod &lt;user&gt; -N ''  
To disable ràtios, utilitzeu pure-pw usermod &lt;user&gt; -q '' -Q ''  
To disable download bandwidth throttling, utilitzeu pure-pw usermod &lt;user&gt; -t ''  
To disable upload bandwidth throttling, utilitzeu pure-pw usermod &lt;user&gt; T ''  
To disable IP filtering, utilitzeu pure-pw usermod &lt;user&gt; &lt;-i, -I, -r or -R&gt; ''  
To disable time restrictions, utilitzeu pure-pw usermod &lt;user&gt; -z ''  
To disable the number of concurrent sessions, utilitzeu pure-pw usermod &lt;user&gt; -i''  


#### **Esborrat d'usuaris virtuals**

Per esborrar un usuari haurem d'executar:

pure-pw userdel &lt;login&gt; \[-f&lt;passwdfile&gt;\] \[-m\]_\# Si volem esborrar adolfo:_  
pure-pw userdel adolfo

_\# Atenció: el seu directori personal no s'esborrarà._  
_\# Haurem de esborrar-a mà:_  
rm -rf / home / ftpusuarios / adolfo

#### **Modificació de contrasenyes**

Per modificar la contrasenya d'un usuari:

pure-pw passwd &lt;login&gt; \[-f&lt;passwdfile&gt;\] \[-m\]

_\# Per exemple per adolfo:_  
pure-pw passwd adolfo

_\# Recordeu que per aplicar canvis farem:_  
pure-pw mkdb

#### **Consulta d'informació d'usuari**

Per consultar la informació d'un usuari ho farem amb:

pure-pw show login

_\# Per exemple per adolfo:_  
pure-pw show adolfo

#### **Més paràmetres sobre la gestió d'usuaris**

Es recomana consultar l'ajuda en la línia de comandes amb:

man pure-pw  


**gestió del servei**

per reiniciar el servei pure-ftpd:

service pure-ftpd restart  


per veure la llista d'usuaris que estan connectats al FTP:

pure-ftpwho

