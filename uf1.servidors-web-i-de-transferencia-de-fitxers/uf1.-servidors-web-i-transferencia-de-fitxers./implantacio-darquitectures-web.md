# Implantació d'arquitectures web

## **1.Arquitectures web. Models**

Les **arquitectures web** són els dissenys estructurals que defineixen la interacció entre els diferents components d'una aplicació web. Aquestes arquitectures poden variar segons els requisits de l'aplicació i la seva complexitat. Els models més comuns inclouen:

* **Arquitectura de dos nivells (Client-Servidor)**: En aquest model, hi ha dos components principals:
  * **Client**: Sol·licita serveis i recursos.
  * **Servidor**: Proporciona serveis i processa les sol·licituds del client.
  * **Avantatges**: Senzillesa en la implementació i manteniment.
  * **Inconvenients**: Escalabilitat limitada.
* **Arquitectura de tres nivells (n-Tiers)**: Divideix les responsabilitats en tres nivells:
  * **Presentació**: Interfície d'usuari.
  * **Lògica de negoci**: Processament de la lògica de l'aplicació.
  * **Dades**: Emmagatzematge i recuperació de dades.
  * **Avantatges**: Millor modularitat i escalabilitat.
  * **Inconvenients**: Complexitat més gran en la configuració i manteniment.
* **Arquitectura de microserveis**: L'aplicació es desglossa en serveis petits i independents que poden desplegar-se i escalar-se de manera autònoma.
  * **Avantatges**: Escalabilitat, facilitat de desplegament independent i robustesa.
  * **Inconvenients**: Requereix una gestió i coordinació més avançada, pot augmentar la latència.

## **2. Servidors web i d'aplicacions. Instal·lació i configuració bàsica**

Els **servidors web** i **servidors d'aplicacions** són components essencials per al funcionament de les aplicacions web. Aquí s'expliquen els passos per a la seva instal·lació i configuració bàsica:

* **Servidor web (Apache/Nginx)**:
  * **Instal·lació**:
    * Apache: `sudo apt-get install apache2`
    * Nginx: `sudo apt-get install nginx`
  * **Configuració bàsica**:
    * Apache: Editar `/etc/apache2/apache2.conf` i configurar llocs virtuals en `/etc/apache2/sites-available/`.
    * Nginx: Editar `/etc/nginx/nginx.conf` i configurar blocs de servidor en `/etc/nginx/sites-available/`.
* **Servidor d'aplicacions (Tomcat/Node.js)**:
  * **Instal·lació**:
    * Tomcat: `sudo apt-get install tomcat9`
    * Node.js: `sudo apt-get install nodejs`
  * **Configuració bàsica**:
    * Tomcat: Configurar `server.xml` i desplegar aplicacions en la carpeta `webapps`.
    * Node.js: Configurar el fitxer de l'aplicació i definir el port d'escolta (per exemple, en un fitxer `app.js`).

## **3. Tecnologies de virtualització de servidors al núvol i en contenidors. Instal·lació i configuració bàsica**

Les **tecnologies de virtualització** permeten crear entorns aïllats per desplegar aplicacions, tant al núvol com en contenidors locals. Les tecnologies principals inclouen Docker i Kubernetes.

* **Docker**:
  * **Instal·lació**: `sudo apt-get install docker-ce`
  * **Configuració bàsica**:
    * Crear i executar contenidors: `docker run -d -p 80:80 nginx`
    * Gestionar imatges i contenidors amb comandes com `docker pull`, `docker ps`, i `docker stop`.
* **Kubernetes**:
  * **Instal·lació**:
    * Instal·lació de `kubectl`: `sudo apt-get install kubectl`
    * Instal·lació de `minikube` per a desenvolupament local: `sudo apt-get install minikube`
  * **Configuració bàsica**:
    * Crear i gestionar pods, serveis i desplegaments amb fitxers YAML.
    * Comandes bàsiques: `kubectl apply -f deployment.yaml`, `kubectl get pods`.

**1.4 Estructura i recursos que componen una aplicació web**

Una **aplicació web** es compon de diversos elements i recursos:

* **Frontend**: La part visible per l'usuari, desenvolupada amb tecnologies com:
  * **HTML**: Estructura del contingut.
  * **CSS**: Estilització del contingut.
  * **JavaScript**: Interactivitat i dinàmica.
* **Backend**: La part que gestiona la lògica de l'aplicació i la comunicació amb la base de dades, desenvolupada amb tecnologies com:
  * **Llenguatges de programació**: Java, Python, Node.js.
  * **Frameworks**: Spring, Django, Express.
* **Base de dades**: Sistema per emmagatzemar i recuperar dades, com:
  * **SQL**: MySQL, PostgreSQL.
  * **NoSQL**: MongoDB, Redis.
* **APIs**: Interfícies per a la comunicació entre components:
  * **RESTful**: Estructura basada en recursos i mètodes HTTP.
  * **GraphQL**: Sistema de consulta flexible i eficient.

### **5. Documentació dels processos realitzats**

La **documentació** és essencial per assegurar que els processos d'instal·lació i configuració siguin replicables i comprensibles per altres persones o equips. Els elements clau de la documentació inclouen:

* **Passos d'instal·lació**:
  * Llista detallada de comandes utilitzades.
  * Descripció dels paquets i versions instal·lades.
* **Configuracions aplicades**:
  * Contingut dels fitxers de configuració modificats.
  * Explicació dels paràmetres configurats i la seva finalitat.
* **Proves de funcionament**:
  * Descripció de les proves realitzades per verificar el correcte funcionament dels serveis.
  * Resultats obtinguts i captures de pantalla (si és aplicable).
* **Solució de problemes comuns**:
  * Descripció dels problemes trobats durant el procés i les solucions aplicades.

Aquesta documentació  realitzada assegura la coherència, facilita el manteniment futur i permet que altres membres de l'equip puguin comprendre i seguir els mateixos passos amb facilitat.
