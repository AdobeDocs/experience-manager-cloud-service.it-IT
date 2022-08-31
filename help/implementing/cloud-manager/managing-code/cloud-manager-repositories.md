---
title: Repository di Cloud Manager
description: Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Repository di Cloud Manager {#cloud-manager-repos}

Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.

>[!NOTE]
>
>Esiste un limite di 300 archivi in tutti i programmi di una determinata azienda o organizzazione IMS.

## Aggiunta e gestione di archivi {#add-manage-repos}

Segui questi passaggi per visualizzare e gestire gli archivi in Cloud Manager.

1. Da **Panoramica del programma** pagina, fai clic su **Repository** e passa alla **Repository** pagina.

1. Fai clic su **Aggiungi archivio** per avviare la procedura guidata.

   ![Pulsante Aggiungi repository](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Inserisci il nome e la descrizione come richiesto e fai clic su **Salva**.

   ![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/assets/repos/repo-1.png)

Al termine della procedura guidata, il nuovo archivio verrà visualizzato nella tabella.

Puoi selezionare il repository nella tabella e fare clic sul pulsante con i puntini di sospensione e selezionare **Copia URL archivio**, **Visualizza e aggiorna** oppure **Elimina**.

![Opzioni archivio](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Gli archivi creati in Cloud Manager saranno disponibili anche per la selezione al momento dell’aggiunta o della modifica delle pipeline. Fare riferimento al documento [Pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) per saperne di più.

Esiste un singolo archivio principale o un ramo per una determinata pipeline. Con [supporto dei sottomoduli git](#git-submodule-support), molti rami secondari possono essere inclusi in fase di creazione.

>[!NOTE]
>
>Un utente deve avere il ruolo **Gestione distribuzione** o **Proprietario business** per poter aggiungere un archivio.

## Eliminazione di un archivio {#delete-repo}

L&#39;eliminazione di un repository comporta:

* Rendi il nome del repository eliminato inutilizzabile per i nuovi archivi che possono essere creati in futuro.
   * Messaggio di errore `Repository name should be unique within organization.` in tali casi.
* Rendi l’archivio eliminato non disponibile in Cloud Manager e non disponibile per il collegamento a una pipeline.

Segui questi passaggi per eliminare un archivio in Cloud Manager.

1. Da **Panoramica del programma** pagina, fai clic su **Repository** e passa alla **Repository** pagina.

1. Seleziona il repository e fai clic sul pulsante dei puntini di sospensione e seleziona **Elimina** per eliminare il repository.

   ![Elimina archivio](/help/implementing/cloud-manager/assets/repos/delete-repo.png)

## Supporto per i sottomoduli Git {#git-submodule-support}

I sottomoduli Git possono essere utilizzati per unire il contenuto di più rami tra archivi Git in fase di creazione.

Quando viene eseguito il processo di creazione di Cloud Manager, dopo che l’archivio configurato per la pipeline è stato clonato e il ramo configurato viene estratto, se il ramo contiene un `.gitmodules` file nella directory principale, il comando viene eseguito.

Il comando seguente estrae ogni sottomodulo nella directory appropriata.

```
$ git submodule update --init
```

Questa tecnica rappresenta una potenziale alternativa alla soluzione descritta nel documento [Utilizzo di più archivi Git di origine](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) per le organizzazioni che hanno familiarità con l’utilizzo dei sottomoduli git e che non desiderano gestire un processo di unione esterno.

Ad esempio, supponiamo che ci siano tre archivi, ciascuno contenente un singolo ramo denominato `main`. Nell’archivio principale, ovvero quello configurato nelle pipeline, il `main` un ramo `pom.xml` file che dichiara i progetti contenuti negli altri due archivi.

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

Aggiungeresti quindi i sottomoduli per gli altri due archivi.

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Questo determina un `.gitmodules` simile al seguente.

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Ulteriori informazioni sui sottomoduli git sono disponibili nella sezione [Manuale Di Riferimento Git.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Limitazioni e consigli {#limitations-recommendations}

Quando utilizzi i sottomoduli git, tieni presente le seguenti limitazioni.

* L’URL Git deve essere esattamente nella sintassi descritta nella sezione precedente.
* Sono supportati solo i sottomoduli nella directory principale del ramo.
* Per motivi di sicurezza, non incorporare le credenziali negli URL Git.
* Se non diversamente necessario, si consiglia vivamente di utilizzare sottomoduli superficiali.
   * Per eseguire questa operazione, esegui `git config -f .gitmodules submodule.<submodule path>.shallow true` per ciascun sottomodulo.
* I riferimenti ai sottomoduli Git vengono archiviati in commit specifici Git. Di conseguenza, quando vengono apportate modifiche all’archivio dei sottomoduli, il commit a cui si fa riferimento deve essere aggiornato.
   * Ad esempio, utilizzando `git submodule update --remote`
