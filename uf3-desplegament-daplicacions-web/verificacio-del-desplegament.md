# Verificació del desplegament

Verificar l'execució d'aplicacions web comprovant els paràmetres de configuració de serveis de xarxa és essencial per assegurar-se que l'aplicació funcioni correctament i estigui accessible als usuaris.&#x20;

#### Elements  a verificar en l'execució d'aplicacions web:

1. **Comprovar la configuració del servidor web:**
   * **Configuració del domini i ports:**
     * Assegura't que el servidor web està configurat per escoltar en el port correcte (per exemple, 80 per HTTP o 443 per HTTPS).
     * Verifica que el nom de domini està correctament configurat i apunta a l'adreça IP del servidor.
2. **Revisar els fitxers de configuració del servidor web:**
   * Per a servidors Apache, el fitxer `httpd.conf` o els fitxers dins de `sites-available` i `sites-enabled`.
   * Per a Nginx, el fitxer `nginx.conf` o els fitxers dins de `sites-available` i `sites-enabled`.
   * Comprova configuracions com els Virtual Hosts (Apache) o Server Blocks (Nginx).
3. **Revisar la configuració del tallafocs:**
   * Assegura't que els ports necessaris estan oberts en el tallafocs per permetre el trànsit HTTP/HTTPS.
   * Això es pot fer amb eines com `iptables` en Linux o configurant el tallafocs del sistema operatiu.
4. **Verificar la connectivitat de la base de dades:**
   * Revisa la configuració de connexió a la base de dades (host, port, usuari, contrasenya) en els fitxers de configuració de l'aplicació web.
   * Assegura't que el servidor de base de dades està en funcionament i accepta connexions des del servidor web.
5. **Monitoritzar els registres (logs):**
   * Revisa els registres del servidor web (`access.log` i `error.log` per Apache o Nginx) per detectar errors o problemes de configuració.
   * Revisa els registres de l'aplicació per errors específics de l'aplicació.
6. **Eines de supervisió i diagnòstic:**
   * Utilitza eines com `curl` o `wget` per comprovar la resposta del servidor web.
   * Utilitza navegadors web per accedir a l'aplicació i comprovar la seva funcionalitat.

#### Exemple pràctic:

Suposem que tenim una aplicació web allotjada en un servidor Apache.

1.  **Verificar el Virtual Host en Apache:**

    ```apache
    <VirtualHost *:80>
        ServerAdmin admin@example.com
        ServerName www.example.com
        DocumentRoot /var/www/html/example
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```

    Assegurem  que aquesta configuració existeix i està habilitada (normalment a `sites-available` i enllaçada a `sites-enabled`).
2. Verifica també si el servei DNS és capaç de resoldre el _ServerName_
3.  **Revisar la configuració del tallafocs (ufw):**

    ```bash
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp
    sudo ufw status
    ```

    Això assegura que els ports 80 i 443 estan oberts.
4.  **Verificar la connectivitat a la base de dades:** Suposem que la configuració de la base de dades està en un fitxer `config.php`:

    ```php
    $dbHost = 'localhost';
    $dbUser = 'dbuser';
    $dbPass = 'dbpass';
    $dbName = 'dbname';
    $conn = new mysqli($dbHost, $dbUser, $dbPass, $dbName);

    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }
    ```

    Assegura't que aquests paràmetres són correctes i que la base de dades està en funcionament.
5.  **Revisar els registres:**

    ```bash
    tail -f /var/log/apache2/error.log
    tail -f /var/log/apache2/access.log
    ```

    Aquestes comandes mostren els últims registres i ajuden a identificar problemes.
6.  **Verificar amb eines com `curl`:**

    ```bash
    curl -I http://www.example.com
    ```

    Aquesta comanda mostra la resposta del servidor, incloent els codis d'estat HTTP, que poden ajudar a diagnosticar problemes (per exemple, 200 OK, 404 Not Found, 500 Internal Server Error, etc.).

####
