# Elaboració de documentació i sistemes de control de versió

Elaborar la documentació d'una aplicació web és molt important per garantir la comunicació entre desenvolupadors, mantenir la qualitat del codi i assegurar una transició suau entre les diferents etapes del desenvolupament.&#x20;

#### Elaboració de la documentació d'una aplicació web

1. **Cal identificar els tipus de documentació necessària:**
   * **Documentació de l'usuari final:** Guia d'usuari, FAQ, manuals d'instruccions.
   * **Documentació tècnica:** Manual del desenvolupador, arquitectura de l'aplicació, API, instal·lació i configuració.
   * **Documentació del codi:** Comentaris en el codi, explicació de mòduls i funcions.
2. **Seleccionar eines de generació de documentació:**
   * **Per a la documentació del codi:**
     * **Javadoc:** Ideal per a projectes en Java. Genera documentació HTML a partir dels comentaris Javadoc en el codi.
     * **Doxygen:** Suporta múltiples llenguatges (C++, Java, Python). Genera documentació HTML, PDF, etc.
     * **Sphinx:** Especialment per a Python. Genera documentació HTML i PDF a partir de fitxers reStructuredText.
     * **Swagger/OpenAPI:** Per documentar APIs RESTful. Genera documentació interactiva de les APIs.
   * **Per a la documentació tècnica i de l'usuari final:**
     * **Markdown + Static Site Generators (SSG):** Com Jekyll, Hugo o MkDocs. Ideal per a documentació estàtica que es pot allotjar en llocs com GitHub Pages.
     * **Confluence:** Eina de documentació col·laborativa. Ideal per a equips grans.
     * **Read the Docs:** Integrat amb Sphinx, facilita la publicació de documentació de projectes Python.
3. **Implementar un sistema de control de versions:**
   * **Git:** El sistema de control de versions més popular. Permet el seguiment de canvis en el codi i la documentació.
   * **Plataformes de repositoris:**
     * **GitHub:** Ofereix eines de col·laboració, integració amb GitHub Pages per a la publicació de documentació.
     * **GitLab:** Ofereix CI/CD integrat i una gestió avançada de projectes.
     * **Bitbucket:** Integració amb Jira, ideal per a equips que ja utilitzen l'ecosistema Atlassian.

#### Exemples pràctics

**Documentació del codi amb Javadoc**

1.  **Comentaris en el codi:**

    ```java
    /**
     * Aquesta classe representa un usuari en el sistema.
     */
    public class Usuari {
        /**
         * Nom de l'usuari.
         */
        private String nom;

        /**
         * Constructor de la classe Usuari.
         * @param nom El nom de l'usuari.
         */
        public Usuari(String nom) {
            this.nom = nom;
        }

        /**
         * Obté el nom de l'usuari.
         * @return El nom de l'usuari.
         */
        public String getNom() {
            return nom;
        }
    }
    ```
2.  **Generació de documentació:**

    ```bash
    javadoc -d ./doc Usuari.java
    ```

    Això generarà la documentació HTML a la carpeta `./doc`.

**Documentació tècnica amb Sphinx**

1.  **Instal·lació de Sphinx:**

    ```bash
    pip install sphinx
    sphinx-quickstart
    ```

    Segueix les instruccions per configurar el projecte de documentació.
2.  **Escriure documentació en reStructuredText:**

    ```rst
    ================
    Guia d'usuari
    ================

    Benvingut a la guia d'usuari de la nostra aplicació web.

    .. toctree::
       :maxdepth: 2
       :caption: Contingut:

    introduccio
    instal·lacio
    us
    ```
3.  **Generació de documentació HTML:**

    ```bash
    make html
    ```

    La documentació generada es trobarà a la carpeta `_build/html`.

**Control de versions amb Git i GitHub**

1.  **Inicialitzar un repositori Git:**

    ```bash
    git init
    ```
2.  **Afegir fitxers i fer un commit:**

    ```bash
    git add .
    git commit -m "Primera versió de la documentació"
    ```
3. **Pujar a GitHub:**
   * Crea un nou repositori a GitHub.
   *   Afegir el repositori remot i pujar els canvis:

       ```bash
       git remote add origin https://github.com/usuari/repositori.git
       git push -u origin master
       ```

####
