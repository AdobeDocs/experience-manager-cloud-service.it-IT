---
title: Utilizzo di più archivi
description: Scopri come gestire più archivi Git quando si lavora con Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Utilizzo di più archivi {#working-with-multiple-source-git-repos}

Scopri come gestire più archivi Git quando si lavora con Cloud Manager.

## Sincronizzazione degli archivi Git gestiti dal cliente {#syncing-customer-managed-git-repositories}

Invece di lavorare direttamente con l’archivio Git di Cloud Manager, [I clienti possono lavorare con il proprio archivio Git](integrating-with-git.md) o più archivi git propri. In questi casi, è necessario configurare un processo di sincronizzazione automatizzata per garantire che l’archivio Git di Cloud Manager sia sempre aggiornato.

A seconda della posizione in cui è ospitato l’archivio Git del cliente, per configurare l’automazione è possibile utilizzare un’azione GitHub o una soluzione di integrazione continua come Jenkins. Con l’implementazione di un’automazione, ogni push a un archivio Git di proprietà del cliente può essere inoltrato automaticamente all’archivio Git di Cloud Manager.

Sebbene un’automazione di questo tipo per un singolo archivio Git di proprietà del cliente sia diretta, la configurazione per più archivi richiede una configurazione iniziale. I contenuti di più archivi Git devono essere mappati su directory diverse all’interno del singolo archivio Git di Cloud Manager.  Il provisioning dell’archivio Git di Cloud Manager deve essere effettuato con un Maven principale `pom.xml`, elencando i diversi sottoprogetti nella sezione moduli .

Di seguito è riportato un esempio `pom.xml` file per due archivi git di proprietà del cliente.

* Il primo progetto verrà inserito nella directory denominata `project-a`.
* Il secondo progetto viene inserito nella directory denominata `project-b`.

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

Tale radice `pom.xml` viene inviato a un ramo nell’archivio Git di Cloud Manager. Quindi è necessario configurare i due progetti per inoltrare automaticamente le modifiche all’archivio Git di Cloud Manager.

Una possibile soluzione sarebbe la seguente.

1. Un’azione GitHub può essere attivata da un push a un ramo nel progetto A.
1. L’azione esegue il checkout del progetto A e dell’archivio Git di Cloud Manager e copia tutti i contenuti dal progetto A alla directory `project-a` nell’archivio Git di Cloud Manager.
1. Quindi l&#39;azione eseguirà il commit-push del cambiamento.

Ad esempio, una modifica sul ramo principale nel progetto A viene inviata automaticamente al ramo principale nell’archivio Git di Cloud Manager. Naturalmente, potrebbe esserci una mappatura tra rami come un push a un ramo denominato `dev` nel progetto A viene inviato a un ramo denominato `development` nell’archivio Git di Cloud Manager. Passaggi simili sono necessari per il progetto B.

A seconda della strategia e dei flussi di lavoro di diramazione, la sincronizzazione può essere configurata per diversi rami. Se l’archivio Git utilizzato non fornisce un concetto simile alle azioni GitHub, è possibile anche un’integrazione tramite Jenkins (o simile). In questo caso, un webhook innesca un lavoro Jenkins che fa il lavoro.

Segui questi passaggi per aggiungere una nuova, terza origine o archivio.

1. Aggiungi una nuova azione GitHub al nuovo archivio che invia le modifiche da tale archivio all’archivio Git di Cloud Manager.
1. Esegui questa azione almeno una volta per assicurarti che il codice del progetto sia nell’archivio Git di Cloud Manager.
1. Aggiungi un riferimento alla nuova directory nella directory principale Maven `pom.xml` nell’archivio Git di Cloud Manager.

## Azione GitHub di esempio {#sample-github-action}

Si tratta di un esempio di azione GitHub attivata da un push al ramo principale e quindi da un push in una sottodirectory dell’archivio Git di Cloud Manager. È necessario fornire alle azioni GitHub due segreti, `MAIN_USER` e `MAIN_PASSWORD`, per connettersi e inviare messaggi push all’archivio Git di Cloud Manager.

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
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

L’utilizzo di un’azione GitHub è molto flessibile. È possibile eseguire qualsiasi mappatura tra i rami degli archivi Git e qualsiasi mappatura dei progetti Git separati nel layout di directory del progetto principale.

>[!NOTE]
>
>Lo script di esempio utilizza `git add` per aggiornare il repository. Ciò presuppone che siano incluse le rimozioni. A seconda della configurazione predefinita di Git, potrebbe essere necessario sostituirla con `git add --all`.

## Esempio di processo Jenkins {#sample-jenkins-job}

Questo è uno script di esempio che può essere utilizzato in un processo Jenkins o simile e ha il seguente flusso:

1. Viene attivato da una modifica in un archivio Git.
1. Il lavoro di Jenkins verifica lo stato più recente di quel progetto o ramo.
1. Il processo attiva quindi questo script.
1. Questo script a sua volta estrae l’archivio Git di Cloud Manager e commit il codice del progetto in una sottodirectory.

Il lavoro di Jenkins deve essere fornito con due segreti, `MAIN_USER` e `MAIN_PASSWORD`, per connettersi e inviare messaggi push all’archivio Git di Cloud Manager.

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

Utilizzare un lavoro Jenkins è molto flessibile. È possibile eseguire qualsiasi mappatura tra i rami degli archivi Git e qualsiasi mappatura dei progetti Git separati nel layout di directory del progetto principale.

>[!NOTE]
>
>Lo script di esempio utilizza `git add` per aggiornare il repository. Ciò presuppone che siano incluse le rimozioni. A seconda della configurazione predefinita di Git, potrebbe essere necessario sostituirla con `git add --all`.
