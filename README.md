### Istruzioni per sviluppare in WSL linux da Visual Studio Code in Windows

## prerequisiti

- avere un account GITHUB
- avere installato WSL (wsl2) linux e una distribuzione di Linux (Ubuntu)
- avere installato VSC con l'estensione WSL di Microsoft


## configurazione SSH

In ubuntu bisogna creare una coppia di chiavi (privata e pubblica) e settare la chiave pubblica su GITHUB

Per creare la coppia di chiavi usare il comando seguente mettendo come email quella del proprio account github e come cognome il proprio, vi sarà richiesto di scegliere una password (mentre le digitate non è visualizzata):

```shell
ssh-keygen -t ed25519 -C "email@email.com" -f $HOME/.ssh/id_cognome
```

Va quindi collegata la chiave pubblica (estensione .pub) al vostro account GITHUB. 
Eseguiamo il seguente comando per visualizzare la chiave pubblica (mettendo il proprio cognome)

```shell
cat $HOME/.ssh/id_cognome.pub
```

Copiare l'output del comando e incollare in GITHUB -> click sulla icona del profilo -> settings -> SSH and GPG Keys -> ADD new SSH key  (scegliere un title a piacere)


## attivazione della chiave


Eseguire i seguenti due comandi, inserire la password della chiave privata quando richiesto:


```shell
eval $(ssh-agent -s)
```

```shell
ssh-add $HOME/.ssh/id_cognome
```

Attenzione questa operazione andrà ripetuta ogni volta che prendete il computer e iniziate a lavorare su un progetto GITHUB.

## clonare un repository

Per avere una copia locale di un repository GITHUB eseguire i seguenti comandi, sostituendo "username" e "repository" con l'username GITHUB che ha creato il repository e il nome del repository. Attenz

```shell
mkdir /mnt/c/TPS
```

```shell
mkdir /mnt/c/TPS/repository
```

```shell
git clone git@github.com:username/repository.git 
```

```shell
cd /mnt/c/TPS/repository
```

```shell
git remote set-url origin git@github.com:username/repository.git
```

## collegare le proprie credenziali al repository. Inserire la propria email GITHUB e il proprio username GITHUB

```shell
git config user.email "email@email.com"
```

```shell
git config user.name "username"
```

## Avviare VSC

Lanciare i comandi seguenti, sostituendo "repository" con il nome del repository.

```shell
cd /mnt/c/TPS/repository
```

```shell
code .
```


## testare il funzionamento

Creare un file in in VSC con nome "test_cognome.txt" inserendo la parola "test" come contenuto.

- Quindi aggiungere il file a GIT (cliccare su icona del ramo) quindi "+" sul file.
- Committare inserendo un messaggio di commit.
- aprire un terminale da VSC ed eseguire i comandi:

```shell
git push
```

```shell
git pull
```

Andare su GITHUB e verificare che il file sia arrivato sul repository:

https://github.com/username/repository