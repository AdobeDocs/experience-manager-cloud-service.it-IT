---
title: Utilizzare più archivi
description: Scopri come gestire più archivi Git con Cloud Manager.
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 31%

---

# Utilizzare più archivi {#working-with-multiple-source-git-repos}

Scopri come gestire più archivi Git con Cloud Manager.

## Sincronizza archivi Git privati {#syncing-customer-managed-git-repositories}

Anziché utilizzare direttamente l&#39;archivio Git di Cloud Manager, i [clienti possono utilizzare un proprio archivio Git privato](integrating-with-git.md) o più archivi Git personali. In questi casi, imposta un processo di sincronizzazione automatizzato per garantire che l’archivio Git in Cloud Manager sia sempre aggiornato.

A seconda della posizione in cui è ospitato l’archivio Git del cliente, per configurare l’automazione è possibile utilizzare un’azione GitHub o una soluzione di integrazione continua come Jenkins. Con l’implementazione dell’automazione, ogni push in un archivio Git del cliente può essere inoltrato automaticamente all’archivio Git di Cloud Manager.

Sebbene un’automazione di questo tipo per un singolo archivio Git di proprietà del cliente sia diretta, la sua configurazione per più archivi richiede una configurazione iniziale. I contenuti di più archivi Git devono essere mappati su directory diverse all’interno del singolo archivio Git di Cloud Manager. Il provisioning dell’archivio Git di Cloud Manager deve essere eseguito con una radice Maven `pom.xml`, elencando i diversi sottoprogetti nella sezione moduli.

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

Tale radice `pom.xml` viene inviata a un ramo nell’archivio Git di Cloud Manager. Quindi, è necessario configurare i due progetti per inoltrare automaticamente le modifiche all’archivio Git di Cloud Manager.

Di seguito viene indicata una possibile soluzione.

1. Attiva un’azione GitHub inviandola a un ramo nel progetto A.
1. L’azione verifica il progetto A e l’archivio Git di Cloud Manager. Quindi copia tutto il contenuto del progetto A nella directory `project-a` nell&#39;archivio Git di Cloud Manager.
1. Quindi l’azione esegue il commit e invia la modifica.

Ad esempio, una modifica sul ramo principale nel progetto A viene inviata automaticamente al ramo principale nell’archivio Git di Cloud Manager. Potrebbe essere presente una mappatura tra rami, ad esempio un push in un ramo denominato `dev` nel progetto A viene inviato a un ramo denominato `development` nell&#39;archivio Git di Cloud Manager. Il progetto B richiede una procedura analoga.

In base alla strategia e ai flussi di lavoro impiegati per i rami, è possibile configurare la sincronizzazione per diversi rami. Se l’archivio Git utilizzato non fornisce un concetto simile alle azioni GitHub, è possibile anche un’integrazione tramite Jenkins (o simile). In questo caso, un webhook attiva un processo Jenkins, che esegue l’operazione.

Segui questi passaggi per aggiungere una nuova terza origine o archivio.

1. Aggiungi un’azione GitHub al nuovo archivio, che invia le modifiche da tale archivio all’archivio Git di Cloud Manager.
1. Esegui questa azione almeno una volta per verificare che il codice del progetto sia riportato nell’archivio Git di Cloud Manager.
1. Nell&#39;archivio Git di Cloud Manager, aggiungere un riferimento alla nuova directory nella radice Maven `pom.xml`.



## Azione GitHub di esempio {#sample-github-action}

Di seguito è riportato un esempio di azione GitHub attivata da un invio al ramo principale. Quindi esegui il push in una sottodirectory dell’archivio Git di Cloud Manager. Per connettersi ed eseguire il push all&#39;archivio Git di Cloud Manager, è necessario fornire alle azioni GitHub due segreti, `MAIN_USER` e `MAIN_PASSWORD`.

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

L’utilizzo di un’azione GitHub è flessibile. È possibile eseguire qualsiasi mappatura tra i rami degli archivi Git e qualsiasi mappatura di progetti Git distinti nel layout di directory del progetto principale.

>[!NOTE]
>
>Lo script di esempio utilizza `git add` per aggiornare l’archivio. Lo script presuppone che siano incluse le rimozioni. A seconda della configurazione predefinita di Git, deve essere sostituito con `git add --all`.

## Esempio di processo Jenkins {#sample-jenkins-job}

Di seguito è riportato uno script di esempio che può essere utilizzato in un processo Jenkins o simile e ha il seguente flusso:

1. Viene attivato da una modifica in un archivio Git.
1. Il processo Jenkins verifica lo stato più recente del progetto o ramo in questione.
1. A questo punto, il processo attiva lo script.
1. Questo script a sua volta verifica l’archivio Git di Cloud Manager e conferma il codice del progetto in una sottodirectory.

Il processo Jenkins deve essere fornito con due segreti, `MAIN_USER` e `MAIN_PASSWORD`, per connettersi e inviare messaggi push all&#39;archivio Git di Cloud Manager.

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

L’utilizzo di un processo Jenkins è flessibile. È possibile eseguire qualsiasi mappatura tra i rami degli archivi Git e qualsiasi mappatura di progetti Git distinti nel layout di directory del progetto principale.

>[!NOTE]
>
>Lo script di esempio utilizza `git add` per aggiornare l’archivio. Lo script presuppone che siano incluse le rimozioni. A seconda della configurazione predefinita di Git, deve essere sostituito con `git add --all`.
