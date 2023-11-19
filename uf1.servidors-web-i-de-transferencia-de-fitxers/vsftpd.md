---
description: Servidor de FTP (Debian 12)
---

# VSFTPD

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
