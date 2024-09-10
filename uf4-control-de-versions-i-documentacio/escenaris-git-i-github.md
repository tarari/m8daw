# Escenaris Git i Github

En un projecte de desenvolupament, l’ús de Git (sistema de control de versions) i GitHub (plataforma de col·laboració basada en Git) és clau per organitzar i gestionar el codi font. Dins la gestió de projectes i repositoris podem trobar-nos amb diverses situacions, podem sintetitzar-les en les següents:

***

### 1. Escenari: Inicialitzar un projecte i pujar-lo a GitHub

* Objectiu: Crear un repositori local de Git, afegir fitxers i pujar-los a un repositori remot de GitHub.

Comandos Git:

```bash
git init                         # Inicialitza un repositori Git local.
git add .                        # Afegeix tots els fitxers al staging area.
git commit -m "Primer commit"     # Crea un commit amb els fitxers afegits.
git remote add origin <URL>       # Enllaça el repositori local amb el repositori remot a GitHub.
git push -u origin main         # Puja el codi a GitHub, i configura `main` com a branca per defecte.
```

\


**Exemple de situació:**

* Acabes de  crear un nou projecte en local i vols sincronitzar-lo amb un repositori remot a GitHub.

***

### 2. Escenari: Treballar en una nova característica (feature branching)

* **Objectiu**: Crear una branch per desenvolupar una nova funcionalitat i després integrar-la amb la branca principal mitjançant una Pull Request a GitHub.

**Comandos Git:**

```bash
git checkout -b feature/nova-funcio  # Crea una nova branch i et desplaça a ella.
git add .                            # Afegeix els canvis.
git commit -m "Implementació de la nova funció"  # Commit dels canvis.
git push origin feature/nova-funcio  # Puja la branch al repositori remot.
```



**Exemple de situació:**

* Estàs treballant en una nova funcionalitat (com ara l'autenticació d'usuaris) i vols mantenir els canvis aïllats de la branca principal fins que estiguin acabats.

**A GitHub:**

* Un cop pujada la branca, obres una Pull Request (PR) des de la branca _feature/nova-funcio_ cap a develop o main. Després d'una revisió, la pots fusionar amb la branca principal.

***

### 3. Escenari: Resoldre conflictes de merge

* Objectiu: Combinar dos branques que han tingut modificacions al mateix fitxer, resultant en conflictes que cal resoldre manualment.

**Comandos Git:**

```bash
git checkout develop               # Canvia a la branca develop.
git pull origin develop            # Actualitza la branca develop amb els últims canvis del remot.
git merge feature/nova-funcio      # Intenta combinar la branch feature/nova-funcio amb develop.
# Si hi ha conflictes, Git t'ho indicarà i hauràs de resoldre'ls manualment als fitxers afectats.
git add <fitxers-afectats>         # Un cop resolts els conflictes, afegeix els fitxers resolts.
git commit -m "Resolució de conflictes"  # Fes commit dels canvis resolts.
```



**Exemple de situació:**

* Dos desenvolupadors han fet canvis al mateix fitxer (per exemple, al **index.php**). Quan intentes fer un merge, Git detecta conflictes i cal resoldre'ls manualment.

***

### 4. Escenari: Clonar un repositori existent de GitHub

* **Objectiu**: Baixar una còpia d'un repositori remot de GitHub per treballar en ell localment.

**Comandos Git:**

```bash
git clone <URL-repositori>  
# Clona el repositori remot a una carpeta local
```



**Exemple de situació:**

* Un nou desenvolupador s'uneix al projecte i ha de clonar el repositori en local per començar a treballar.

***

### 5. Escenari: Actualitzar el repositori local amb els últims canvis

* **Objectiu**: Sincronitzar el repositori local amb els canvis recents fets per altres desenvolupadors al repositori remot.

**Comandos Git:**

```bash
git checkout develop        # Canvia a la branch develop.
git pull origin develop     # Descarrega els canvis de la branch develop des del remot.

```

**Exemple de situació:**

* Un altre desenvolupador ha fet canvis importants a la branca _develop_ i tu vols assegurar-te que tens la versió més recent abans de començar a treballar.

***

### 6. Escenari: Revertir canvis accidentals

* **Objectiu**: Desfer canvis accidentals o commits erronis.

**Comandos Git:**

Revertir canvis locals no comitejats:

```bash
git checkout -- <fitxer>  
# Reverteix els canvis no comitejats d'un fitxer.
```

\


Desfer l'últim commit (mantenint els canvis en l'staging area):

```bash
git reset --soft HEAD~1
```

Desfer l'últim commit (eliminant els canvis):\


```bash
git reset --hard HEAD~1
```

**Exemple de situació:**

* Has comés  un error en un commit recent o has modificat un fitxer per accident i vols tornar a l'estat anterior.

***

### 7. Escenari: Establir un Tag per a una versió de codi

* **Objectiu**: Crear una etiqueta (tag) en Git per marcar una versió important del codi, com una release.

**Comandos Git:**

```bash
git tag -a v1.0 -m "Versió 1.0"   # Crea una etiqueta amb un missatge associat.
git push origin v1.0              # Puja l'etiqueta al repositori remot.
```



**Exemple de situació:**

* Has acabat una versió funcional del projecte i vols marcar la release 1.0 per poder-la identificar fàcilment en el futur.

***

### 8. Escenari: Crear una Release a GitHub

* **Objectiu**: Crear una release formal a GitHub a partir d'una etiqueta (tag).

**A GitHub:**

* Ves al repositori > "Releases" > "Draft a new release".
* Selecciona l'etiqueta (v1.0 creada prèviament) i afegeix una descripció dels canvis importants en aquesta versió.

**Exemple de situació:**

* L'equip ha completat una versió estable i vols compartir una release oficial amb documentació per als usuaris finals o altres desenvolupadors.

***

### 9. Escenari: Recuperar una branca eliminada accidentalment

* **Objectiu**: Restaurar una branch que s'ha eliminat per error.

**Comandos Git:**

```bash
git reflog                         # Mostra l'historial de referències recents.
git checkout -b nom-de-la-branch <commit_hash>  # Restaura la branca a partir del hash d'un commit anterior.

```

**Exemple de situació:**

* Has eliminat accidentalment una branca important, però saps que els commits encara són presents a l'historial de Git.

***

### 10. Escenari: Rebasing per mantenir un historial net

* **Objectiu**: Combinar l'historial de commits de manera lineal, evitant merges innecessaris.

**Comandos Git:**

```bash
git checkout feature/nova-funcio   # Canvia a la branca que vols rebasar.
git fetch origin                   # Descarrega els canvis més recents del remot.
git rebase origin/develop           # Rebase la branch sobre la develop.

```

**Exemple de situació:**

* Vols mantenir un historial de commits net, on tots els commits es basin en el darrer estat de la branca develop en lloc de tenir merges repetitius.

