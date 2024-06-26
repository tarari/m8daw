---
description: >-
  Estudiarem com implantar aplicacions web de forma segura,  que pot ser a
  través de servidors d'aplicacions o bé directament afegint temes de
  certificats i transport segur
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



## Implantació d'aplicacions web de forma segura

La implantació d'aplicacions web en entorns segurs és un procés crític per garantir la seguretat, la privacitat i la disponibilitat de les aplicacions i les dades que gestionen. Aquest procés inclou diverses pràctiques i tecnologies destinades a protegir tant el servidor on s'executa l'aplicació com les comunicacions entre el servidor i els usuaris. A continuació,  descrivim les principals estratègies i eines per a la implantació segura d'aplicacions web:

#### Estratègies per a la implantació segura

1. **Autenticació i Autorizació**
   * **Autenticació:** Assegura que només usuaris legítims poden accedir a l'aplicació. Això es pot fer mitjançant l'ús de contrasenyes segures, autenticació multifactor (MFA) i sistemes de Single Sign-On (SSO).
   * **Autorizació:** Defineix què pot fer cada usuari un cop autenticat. L'ús de rols i permisos ajuda a limitar l'accés a parts sensibles de l'aplicació.
2. **Comunicacions Segures**
   * **TLS/SSL:** L'ús de protocols TLS (Transport Layer Security) o SSL (Secure Sockets Layer) per xifrar les comunicacions entre el servidor i els clients assegura que les dades no poden ser interceptades o modificades per tercers.
   * **Certificats Digitals:** Els certificats SSL/TLS, emesos per autoritats de certificació confiables, s'utilitzen per autenticar la identitat del servidor.
3. **Protecció contra Atacs Comuns**
   * **Firewall d'Aplicacions Web (WAF):** Un WAF filtra i monitora el tràfic HTTP cap a l'aplicació web, protegint-la contra atacs comuns com injecció SQL, XSS (Cross-Site Scripting), i altres amenaces.
   * **Rate Limiting i Throttling:** Limitació del nombre de peticions que pot fer un usuari en un període determinat per prevenir atacs de Denial of Service (DoS).
4. **Gestió de Vulnerabilitats**
   * **Actualitzacions Regulars:** Assegurar-se que el sistema operatiu, el servidor web, les llibreries i l'aplicació en si mateixa estan actualitzats amb les darreres versions i pegats de seguretat.
   * **Escanejos de Vulnerabilitats:** Ús d'eines automatitzades per detectar i corregir vulnerabilitats en l'aplicació web.
5. **Seguretat del Servidor**
   * **Configuració Segura del Servidor:** Desactivar serveis innecessaris, configurar correctament permisos d'arxius i directoris, i utilitzar principis de mínim privilegi.
   * **Seguretat de la Base de Dades:** Protegir la base de dades amb mesures com xifrat, autenticació robusta, i control d'accés rigorós.

#### Exemple d'Implantació Segura

**Exemple: Implantació d'una Aplicació de Comerç Electrònic**

**Fase de Desenvolupament**

1. **Desenvolupament Segur:** L'equip de desenvolupament segueix pràctiques de codificació segura i utilitza eines de revisió de codi per detectar vulnerabilitats.
2. **Autenticació MFA:** S'integra un sistema d'autenticació multifactor per assegurar que només usuaris autoritzats poden accedir a les àrees sensibles de la botiga en línia, com la informació de pagament.

**Fase de Prova**

1. **Escaneig de Vulnerabilitats:** Abans de la implantació, es realitza un escaneig complet de vulnerabilitats per identificar i corregir qualsevol problema de seguretat.
2. **Penetration Testing:** Es contracten especialistes en seguretat per realitzar proves de penetració i assegurar que l'aplicació resisteix atacs simulats.

**Fase de Producció**

1. **TLS/SSL:** Es configura el servidor web per utilitzar TLS amb un certificat digital emès per una autoritat de certificació reconeguda.
2. **Firewall d'Aplicacions Web (WAF):** S'implementa un WAF per monitorar i filtrar el tràfic, bloquejant intents d'injecció SQL i altres atacs.
3. **Monitorització Continua:** Es despleguen eines de monitorització per detectar activitats sospitoses i resoldre incidents de seguretat en temps real.

**Manteniment**

1. **Actualitzacions Regulars:** El servidor web, la base de dades, i l'aplicació s'actualitzen regularment per incorporar les darreres millores de seguretat.
2. **Còpies de Seguretat:** Es realitzen còpies de seguretat periòdiques de les dades per assegurar la recuperació en cas d'incidents.

Mitjançant aquestes pràctiques, l'aplicació de comerç electrònic pot funcionar de manera segura, protegint la informació dels usuaris i mantenint la confiança dels clients.

