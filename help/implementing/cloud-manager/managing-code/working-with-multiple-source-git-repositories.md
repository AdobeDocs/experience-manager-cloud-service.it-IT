---
title: Utilizzo di più archivi
description: Scopri come gestire più archivi Git con Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '752'
ht-degree: 100%

---

# Utilizzo di più archivi {#working-with-multiple-source-git-repos}

Scopri come gestire più archivi Git con Cloud Manager.

## Sincronizzazione degli archivi Git gestiti dal cliente {#syncing-customer-managed-git-repositories}

Anziché utilizzare direttamente l’archivio Git di Cloud Manager, [gli utenti possono utilizzare uno o più archivi Git](integrating-with-git.md) personali. In questi casi è necessario configurare un processo di sincronizzazione automatica per garantire che l’archivio Git di Cloud Manager sia sempre aggiornato.

A seconda della posizione in cui è ospitato l’archivio Git del cliente, per configurare l’automazione è possibile utilizzare un’azione GitHub o una soluzione di integrazione continua come Jenkins. Con l’implementazione dell’automazione, ogni push in un archivio Git del cliente viene inviato automaticamente all’archivio Git di Cloud Manager.

Sebbene un’automazione di questo tipo per un singolo archivio Git del cliente possa essere configurata direttamente, per più archivi è necessaria una configurazione iniziale. I contenuti di più archivi Git devono essere associati a diverse directory all’interno del singolo archivio Git di Cloud Manager. Il provisioning dell’archivio Git di Cloud Manager deve essere eseguito con un file radice Maven `pom.xml`, elencando i diversi progetti secondari nella sezione moduli.

Di seguito è riportato un file `pom.xml` di esempio per due archivi Git del cliente.

* Il primo progetto viene aggiunto alla directory denominata `project-a`.
* Il secondo progetto viene aggiunto alla directory denominata `project-b`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
  
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
  
</project>
```

Viene eseguito il push di un file radice `pom.xml` in un ramo nell’archivio Git di Cloud Manager. A questo punto è necessario configurare i due progetti affinché inoltrino automaticamente le modifiche all’archivio Git di Cloud Manager.

Di seguito viene indicata una possibile soluzione.

1. È possibile attivare un’azione GitHub con un push in uno dei rami nel progetto A.
1. L’azione estrae il progetto A e l’archivio Git di Cloud Manager e copia tutti i contenuti del progetto A nella directory `project-a` contenuta nell’archivio Git di Cloud Manager.
1. A quel punto l’azione eseguirà i comandi commit-push della modifica.

Ad esempio, il push di una modifica apportata al ramo principale nel progetto A viene eseguito automaticamente nel ramo principale dell’archivio Git di Cloud Manager. Naturalmente potrebbe essere presente una mappatura tra rami, come nel caso in cui il push in un ramo denominato `dev` nel progetto A venga eseguito in un ramo denominato `development` nell’archivio Git di Cloud Manager. Il progetto B richiede una procedura analoga.

In base alla strategia e ai flussi di lavoro impiegati per i rami, è possibile configurare la sincronizzazione per diversi rami. Se l’archivio Git utilizzato non fornisce un concetto simile alle azioni GitHub, è possibile optare anche per un’integrazione tramite Jenkins (o processo analogo). In questo caso, un webhook attiva un processo Jenkins per eseguire l’operazione.

Per aggiungere una terza nuova origine o archivio, segui la procedura riportata di seguito.

1. Aggiungi al nuovo archivio una nuova azione GitHub per eseguire il push delle modifiche da tale archivio all’archivio Git di Cloud Manager.
1. Esegui questa azione almeno una volta per verificare che il codice del progetto sia riportato nell’archivio Git di Cloud Manager.
1. Aggiungi un riferimento alla nuova directory nel file radice Maven `pom.xml` nell’archivio Git di Cloud Manager.

## Azione GitHub di esempio {#sample-github-action}

Questo è un esempio di azione GitHub attivata da un push nel ramo principale e quindi da un push in una directory secondaria dell’archivio Git di Cloud Manager. Per connettersi ed eseguire il push all’archivio Git di Cloud Manager, le azioni GitHub devono avere due segreti, `MAIN_USER` e `MAIN_PASSWORD`.

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

L’utilizzo di un’azione GitHub è molto flessibile. È possibile eseguire qualsiasi mappatura tra i rami degli archivi Git e qualsiasi mappatura di progetti Git distinti nel layout di directory del progetto principale.

>[!NOTE]
>
>Lo script di esempio utilizza `git add` per aggiornare l’archivio. Ciò presuppone che siano incluse le rimozioni. A seconda della configurazione predefinita di Git, potrebbe essere necessario sostituirlo con `git add --all`.

## Esempio di processo Jenkins {#sample-jenkins-job}

Questo è uno script di esempio che puoi utilizzare in un processo Jenkins o di tipo analogo. Presenta il seguente flusso:

1. Viene attivato da una modifica apportata in un archivio Git.
1. Il processo Jenkins verifica lo stato più recente del progetto o ramo in questione.
1. A questo punto, il processo attiva lo script.
1. Lo script a sua volta estrae l’archivio Git di Cloud Manager ed esegue il commit del codice del progetto in una directory secondaria.

Per connettersi ed eseguire il push all’archivio Git di Cloud Manager, il processo Jenkins deve avere due segreti, `MAIN_USER` e `MAIN_PASSWORD`.

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

L’utilizzo di un processo Jenkins è molto flessibile. È possibile eseguire qualsiasi mappatura tra i rami degli archivi Git e qualsiasi mappatura di progetti Git distinti nel layout di directory del progetto principale.

>[!NOTE]
>
>Lo script di esempio utilizza `git add` per aggiornare l’archivio. Ciò presuppone che siano incluse le rimozioni. A seconda della configurazione predefinita di Git, potrebbe essere necessario sostituirlo con `git add --all`.
