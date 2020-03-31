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

