---
title: Utilizzo di più repository Git di origine
description: Utilizzo di più repository Git sorgente - Cloud Services
translation-type: tm+mt
source-git-commit: e8cfe8eeec697fe74da02e178a89fc7a0e22d441
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---


# Utilizzo di più repository Git di origine {#working-with-multiple-source-git-repos}


## Sincronizzazione dei repository Git gestiti dal cliente {#syncing-customer-managed-git-repositories}

Invece di lavorare direttamente con l&#39;archivio Git di Cloud Manager, i clienti possono lavorare con il proprio repository Git o con più repository Git. In questi casi, è necessario configurare un processo di sincronizzazione automatizzata per garantire che l&#39;archivio Git di Cloud Manager sia sempre aggiornato. A seconda della posizione in cui è ospitato il repository Git del cliente, è possibile utilizzare un&#39;azione GitHub o una soluzione di integrazione continua come Jenkins per configurare l&#39;automazione. Grazie all&#39;automazione, ogni push a un repository Git di proprietà del cliente può essere automaticamente inoltrato al repository Git di Cloud Manager.

Anche se tale automazione per un singolo repository Git di proprietà di un cliente è semplice, l&#39;impostazione per più repository richiede una configurazione iniziale. I contenuti dei repository Git multipli devono essere mappati su directory diverse all&#39;interno del repository Git di Single Cloud Manager.  L&#39;archivio Git di Cloud Manager deve essere fornito con un master Maven, in cui sono elencati i diversi sottoprogetti nella sezione dei moduli

Di seguito è riportato un esempio di cartella per due repository Git di proprietà del cliente: il primo progetto verrà inserito nella directory `project-a`, il secondo nella directory `project-b`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

Tale cartella principale viene inserita in un ramo nell&#39;archivio Git di Cloud Manager. I due progetti devono quindi essere configurati per inoltrare automaticamente le modifiche al repository Git di Cloud Manager.

Ad esempio, un&#39;azione GitHub può essere attivata da un push a un ramo nel progetto A. L&#39;azione eseguirà il checkout del progetto A e dell&#39;archivio Git di Cloud Manager, copierà tutti i contenuti dal progetto A alla directory `project-a` nell&#39;archivio Git di Cloud Manager, quindi eseguirà il commit-push della modifica. Ad esempio, una modifica sul ramo principale del progetto A viene automaticamente inserita nel ramo principale del repository git di Cloud Manager. Naturalmente, potrebbe esserci una mappatura tra rami come il push a un ramo denominato &quot;dev&quot; nel progetto A viene inviato a un ramo denominato &quot;development&quot; nell&#39;archivio Git di Cloud Manager. Passaggi simili sono richiesti per il progetto B.

A seconda della strategia di ramificazione e dei flussi di lavoro, la sincronizzazione può essere configurata per diversi rami. Se l’archivio Git utilizzato non fornisce un concetto simile alle azioni GitHub, è possibile effettuare un’integrazione anche tramite Jenkins (o simili). In questo caso, un webhook attiva un processo Jenkins che esegue il lavoro.

Per aggiungere una nuova origine o un repository, effettuate le operazioni seguenti:

1. Aggiungi una nuova azione GitHub al nuovo archivio che invia le modifiche da tale repository al repository Git di Cloud Manager.
1. Eseguite questa azione almeno una volta per assicurarvi che il codice del progetto sia nell&#39;archivio Git di Cloud Manager.
1. Aggiungete un riferimento alla nuova directory nella directory principale Maven nell&#39;archivio Git di Cloud Manager.


## Azione GitHub di esempio {#sample-github-action}

Si tratta di un&#39;azione GitHub di esempio attivata da un push al ramo principale per poi passare a una sottodirectory dell&#39;archivio Git di Cloud Manager. Le azioni GitHub devono essere fornite con due segreti, `MAIN_USER` e `MAIN_PASSWORD`, per essere in grado di connettersi e inviare i dati all&#39;archivio Git di Cloud Manager.

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
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
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

Come mostrato sopra, l&#39;utilizzo di un&#39;azione GitHub è molto flessibile. È possibile eseguire qualsiasi mappatura tra rami dei repository Git, nonché mappatura dei progetti git separati nel layout di directory del progetto principale.

>[!NOTE]
>Lo script di cui sopra utilizza `git add` per aggiornare il repository, che presuppone che siano inclusi i rimozioni, a seconda della configurazione predefinita di Git, che deve essere sostituito con `git add --all`.

## Esempio di processo Jenkins {#sample-jenkins-job}

Si tratta di uno script di esempio che può essere utilizzato in un processo Jenkins o in un processo simile. Viene attivato da una modifica in un repository Git. Il processo Jenkins verifica lo stato più recente del progetto o del ramo e quindi attiva lo script.

Questo script a sua volta estrae l&#39;archivio Git di Cloud Manager e impegna il codice del progetto in una sottodirectory.

Il processo Jenkins deve essere dotato di due segreti, `MAIN_USER` e `MAIN_PASSWORD`, per essere in grado di connettersi e inviare i dati all&#39;archivio Git di Cloud Manager.

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

Come mostrato sopra, l&#39;utilizzo di un lavoro Jenkins è molto flessibile. È possibile eseguire qualsiasi mappatura tra rami dei repository Git, nonché mappatura dei progetti Git separati nel layout di directory del progetto principale.

>[!NOTE]
>Lo script di cui sopra utilizza `git add` per aggiornare il repository, che presuppone che siano inclusi i rimozioni, a seconda della configurazione predefinita di Git, che deve essere sostituito con `git add --all`.