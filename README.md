---
description: >-
  En aquest mòdul M8 estudiarem el procesos necessaris per realitzar ldel
  desplegament de l'aplicació web i el seu entorn, prenent consciència de totes
  les tecnologies que hi són necessàries.
---

# Introducció

### Reconeixement de l'autor

{% hint style="info" %}
   
 ![](.gitbook/assets/by-nc.eu.png)   
**Desplegament d'aplicacions web** by [Toni Jiménez](https://t-jimenez.gitbook.io/desenvolupament-d-apps-en-php/) is licensed under a [Creative Commons Reconocimiento-NoComercial 4.0 Internacional License](http://creativecommons.org/licenses/by-nc/4.0/).

**Toni Jiménez** [**&lt;t.jimenez@escolesnuria.cat**](mailto:t.jimenez@escolesnuria.cat)**&gt;**
{% endhint %}

Començarem explicant l'entorn de qualsevol desplegament, cal fer primer un repàs de tot allò.

## Model OSI

Segons la Viquipèdia

_És un estàndard que té per objectiu aconseguir interconnectar sistemes de procedència diferent perquè aquests poguessin intercanviar informació sense cap tipus d'impediments a causa dels protocols amb els que aquests operaven de forma pròpia segons el seu fabricant._

![Model capes OSI](.gitbook/assets/osi_model_v1.svg)

El model de capes OSI, representa un estandar però serveix de referència per estudiar un procés de COMUNICACIÓ. 

El procés que acompanya qualsevol operació amb una aplicació web es basa en aquest model, per tant la seva utilitat és innegable.

### Comunicació a través d'un exemple.

Quan s'estableix una comunicació entre dos equips cal tenir en compte el rol que assumeix cadascú en la comunicació, és a dir, si parlem de l'emissor que transmet el missatge o bé el receptor que rep el missatge. En termes de computació, podem parlar també del **client**, qui sol·licita un recurs \( creant un llenguatge associat per indicar qui, què i com vol el recurs - **protocol**\) i servidor, qui ofereix el recurs \(creant un llenguatge associat per indicar què, a qui i com pot oferir el recurs\).

### El model OSI es construeix per capes

Imaginem una comunicació típica, una consulta a Internet, per exemple una consulta a la pàgina de la nostra escola:

**`https://escolesnuria.cat`** aquí som clients i qui ens servirà la pàgina es diu servidor.

Pensem en el procediment:

**Request** al servidor que conté la pàgina HTML que ens servirà el servidor seguint la nostra petició. protocol HTTP

Servidor a través d'un programari, processa i extreu la pàgina HTML, i **respon** al client a través de protocol HTTP.

Tot aquest procediment es realitza de forma immediata \(o no\) de manera que si hem de pensar com es fa, ens hem de plantejar un model d'estudi per capes.

Les dades passen en sentit descendent a través de les capes transformant-se \( encapsulació \) fins poder arribar al medi físic on es transmetre a l'equip de destinació a través d'impulsos elèctrics. En arribar a la destinació es procedeix de nou a encapsular segons el protocol de cada capa per arribar finalment a destinació.

![Nivells OSI en una comunicaci&#xF3;](.gitbook/assets/osi.png)



