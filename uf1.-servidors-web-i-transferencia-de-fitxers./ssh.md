---
description: Secure Shell
---

# SSH

Connexió segura de shell

## SSH General

| Acció | Comanda |
| :--- | :--- |
| Accés a servidor remot \(Afegeix IP del client a la llista _known\_hosts_\) | `ssh IP , ssh nomDNS` |
| Accés especificant usuari |  `ssh username@host_o_IP` |
| Connexió a port diferente del 22 | `ssh IP_host  -p <nport>` |
| Connexió amb fitxer de certificat | `ssh -i /path/file.pem user@sever` |
| Generar un parell de clau privada/pública \(dins ~/.ssh\) | `ssh-keygen` |

\`\`

### scp

Copiar fitxers de client a remot o viceversa

De local a remot, amb l'usuari toni de l'equip 123.123.123.123, a la carpeta personal de l'usuari:

`scp bar.txt toni@123.123.123.123:~/`

I al revés, creant en local un nou fitxer anomenat _new.txt_

`scp toni@123.123.123.123:~/bar.txt ./new.txt`

