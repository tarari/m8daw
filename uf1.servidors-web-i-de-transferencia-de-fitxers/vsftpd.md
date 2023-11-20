---
description: Servidor de FTP (Debian 12)
---

# VSFTPD



## Usuaris virtuals&#x20;

En l'allotjament compartit de llocs web, molt sovint es necessita independitzar el sistema operatiu i els seus comptes del servei que estem oferint **http** i **ftp**. Vsftpd ho soluciona a través dels usuaris virtuals i la utilitat **db\_util** de vsftd.

Per crear usuaris virtuals amb el servidor FTP vsftpd en Debian, seguirem els següents passos:

1.  **Instal·lar vsftpd:** Assegura't que tens vsftpd instal·lat al teu sistema Debian. Si no és així, pots instal·lar-lo amb la comanda:

    ```bash
    sudo apt-get update
    sudo apt-get install vsftpd
    ```
2.  **Configurar el fitxer vsftpd.conf:** Edita el fitxer de configuració del vsftpd, `/etc/vsftpd.conf`, per permetre usuaris virtuals i establir els paràmetres necessaris. Editem el fitxer:

    ```bash
    sudo nano /etc/vsftpd.conf
    ```

    A continuació, **afegeix** o **modifica** aquests valors:

    ```bash
    listen=YES
    anonymous_enable=NO
    local_enable=NO
    virtual_use_local_privs=YES
    guest_enable=YES
    guest_username=ftp
    user_sub_token=$USER
    local_root=/home/ftp/$USER
    chroot_local_user=YES
    hide_ids=YES
    ```

    Assegura't que la línia `virtual_use_local_privs=YES` està establerta com a "YES" per permetre als usuaris virtuals accedir a fitxers locals.

La variable $USER determina l'usuari privat virtual que s'està utilitzant.



3. **Crea els directoris necessaris:** Crea el directori per a l'emmagatzematge dels usuaris virtuals, i assigna permisos:

```bash
sudo mkdir -p /home/ftp
sudo chmod a-w /home/ftp
```

4. **Crea usuaris virtuals:** Utilitza el mòdul **`db_util`** de vsftpd per afegir els usuaris virtuals. Afegeix un usuari i la seva contrasenya a la base de dades del vsftpd:

```bash
sudo db_util -rv /etc/vsftpd/virtual_users.db add
```

Has de seguir  les instruccions que es mostren a la terminal per afegir els usuaris virtuals.

1.  **Reinicia vsftpd:** Després de fer aquests canvis, reinicia el servei vsftpd per aplicar la nova configuració:

    ```bash
    sudo systemctl restart vsftpd
    ```

Ara hauries de tenir un servidor vsftpd configurat per utilitzar usuaris virtuals en Debian. Pots crear, modificar o eliminar usuaris virtuals amb el mòdul `db_util` segons les teves necessitats.&#x20;

És molt important que  comprenguis els permisos i les configuracions de seguretat que s'apliquen a aquests usuaris virtuals per evitar problemes de seguretat al teu servidor FTP.



## Usuari anònim

Un usuari anònim en el context dels serveis FTP com vsftpd, fa referència a un tipus d'accés que permet a **qualsevol persona connectar-se a un servidor FTP sense haver de proporcionar un nom d'usuari o contrasenya**. En lloc d'utilitzar credencials d'accés específiques, els usuaris anònims tenen permisos limitats i generalment es redirigeixen a un directori específic al qual poden accedir.

**Utilitats**

Aquest tipus d'accés anònim pot ser útil per a la distribució d'arxius o contingut públic en un servidor FTP, com arxius de programari de codi obert, actualitzacions de sistemes o altres continguts disponibles per al públic en general. És important destacar que l'accés anònim, per la seva naturalesa oberta, pot implicar riscos de seguretat si no es configura adequadament.

Amb freqüència, els servidors FTP configuren un directori específic anomenat **`anonymous`** o **`ftp`** al qual els usuaris anònims tenen accés. Aquest directori pot contenir informació o arxius que són accessibles públicament sense requerir autenticació.

### Com es crea?

Per crear un usuari anònim amb el servidor FTP vsftpd i fer-lo compatible amb els usuaris virtuals:

1.  **Modifica la configuració de vsftpd:**

    Edita el fitxer de configuració del vsftpd, `/etc/vsftpd.conf`:

    ```bash
    sudo nano /etc/vsftpd.conf
    ```

    Modifica o afegeix aquestes línies per permetre l'accés anònim i fer-lo compatible amb els usuaris virtuals:

    ```bash
    anonymous_enable=YES
    anon_root=/home/ftp
    no_anon_password=YES
    ```

    Aquesta configuració permetrà que els usuaris anònims accedeixin a la carpeta `/home/ftp` sense una contrasenya. Assegura't que aquesta carpeta estigui disponible i tingui els permisos adequats a l'usuari de compte `ftp`.
2.  **Configura els usuaris virtuals compatibles amb l'accés anònim:**

    Els usuaris virtuals poden coexistir amb l'accés anònim. Quan configures els usuaris virtuals, assegura't que els seus directoris es trobin dins del directori que has designat per als usuaris anònims (`/home/ftp` en aquest cas). Això permetrà que tant els usuaris virtuals com els usuaris anònims accedeixin als seus directoris corresponents.
3.  **Reinicia vsftpd:**

    Després de fer aquests canvis, reinicia el servei vsftpd per aplicar la nova configuració:

    ```bash
    sudo systemctl restart vsftpd
    ```

Ara hauríem  de tenir tant usuaris virtuals com accesos anònims funcionant al servidor vsftpd. Els usuaris virtuals poden tenir els seus propis directoris dins del directori `/home/ftp`, mentre que l'accés anònim estarà limitat al directori establert com a `anon_root`. Assegurem-nos de comprovar adequadament els permisos dels directoris per evitar problemes de seguretat o conflictes entre usuaris.
