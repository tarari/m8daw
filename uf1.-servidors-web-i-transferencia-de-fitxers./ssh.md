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

