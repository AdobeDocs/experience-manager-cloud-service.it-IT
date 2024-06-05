---
title: Archivi di Cloud Manager
description: Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 84%

---


# Archivi di Cloud Manager {#cloud-manager-repos}

Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.

>[!NOTE]
>
>Per ogni azienda o organizzazione IMS, vi è un limite di 300 archivi per tutti i programmi.

## Aggiunta e gestione degli archivi {#add-manage-repos}

Per visualizzare e gestire gli archivi in Cloud Manager, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla sezione **Panoramica del programma** , seleziona la **Archivi** per passare alla scheda **Archivi** pagina.

1. Clic **Aggiungi archivio**.

   ![Pulsante Aggiungi archivio](/help/implementing/cloud-manager/assets/repos/create-repo2.png)

1. Inserisci il nome e la descrizione come richiesto e fai clic su **Salva**.

   ![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/assets/repos/repo-1.png)

Al termine della procedura guidata, il nuovo archivio viene visualizzato nella tabella.

Puoi selezionare l’archivio nella tabella, fare clic sul pulsante con i puntini di sospensione e selezionare **Copia URL archivio**, **Visualizza e aggiorna**, o **Elimina**.

![Opzioni dell’archivio](/help/implementing/cloud-manager/assets/repos/create-repo3.png)

Gli archivi creati in Cloud Manager sono disponibili per la selezione anche quando aggiungi o modifichi le pipeline. Per ulteriori informazioni, consulta [Pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Esiste un singolo archivio principale o ramo per ogni pipeline. Grazie al [supporto per i moduli Git secondari](#git-submodule-support), molti rami secondari possono essere aggiunti al momento della generazione.

>[!NOTE]
>
>Per poter aggiungere un archivio, l’utente deve avere il ruolo **Responsabile dell’implementazione** o **Proprietario business**.

## Eliminazione di un archivio {#delete-repo}

L’eliminazione di un archivio:

* Rende il nome dell’archivio eliminato inutilizzabile per i nuovi archivi che possono essere creati in futuro.
   * In tali casi viene visualizzato il messaggio di errore `Repository name should be unique within organization.`.
* Rende l’archivio eliminato non disponibile in Cloud Manager e non disponibile per il collegamento a una pipeline.

Per eliminare un archivio in Cloud Manager, segui la procedura riportata di seguito.

1. Dalla sezione **Panoramica del programma** , fare clic su **Archivi** e passare alla scheda **Archivi** pagina.

1. Seleziona l’archivio, fai clic sul pulsante con i puntini di sospensione e seleziona **Elimina** per eliminare l’archivio.

## Supporto per i moduli Git secondari {#git-submodule-support}

È possibile utilizzare i moduli Git secondari per unire il contenuto di più rami tra archivi Git al momento della generazione.

Quando viene eseguito il processo di build di Cloud Manager, dopo la clonazione dell’archivio configurato per la pipeline e l’estrazione del ramo configurato, se il ramo contiene un file `.gitmodules` nella directory radice il comando viene eseguito.

Il comando seguente estrae ogni modulo secondario nella directory appropriata.

```
$ git submodule update --init
```

Questa tecnica rappresenta una potenziale alternativa alla soluzione descritta nel documento [Utilizzo di più archivi Git di origine](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) per le organizzazioni che hanno familiarità con l’utilizzo dei moduli Git secondari e non desiderano gestire un processo di unione esterno.

Supponiamo ad esempio la presenza di tre archivi, ciascuno contenente un singolo ramo denominato `main`. Nell’archivio principale, ovvero quello configurato nelle pipeline, il ramo `main` include un file `pom.xml` dove sono riportati i progetti contenuti negli altri due archivi.

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

A questo punto, si aggiungono i moduli secondari degli altri due archivi.

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Questo determina un file `.gitmodules` simile al seguente.

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

Per ulteriori informazioni sui moduli Git secondari, consulta il [Manuale di riferimento Git.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Limitazioni e consigli {#limitations-recommendations}

Quando utilizzi dei moduli Git secondari, tieni presente le seguenti limitazioni.

* La sintassi dell’URL Git deve essere esattamente quella descritta nella sezione precedente.
* I moduli secondari sono supportati unicamente nella radice del ramo.
* Per motivi di sicurezza, non incorporare le credenziali negli URL Git.
* Se non diversamente necessario, è consigliabile utilizzare dei moduli secondari superficiali.
   * Per eseguire l’operazione, esegui `git config -f .gitmodules submodule.<submodule path>.shallow true` per ciascun modulo secondario.
* I riferimenti ai moduli Git secondari vengono archiviati in commit Git specifici. Di conseguenza, quando vengono apportate modifiche all’archivio dei sottomoduli, il commit a cui si fa riferimento deve essere aggiornato.
   * Ad esempio, utilizzando `git submodule update --remote`. 
