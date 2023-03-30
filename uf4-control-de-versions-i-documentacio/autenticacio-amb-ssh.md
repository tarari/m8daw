# Autenticació amb SSH

Fent servir el protocol SSH, ens podem connectar i autenticar amb serveis i servidors remots. Amb les claus SSH pots connectar-te a GitHub sense necessitat de proporcionar el nom d'usuari i el personal access token a cada visita. També podeu utilitzar una clau SSH per signar confirmacions.

### Agent SSH

L'agent SSH ens permet el reenviament de claus SSH de forma segura quan són sol·licitades.

Primer, assegurem-nos que la nostra clau està correctament configurada:

```sh
$ ssh -T git@github.com
# Attempt to SSH in to github
> Hi USERNAME! You've successfully authenticated, but GitHub does not provide
> shell access.
```

És recomanable que l'accés als repositoris GitHub siguin a través de ssh:

```sh
[remote "origin"]
  url = git@github.com:YOUR_ACCOUNT/YOUR_PROJECT.git
  fetch = +refs/heads/*:refs/remotes/origin/*
```

#### La clau  ha  d'estar disponible per a `ssh-agent` <a href="#your-key-must-be-available-to-ssh-agent" id="your-key-must-be-available-to-ssh-agent"></a>

```sh
ssh-add -L
```
