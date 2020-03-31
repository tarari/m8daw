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

### Add-on mysql

Pugem l'esquema al Gestor ClearDB:

```javascript
$ mysql -u b9f7f41a06f314 -h us-cdbr-iron-east-01.cleardb.net -p heroku_fb40bdc559eaffa < projecte.sql
```

