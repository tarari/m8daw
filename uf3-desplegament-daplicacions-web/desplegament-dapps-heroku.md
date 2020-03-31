# Desplegament d'aplicacions en Heroku

El desplegament d'aplicacions php web sobre Heroku obliga als següents requeriments:

* Compte en [Heroku](https://heroku.com)
* PHP instal·lat
* git instal·lat
* composer instal·lat

## Aplicació web amb php i mysql

Suposant que ja tenim el projecte que volem desplegar, ens col·loquem al seu directori.

```text
cd projecte

```

Un cop dins, cal crear un fitxer composer.json amb les dependències del projecte, per exemple:

```javascript
{
  "require": {
    "ext-mysqli": "*"
  }
}
```

Tanmateix, iniciem repositori local en git i fem un commit

```javascript
git init
git add .
git commit -am "First commit heroku project"
```

Posteriorment iniciem sessió en heroku amb `heroku login`

A continació creem el projecte heroku

```javascript
heroku create [nom_aplicació]
```

#### Desplegament en heroku



Ara podem **desplegar la nostra aplicació**:

```javascript
git push heroku master
```

Podem comprovar el desplegament amb `heroku open`

#### Fer commits dels possibles canvis

#### Desplegar canvis amb "git  push heroku master"

#### Establir el add-on de la base de dades

```javascript
heroku addons:add cleardb:ignite
```

Comprovem dades de la base de dades:

```javascript
heroku config
=== project Config Vars
CLEARDB_DATABASE_URL: mysql://b9f7f41a06f314:2aabd0d1@us-cdbr-iron-east-01.cleardb.net/heroku_fb40bdc559eaffa?reconnect=true

```

O anem al dashboard de l'aplicació al navegador:

![Settings del dyno de l&apos;aplicaci&#xF3;](../.gitbook/assets/captura-de-pantalla-2020-03-31-a-les-15.29.12.png)

### Add-on mysql

Podem pujar l'esquema al Gestor ClearDB ignite amb les dades que ens proporciona

**mysql://usuari:password@maquina/base\_de\_dades**

```javascript
$ mysql -u b9f7f41a06f314 -h us-cdbr-iron-east-01.cleardb.net -p heroku_fb40bdc559eaffa < projecte.sql
```

Fem el volcat de l'script de sql, ara ja podem afegir el fitxer de configuració necessari a la nostra aplicació, cas d'utilitzar **mysqli**:

```javascript
<?php
//Get Heroku ClearDB connection information
$cleardb_url      = parse_url(getenv("CLEARDB_DATABASE_URL"));
$cleardb_server   = $cleardb_url["host"];
$cleardb_username = $cleardb_url["user"];
$cleardb_password = $cleardb_url["pass"];
$cleardb_db       = substr($cleardb_url["path"],1);


$active_group = 'default';
$query_builder = TRUE;

$db['default'] = array(
    'dsn'    => '',
    'hostname' => $cleardb_server,
    'username' => $cleardb_username,
    'password' => $cleardb_password,
    'database' => $cleardb_db,
    'dbdriver' => 'mysqli',
    'dbprefix' => '',
    'pconnect' => FALSE,
    'db_debug' => (ENVIRONMENT !== 'production'),
    'cache_on' => FALSE,
    'cachedir' => '',
    'char_set' => 'utf8',
    'dbcollat' => 'utf8_general_ci',
    'swap_pre' => '',
    'encrypt' => FALSE,
    'compress' => FALSE,
    'stricton' => FALSE,
    'failover' => array(),
    'save_queries' => TRUE
);



//connect to DB
$conn = new mysqli($db['default']['hostname'],
    $db['default']['username'],$db['default']['password'],
    $db['default']['database']);
			if ($conn->connect_error) {
			    die("Connection failed: " . $conn->connect_error);
			}
```

I per últim: afegir git, commit, desplegar i comprovar:

```javascript
git add .
git commit -am "Heroku db config"
git push heroku master
heroku open
```