### WAF

La configuració d'un firewall d'aplicacions web (WAF) implica diversos passos per assegurar que l'aplicació web estigui protegida contra atacs comuns i vulnerabilitats. A continuació, descrivim un procés general per configurar un WAF, utilitzant com a exemple **AWS WAF**, però els passos són aplicables a altres WAFs com **ModSecurity**, **Cloudflare**, **Imperva**, etc.

#### Passos per Configurar un WAF

1. **Selecció del WAF**
   * Tria un WAF adequat segons les necessitats de l'aplicació. AWS WAF, Cloudflare WAF, i ModSecurity són opcions populars.
2. **Creació del WAF**
   * Registra't al servei del WAF i crea una instància del WAF. Per AWS WAF, això es fa des de la consola de gestió d'AWS.
3. **Definició de les Regles**
   * Defineix les regles de seguretat que el WAF ha d'aplicar. Aquestes poden incloure regles per prevenir atacs de:
     * **Injecció SQL**
     * **Cross-Site Scripting (XSS)**
     * **File Inclusion**
     * **Remote Code Execution**
   * Les regles poden ser estàndards (o predefinides) o personalitzades.
4. **Configuració de Regles Predefinides**
   * La majoria de WAFs ofereixen regles predefinides que es poden activar fàcilment. Per exemple, AWS WAF té AWS Managed Rules que cobreixen les vulnerabilitats més comunes.
5. **Creació de Regles Personalitzades**
   * Si necessites més control, pots crear regles personalitzades. Per exemple, pots crear una regla per bloquejar IPs específiques, per filtrar certs patrons en les URLs, o per prevenir atacs d'injecció SQL basats en patrons específics.
6. **Configuració de Grups de Regles**
   * Agrupa les regles en grups lògics per facilitar la gestió. Per exemple, pots tenir un grup de regles per la prevenció d'injeccions SQL i un altre per la prevenció de XSS.
7. **Associació del WAF amb l'Aplicació**
   * Associa el WAF amb la teva aplicació web. Això varia segons el WAF. En AWS WAF, es fa associant el WAF amb un CloudFront Distribution, un Application Load Balancer (ALB), o un API Gateway.
8. **Monitorització i Ajust**
   * Monitora l'activitat del WAF per veure quines regles s'estan activant i ajustar-les segons sigui necessari. Això inclou l'addició de noves regles, la modificació de regles existents, i la desactivació de regles que generin falsos positius.
9. **Testing i Validació**
   * Realitza proves per assegurar que el WAF està funcionant correctament. Prova diferents tipus d'atacs per verificar que el WAF els detecta i bloqueja correctament.
10. **Manteniment i Actualització**
    * Manté el WAF actualitzat amb les últimes regles de seguretat i millores. Revisa regularment els logs i informes per ajustar les regles i millorar la protecció.

#### Exemple de Configuració d'AWS WAF

**1. Crear una Política de WAF**

Accedeix a la consola d'AWS i navega a AWS WAF & Shield. Crea una nova política de WAF i selecciona el tipus de recurs que protegiràs (CloudFront, ALB, etc.).

**2. Afegir Regles**

* **Regles Predefinides:** Afegeix un grup de regles gestionades (Managed Rule Groups) proporcionades per AWS. Això inclou regles per prevenir injeccions SQL, XSS, i altres atacs comuns.
*   **Regles Personalitzades:** Crea una regla personalitzada. Per exemple, per bloquejar totes les sol·licituds d'una IP específica:

    ```yaml
    {
        "Name": "BlockIP",
        "Priority": 1,
        "Statement": {
            "IPSetReferenceStatement": {
                "ARN": "arn:aws:wafv2:region:account-id:ipset/IPSetName"
            }
        },
        "Action": {
            "Block": {}
        },
        "VisibilityConfig": {
            "SampledRequestsEnabled": true,
            "CloudWatchMetricsEnabled": true,
            "MetricName": "BlockIPMetric"
        }
    }
    ```

**3. Associar la Política amb el Recurs**

Associa la política de WAF amb el teu recurs seleccionat (per exemple, un CloudFront distribution). Això es fa editant les configuracions del recurs i seleccionant la política de WAF creada.

**4. Monitoritzar i Ajustar**

Utilitza CloudWatch per monitoritzar les sol·licituds bloquejades i ajusta les regles segons sigui necessari. Això t'ajudarà a refinar les configuracions per minimitzar els falsos positius i garantir una protecció efectiva.

Amb aquests passos, pots assegurar que la teva aplicació web està protegida per un WAF ben configurat, millorant la seva seguretat i resistència davant atacs maliciosos.
