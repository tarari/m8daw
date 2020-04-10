---
description: >-
  Estudiarem casos pràctics de control de versions d'aplicacions i les seves
  eines git i Github.
---

# Git i workflow

## Introducció a git <a id="introduccion-a-git"></a>

Git és un sistema de control de versions distribuït que es diferencia de la resta en la manera en què modela les seves dades. La majoria dels altres sistemes emmagatzemen la informació com una llista de canvis en els arxius, mentre que Git modela les seves dades més com un conjunt d'instantànies d'un mini sistema d'arxius.

![Model de dades dels sistemes distribu&#xEF;ts tradicionals](https://aulasoftwarelibre.github.io/taller-de-git/images/distribuido-tradicional.png)

![Model de dades de Git](https://aulasoftwarelibre.github.io/taller-de-git/images/distribuido-git.png)

### Els tres estats  <a id="los-tres-estados"></a>

Git té tres estats principals en què es poden trobar els teus arxius: confirmat \(Committed\), modificat \(modified\), i preparat \(staged\). Confirmat vol dir que les dades estan emmagatzemades de manera segura en la teva base de dades local. Modificat vol dir que has modificat l'arxiu però encara no ho has confirmat a la teva base de dades. Preparat vol dir que has marcat un arxiu modificat en la seva versió actual perquè vagi en la teva propera confirmació.

Això ens porta a les tres seccions principals d'un projecte de Git: directori de Git \(Git directory\), el directori de treball \(working directory\), i l'àrea de preparació \(staging area\).

![ Directori de treball, &#xE0;rea de preparaci&#xF3;, i directori de Git ](https://aulasoftwarelibre.github.io/taller-de-git/images/git-estados.png)

### Fluxos de treball distribuïts amb git  <a id="flujos-de-trabajo-distribuidos-con-git"></a>

Hem vist en què consisteix un entorn de control de versions distribuït, però més enllà de la simple definició, hi ha més d'una manera de gestionar els repositoris. Aquests són els fluxos de treball més comuns en Git.

#### Flux de treball centralitzat  <a id="flujo-de-trabajo-centralizado"></a>

Hi ha un únic repositori o punt central que guarda el codi i tothom sincronitza el seu treball amb ell. Si dos desenvolupadors clonen des del punt central, i tots dos fan canvis; tan sols el primer d'ells en enviar els seus canvis de tornada ho podrà fer netament. El segon desenvolupador haurà de fusionar prèviament el seu treball amb el de el primer, abans d'enviar, per evitar el sobreescriure els canvis de el primer

![ Flux de treball centralitzat ](https://aulasoftwarelibre.github.io/taller-de-git/images/flujo-centralizado.png)

#### Flux de treball de l'Gestor-de-Integracions  <a id="flujo-de-trabajo-del-gestor-de-integraciones"></a>

A l'permetre múltiples repositoris remots, en Git és possible tenir un flux de treball on cada desenvolupador tingui accés d'escriptura al seu propi repositori públic i accés de lectura als repositoris de tots els altres. Habitualment, aquest escenari sol incloure un repositori canònic, representant "oficial" de el projecte.

![ Flux de treball de l&apos;Gestor-de-Integracions ](https://aulasoftwarelibre.github.io/taller-de-git/images/flujo-integracion.png)

Informació

Aquest model es va posar molt de moda arran de la forja GitHub que es veurà més endavant.

#### Flux de treball amb Dictador i tinents  <a id="flujo-de-trabajo-con-dictador-y-tenientes"></a>

És una variant de el flux de treball amb múltiples repositoris. S'utilitza generalment en projectes molt grans, amb centenars de col·laboradors. Un exemple molt conegut és el de el nucli de Linux. Uns gestors d'integració s'encarreguen de parts concretes de l'repositori; i s'anomenen tinents. Tots els tinents rendeixen comptes a un gestor d'integració; conegut com el dictador benvolent. El repositori de l'dictador benevolent és el repositori de referència, de què recuperen \(pull\) tots els col·laboradors.

![ Flux de treball amb Dictador i tinents ](https://aulasoftwarelibre.github.io/taller-de-git/images/flujo-dictador.png)

## Aspectes bàsics de Git  <a id="aspectos-basicos-de-git"></a>

### instal·lació  <a id="instalacion"></a>

#### Instal·lant a Linux  <a id="instalando-en-linux"></a>

Si vols instal·lar Git en Linux a través d'un instal·lador binari, en general pots fer-ho mitjançant l'eina bàsica de gestió de paquets que porta la distribució. Si estàs en Fedora, pots utilitzar yum:

O si estàs en una distribució basada en Debian com Ubuntu, prova amb apt-get:

#### Instal·lant a Windows  <a id="instalando-en-windows"></a>

Instal·lar Git en Windows és molt fàcil. El projecte msysGit té un dels processos d'instal·lació més senzills. Simplement descàrrega l'arxiu exe d'l'instal·lador des de la pàgina de GitHub, i executa-ho:

[http://msysgit.github.com/](http://msysgit.github.com/)

Un cop instal·lat, tindràs tant la versió de línia d'ordres \(inclòs un client SSH que ens serà útil més endavant\) com la interfície gràfica d'usuari estàndard. Es recomana no modificar les opcions que porta per defecte l'instal·lador.

#### Instal·lant a MacOS  <a id="instalando-en-macos"></a>

En MacOS es recomana tenir instal·lada l'eina [homebrew](https://brew.sh/) . Després, és tan fàcil com executar:

```text
$ brew install git
```

### Configuració  <a id="configuracion"></a>

#### La teva identitat  <a id="tu-identidad"></a>

El primer que hauries de fer quan instal·les Git és establir el teu nom d'usuari i adreça de correu electrònic. Això és important perquè les confirmacions de canvis \(commits\) en Git fan servir aquesta informació, i és introduïda de manera immutable en els commits que envies:

```text
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

També es recomana configurar el següent paràmetre:

####  <a id="bash-completion"></a>

## Ús bàsic de Git <a id="uso-basico-de-git"></a>

### Crear un projecte  <a id="crear-un-proyecto"></a>

#### Crear un programa "Hola Món" <a id="crear-un-programa-hola-mundo"></a>

Creem un directori on col·locar el codi

Creem un fitxer `hola.php`que mostri Hola Món.

#### Crear el repositori  <a id="crear-el-repositorio"></a>

Per crear un nou repositori s'usa l'ordre `git init`

#### Afegir l'aplicació  <a id="anadir-la-aplicacion"></a>

Anem a emmagatzemar l'arxiu que hem creat al repositori per poder treballar, després explicarem per a què serveix cada ordre.

```text
$ git add hola.php
$ git commit -m "Creació del projecte"
[master (root-commit) e19f2c1] Creación del proyecto
 1 file changed, 2 insertions(+)
 create mode 100644 hola.php
```

#### Comprovar l'estat de l'repositori  <a id="comprobar-el-estado-del-repositorio"></a>

Amb l'ordre `git status`podem veure en quin estat es troben els arxius del nostre repositori.

```text
$ git status
# On branch master
nothing to commit (working directory clean)
```

Si modifiquem l'arxiu `hola.php`:

```php
<?php
    @print "Hola {$argv[1]}\n";
```

I tornem a comprovar l'estat de l'repositori:

```php
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#   modified:   hola.php
#
no changes added to commit (use "git add" and/or "git commit -a")
```

#### Afegir canvis  <a id="anadir-cambios"></a>

Amb l'ordre `git add`indiquem a git que prepari els canvis perquè siguin emmagatzemats.

```php
$ git add hola.php
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   modified:   hola.php
#
```

#### Confirmar els canvis  <a id="confirmar-los-cambios"></a>

Amb l'ordre `git commit`confirmem els canvis definitivament, el que fa que es guardin permanentment en el nostre repositori.

```php
$ git commit -m "Parametrització del programa"
[master efc252e] Parametrització del programa
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git status
# On branch master
nothing to commit (working directory clean)
```

#### Diferències entre _workdir_ i _staging_ . <a id="diferencias-entre-workdir-y-staging"></a>

Modifiquem la nostra aplicació perquè suporti un paràmetre per defecte i afegim els canvis.

```php
<?php
    $nom = isset($argv[1]) ? $argv[1] : "Mon";
    @print "Hola, {$nom}\n";
```

Aquest cop afegim els canvis a la fase d' _staging_ però sense confirmar-los \( _commit_ \).

```php
git add hola.php
```

Tornem a modificar el programa per indicar amb un comentari el que hem fet.

```php
<?php
// El nom per defecte es Mon
$nombre = isset($argv[1]) ? $argv[1] : "Mon";
@print "Hola, {$nombre}\n";
```

I veiem l'estat en què està el repositori

```php
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   modified:   hola.php
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#   modified:   hola.php
#
```

Podem veure com apareixen l'arxiu _hola.php_ dues vegades. El primer està preparat per ser confirmat i està emmagatzemat a la zona de _staging_ . El segon indica que el directori hola.php està modificat altra vegada a la zona de treball \( _workdir_ \).

{% hint style="danger" %}
Avís

Si tornéssim a fer un `git add hola.php`sobreescriuríem els canvis previs que hi havia a la zona d' _staging_ .
{% endhint %}

Emmagatzemem els canvis per separat:

```php
$ git commit -m "Se añade un parámetro por defecto"
[master 3283e0d] Se añade un parámetro por defecto
 1 file changed, 2 insertions(+), 1 deletion(-)
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#   modified:   hola.php
#
no changes added to commit (use "git add" and/or "git commit -a")
$ git add .
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   modified:   hola.php
#
$ git commit -m "Se añade un comentario al cambio del valor por defecto"
[master fd4da94] Se añade un comentario al cambio del valor por defecto
 1 file changed, 1 insertion(+)
```

Informació

El valor "." després d' `git add`indica que s'afegeixin tots els arxius de forma recursiva.

Avís

Cura quan facis servir `git add .`assegura't que no estàs afegint arxius que no vols afegir.

```php

```

```php

```

#### Ignorant arxius [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#ignorando-archivos) <a id="ignorando-archivos"></a>

L'ordre `git add .`o `git add nombre_directorio`és molt còmoda, ja que ens permet afegir tots els arxius de el projecte o tots els continguts en un directori i els seus subdirectoris. És molt més ràpid que haver d'anar afegint-los un per un. El problema és que, si no es va amb compte, es pot acabar per afegir fitxers innecessaris o amb informació sensible.

En general s'ha d'evitar afegir fitxers que s'hagin generat com a producte de la compilació de el projecte, els que generin els entorns de desenvolupament \(arxius de configuració i temporals\) i aquells que s'acontenten informació sensible, com contrasenyes o tokens d'autenticació. Per exemple, en un projecte de `C/C++`, els arxius objecte no s'han d'incloure, només els que continguin codi font i els make que els generin.

Per indicar-li a _git_ que ha d'ignorar un arxiu, es pot crear un fitxer anomenat _.gitignore_ , bé en l'arrel de el projecte o en els subdirectoris que vulguem. Aquest fitxer pot contenir patrons, un a cada línia, que especiquen quins fitxers s'han d'ignorar. El format és el següent:

|  |  |
| :--- | :--- |


Cada tipus de projecte genera els seus fitxers temporals, així que per a cada projecte hi ha un `.gitignore`apropiat. Hi repositoris que ja tenen creades plantilles. Podeu trobar un en [https://github.com/github/gitignore](https://github.com/github/gitignore)

#### Ignorant arxius globalment [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#ignorando-archivos-globalmente) <a id="ignorando-archivos-globalmente"></a>

Si bé, els arxius que hem ficat en `.gitignore`, han de ser aquells fitxers temporals o de configuració que es poden crear durant les fases de compilació o execució de el programa, en ocasions hi haurà altres fitxers que tampoc hem d'introduir en el repositori i que són recurrents en tots els projectes. En aquest cas, és més útil tenir un _gitignore_ que sigui global a tots els nostres projectes. Aquesta configuració seria complementària a la que ja tenim. Exemples del que es pot ignorar de forma global són els fitxers temporals de sistema operatiu \( `*~`, `.nfs*`\) i els que generen els entorns de desenvolupament.

Per indicar a _git_ que volem tenir un fitxer de _gitignore_ global, hem de configurar amb la següent ordre:

|  |  |
| :--- | :--- |


Ara podem crear un arxiu anomenat `.gitignore_global`en l'arrel del nostre compte amb aquest contingut:

|  |  |
| :--- | :--- |


### Treballant amb l'historial [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#trabajando-con-el-historial) <a id="trabajando-con-el-historial"></a>

#### Observant els canvis [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#observando-los-cambios) <a id="observando-los-cambios"></a>

Amb l'ordre `git log`podem veure tots els canvis que hem fet:

|  |  |
| :--- | :--- |


També és possible veure versions abreujades o limitades, depenent dels paràmetres:

|  |  |
| :--- | :--- |


Una versió molt útil de `git log`és la següent, ja que ens permet veure en quins llocs està màster i HEAD, entre altres coses:

|  |  |
| :--- | :--- |


#### Crear àlies [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#crear-alias) <a id="crear-alias"></a>

Com aquestes ordres són massa llargues, Git ens permet crear àlies per crear noves ordres parametritzades. Per a això podem configurar el nostre entorn amb l'ordre `git config`de la següent manera:

|  |  |
| :--- | :--- |


Exemple

Pots configurar fins i tot àlies per abreujar ordres. Alguns exemples d'àlies útils:

|  |  |
| :--- | :--- |


#### Recuperant versions anteriors [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#recuperando-versiones-anteriores) <a id="recuperando-versiones-anteriores"></a>

Cada canvi és etiquetat per un hash, per poder tornar a aquest moment de l'estat de el projecte s'usa l'ordre `git checkout`.

|  |  |
| :--- | :--- |


L'avís que ens surt ens indica que estem en un estat on no treballem en cap branca concreta. Això significa que els canvis que fem podrien "perdre" perquè si no són guardats en una nova branca, en principi no podríem tornar a recuperar-los. Cal pensar que Git és com un arbre on un node té informació del seu node pare, no dels seus nodes fills, de manera que sempre necessitaríem informació d'on es troben els nodes finals o d'una altra manera no podríem accedir-hi.

#### Tornar a l'última versió de la branca master. [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#volver-a-la-ultima-version-de-la-rama-master) <a id="volver-a-la-ultima-version-de-la-rama-master"></a>

Fem servir `git checkout`indicant el nom de la branca:

|  |  |
| :--- | :--- |


#### Etiquetant versions [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#etiquetando-versiones) <a id="etiquetando-versiones"></a>

Per poder recuperar versions concretes en la història de l'repositori, podem etiquetar, la qual cosa és més fàcil de fer servir un hash. Per això farem servir l'ordre `git tag`.

|  |  |
| :--- | :--- |


Ara anem a etiquetar la versió immediatament anterior com v1-beta. Per a això podem usar els modificadors `^`o `~`que ens portaran a un ancestre determinat. Les següents dos ordres són equivalents:

|  |  |
| :--- | :--- |


Si executem l'ordre sense paràmetres ens mostrarà totes les etiquetes existents.

|  |  |
| :--- | :--- |


I per veure-les en l'historial:

|  |  |
| :--- | :--- |


#### Esborrar etiquetes [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#borrar-etiquetas) <a id="borrar-etiquetas"></a>

Per esborrar etiquetes:

|  |  |
| :--- | :--- |


#### Visualitzar canvis [¶](https://aulasoftwarelibre.github.io/taller-de-git/usobasico/#visualizar-cambios) <a id="visualizar-cambios"></a>

Per veure els canvis que s'han realitzat en el codi fem servir l'ordre `git diff`. L'ordre sense especificar res més, mostrarà els canvis que no han estat afegits encara, és a dir, tots els canvis que s'han fet abans d'utilitzar l'ordre `git add`. Després es pot indicar un paràmetre i donarà els canvis entre la versió indicada i l'estat actual. O per comparar dues versions entre si, s'indica la més antiga i la més nova. exemple:

|  |  |
| :--- | :--- |


