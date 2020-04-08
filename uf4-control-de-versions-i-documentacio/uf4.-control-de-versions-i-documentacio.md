---
description: >-
  Estudiarem casos pràctics de control de versions d'aplicacions i les seves
  eines git i Github.
---

# Git i workflow



## Què es Git?

Git és un sistema de control de versions per seguir els canvis d'arxius entre diversos usuaris. És principalment usat per al maneig de codi font dins el desenvolupament de programari però també pot ser usat per manejar els canvis de qualsevol tipus d'arxiu. Com a sistema distribuït de control de revisions, està dirigit a la velocitat, integritat de les dades, suport per a fluxos de treball distribuïts.

#### Fundaments de Git

**Instantáneas, no diferencias**

La principal diferencia entre Git y cualquier otro VCS \(Subversion y compañía incluidos\) es cómo Git modela sus datos. Conceptualmente, la mayoría de los demás sistemas almacenan la información como una lista de cambios en los archivos. Estos sistemas \(CVS, Subversion, Perforce, Bazaar, etc.\) modelan la información que almacenan como un conjunto de archivos y las modificaciones hechas sobre cada uno de ellos a lo largo del tiempo, como ilustra la siguiente imagen

[![](https://camo.githubusercontent.com/79186e9aeb61ddda0b6b163e78259e3a52a50939/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303130342d746e2e706e67)](https://camo.githubusercontent.com/79186e9aeb61ddda0b6b163e78259e3a52a50939/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303130342d746e2e706e67)

Git no modela ni almacena sus datos de este modo. En cambio, Git modela sus datos más como un conjunto de instantáneas de un mini sistema de archivos. Cada vez que confirmas un cambio, o guardas el estado de tu proyecto en Git, él básicamente hace una foto del aspecto de todos tus archivos en ese momento, y guarda una referencia a esa instantánea. Para ser eficiente, si los archivos no se han modificado, Git no almacena el archivo de nuevo, sólo un enlace al archivo anterior idéntico que ya tiene almacenado. Git modela sus datos más como en la imagen a continuación\[2\]

[![](https://camo.githubusercontent.com/50dea14c4b5d354fd977cf959832166b9f28d060/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303130352d746e2e706e67)](https://camo.githubusercontent.com/50dea14c4b5d354fd977cf959832166b9f28d060/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303130352d746e2e706e67)

**Los tres estados de Git**

Git tiene tres estados principales en los que se pueden encontrar tus archivos: confirmado \(committed\), modificado \(modified\), y preparado \(staged\). Confirmado significa que los datos están almacenados de manera segura en tu base de datos local. Modificado significa que has modificado el archivo pero todavía no lo has confirmado a tu base de datos. Preparado significa que has marcado un archivo modificado en su versión actual para que vaya en tu próxima confirmación.

Esto nos lleva a las tres secciones principales de un proyecto de Git: el directorio de Git \(Git directory\), el directorio de trabajo \(working directory\), y el área de preparación \(staging area\).

[![](https://camo.githubusercontent.com/cfcc15d315075892a5062c1f4fca0177c2a22820/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303130362d746e2e706e67)](https://camo.githubusercontent.com/cfcc15d315075892a5062c1f4fca0177c2a22820/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303130362d746e2e706e67)

El directorio **.git** es donde Git almacena los metadatos y la base de datos de objetos para tu proyecto. Es la parte más importante de Git, y es lo que se copia cuando clonas un repositorio desde otro ordenador.

El _directorio de trabajo_ es una copia de una versión del proyecto. Estos archivos se sacan de la base de datos comprimida en el directorio de Git, y se colocan en disco para que los puedas usar o modificar.

El _área de preparación_ es un sencillo archivo, generalmente contenido en tu directorio **.git**, que almacena información acerca de lo que va a ir en tu próxima confirmación. A veces se le denomina índice, pero se está convirtiendo en estándar el referirse a ella como el _área de preparación_.

El flujo de trabajo básico en Git es algo así:

```text
1. Modificas una serie de archivos en tu directorio de trabajo.
2. Preparas los archivos, añadiendolos a tu área de preparación.
3. Confirmas los cambios, lo que toma los archivos tal y como están en el área de preparación, y almacena esas instantáneas de manera permanente en tu directorio de Git.
```

Si una versión concreta de un archivo está en el directorio **.git**, se considera _confirmada_ \(committed\). Si ha sufrido cambios desde que se obtuvo del repositorio, pero ha sido añadida al área de preparación, está _preparada_ \(staged\). Y si ha sufrido cambios desde que se obtuvo del repositorio, pero no se ha preparado, está _modificada_ \(modified\)\[2\].

#### Configurando Git por primera vez

Una vez que tienes instalado Git es necesario algunas cosas para personalizar tu entorno. Git contiene una herramienta llamada _git config_ que te permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git. Estas variables pueden almacenarse en tres archivos distintos\[3\]:

* /etc/gitconfig: Contiene configuraciones de Git aplicables a todos los usuarios. Puedes hacer que Git lea o escriba a este archivo pasando la opción _--system_.
* ~/.gitconfig: Archivo específico para tu usuario. Puedes hacer que Git lea y escriba a este archivo pasando la opción _--global_.
* ./.git/config: Archivo de configuración del repositorio en el que estoy ubicado. Cada nivel sobreescribe los valores del nivel anterior, es decir que el archivo de configuración del repositorio sobreescribirá los valores de _/etc/gitconfig_ y _~/.gitconfig_.

**Tu identidad**

Lo primero que deberías hacer cuando instalas Git es establecer tu nombre de usuario y dirección de correo electrónico. Esto es importante porque las confirmaciones de cambios \(commits\) en Git usan esta información, y es introducida de manera inmutable en los commits que envías\[3\]:

```text
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

De nuevo, sólo necesitas hacer esto una vez si especificas la opción --global, ya que Git siempre usará esta información para todo lo que hagas en ese sistema. Si quieres sobrescribir esta información con otro nombre o dirección de correo para proyectos específicos, puedes ejecutar el comando sin la opción --global cuando estés en ese proyecto\[3\].

Para comprobar tu configuración solo necesitas ejecutar el siguiente comando:

```text
$ git config --list
```

#### Obteniendo ayuda

Si alguna vez necesitas ayuda usando Git, hay tres formas de ver la página del manual \(manpage\) para cualquier comando de Git\[4\]:

```text
$ git help <comando>
$ git <comando> --help
$ man git-<comando>
```

#### Inicializando un repositorio en un directorio existente

Lo primero que haremos es crear una carpeta dentro de la cual estarán los archivos a darle seguimiento.

```text
$ mkdir git-workshop
$ cd git-workshop
$ git init
```

Esto crea un nuevo subdirectorio llamado .git que contiene todos los archivos necesarios del repositorio —un esqueleto de un repositorio Git. Todavía no hay nada en tu proyecto que esté bajo seguimiento\[5\].

Lo que sigue para agregar un remoto al repositorio que recién creamos es:

1. Crear un nuevo repositorio remoto en cualquier herramienta, en este caso usaremos Github

[![](https://github.com/mayela/git-workshop/raw/master/images/new-remote.png)](https://github.com/mayela/git-workshop/blob/master/images/new-remote.png)

1. Agregar la información necesaria para la creación del nuevo repositorio remoto

[![](https://github.com/mayela/git-workshop/raw/master/images/remote-description.png)](https://github.com/mayela/git-workshop/blob/master/images/remote-description.png)

1. Agregar al repositorio local el repositorio remoto que acabamos de crear

[![](https://github.com/mayela/git-workshop/raw/master/images/setup.png)](https://github.com/mayela/git-workshop/blob/master/images/setup.png)

```text
$ git remote add origin https://github.com/mayela/git-workshop.git
```

A estas alturas ya tenemos un creados un repositorio local y un repositorio remoto, pero aún no tenemos archivos a los cuales darles seguimiento.Si deseas empezar a controlar versiones de archivos existentes \(a diferencia de un directorio vacío\), probablemente deberías comenzar el seguimiento de esos archivos y hacer una confirmación inicial. Puedes conseguirlo con unos pocos comandos git add para especificar qué archivos quieres controlar, seguidos de un commit para confirmar los cambios\[5\]. Para esto consideraremos que ya tenemos un archivo llamado README.md al cual dar segumiento:

```text
$ git add README.md
$ git commit -m "Versión inicial del proyecto"
```

Para subir los cambios al repositorio remoto solo basta ejecutar la siguiente instrucción:

```text
$ git push origin master
```

#### Clonando un repositorio existente

Si deseas obtener una copia de un repositorio Git existente —por ejemplo, un proyecto en el que te gustaría contribuir— el comando que necesitas es _git clone_. Puedes clonar un repositorio con _git clone \[url\]_. Por ejemplo, si quieres clonar unos ejercicios para Javascript llamados Koans, harías algo así\[5\]:

```text
$ git clone https://github.com/mrdavidlaing/javascript-koans.git
```

Esto crea un directorio llamado "grit", inicializa un directorio .git en su interior, descarga toda la información de ese repositorio, y saca una copia de trabajo de la última versión.Si quieres clonar el repositorio a un directorio con otro nombre que no sea grit, puedes especificarlo con la siguiente opción de línea de comandos\[5\]:

```text
$ git clone https://github.com/mrdavidlaing/javascript-koans.git js-koans
```

#### Guardando cambios en el repositorio

Tienes un repositorio Git completo, y una copia de trabajo de los archivos de ese proyecto. Necesitas hacer algunos cambios, y confirmar instantáneas de esos cambios a tu repositorio cada vez que el proyecto alcance un estado que desees grabar.

Recuerda que cada archivo de tu directorio de trabajo puede estar en uno de estos dos estados: bajo seguimiento \(tracked\), o sin seguimiento \(untracked\). Los archivos bajo seguimiento son aquellos que existían en la última instantánea; pueden estar sin modificaciones, modificados, o preparados. Los archivos sin seguimiento son todos los demás —cualquier archivo de tu directorio que no estuviese en tu última instantánea ni está en tu área de preparación—. La primera vez que clonas un repositorio, todos tus archivos estarán bajo seguimiento y sin modificaciones, ya que los acabas de copiar y no has modificado nada\[6\].

[![](https://camo.githubusercontent.com/f7d3f1fc948460d025b60041ba963b84eebe66ab/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303230312d746e2e706e67)](https://camo.githubusercontent.com/f7d3f1fc948460d025b60041ba963b84eebe66ab/68747470733a2f2f6769742d73636d2e636f6d2f666967757265732f3138333333666967303230312d746e2e706e67)

**Comprobando el estado de tus archivos**

Tu principal herramienta para determinar qué archivos están en qué estado es el comando _git status_. Primero verificaremos el estado del repositorio:

```text
$ git status
// la salida será algo muy parecido a lo que sigue
En la rama master
nada para hacer commit, el árbol de trabajo esta limpio
```

Crea un archivo que contenga un _hola mundo_ en Javascript y luego revisa el estado de los archivos.

```text
<!DOCTYPE html>
<html>
    <head>
        <title>El primer script</title>
        <script type="text/javascript">
            alert("Hola Mundo!");
        </script>
    </head>
 
    <body>
        <p>Esta página contiene el primer script</p>
    </body>
</html>
```

```text
$ git status
En la rama master
Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)

	hola.html

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
```

Ahora vamos a darle seguimiento con los comandos _git add_ y _git commit_:

```text
$ git add hola.html
$ git status
En la rama master
Cambios a ser confirmados:
  (usa "git reset HEAD <archivo>..." para sacar del área de stage)

	nuevo archivo:  hola.html
$ git commit -m "Hola mundo en Javascript agregado"
[master d48e617] Hola mundo en Javascript agregado
 1 file changed, 14 insertions(+)
 create mode 100644 hola.html
$ git status
En la rama master
nada para hacer commit, el árbol de trabajo esta limpio
```

