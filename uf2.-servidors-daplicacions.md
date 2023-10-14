---
description: >-
  Estudiarem contenidors d'aplicacions i el seu desplegament i serveis proxy com
  a pasarel·les d'aplicacions i com a balanceig de càrrega.
---

# UF2. Servidors d'aplicacions

## Contenidors Docker

Els contenidors docker constitueixen una nova tecnologia i forma de treballar que sobretot facilita el procés de desplegament d'aplicacions i la transició a l'entorn de producció.

_Docker és una eina dissenyada per facilitar la creació, implementació i execució d'aplicacions mitjançant contenidors. Els contenidors permeten a un desenvolupador empaquetar una aplicació amb totes les parts que necessita, com ara biblioteques i altres dependències, i enviar-ho tot com un sol paquet._&#x20;

**El que realment fa Docker és separar el codi de l'aplicació dels requisits i necessitats d'infraestructura.**

_Fem que el desenvolupador només desenvolupi._

Ens podem assegurar un ecosistema que funcioni independentment del lloc on reproduim l'aplicació.

\
Podem dir als contenidors tot el que necessita per treballar, totes les dependències que cal descarregar i instal·lar per executar l'aplicació. **Aquest procés es fa amb un Dockerfile.**



Docker té quatre eines principals que ofereix per dur a terme les tasques:

* Docker Engine
* Docker compose
* Docker Machine
* Docker Swarm

Docker Engine

El Docker Engine és la "potent tecnologia de contenidors de codi obert de Docker combinada amb un flux de treball per crear i contenir  les vostres aplicacions". — Docker, Sobre Docker Engine És el que crea i executa imatges Docker des d'un únic Dockerfile o -compose.yml. Quan algú utilitza una ordre docker a través de la CLI de Docker, parla amb aquest motor per fer el que cal fer.

