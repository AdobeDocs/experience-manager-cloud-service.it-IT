---
title: Gestire i registri - Cloud Service
description: Gestire i registri - Cloud Service
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: 8a70a343be8a6843436f1df26adae5b1935ad4c3
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 16%

---

# Accesso e gestione dei registri {#manage-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato utilizzando la scheda Ambiente. Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

## Download dei registri {#download-logs}

Questi file possono essere scaricati tramite l&#39;interfaccia utente, dalla scheda **Ambienti** dalla pagina **Panoramica** :

![](assets/download-logs1.png)

Oppure, dalla pagina Dettagli ambiente :

![](assets/download-logs.png)

>[!NOTE]
>Indipendentemente da dove viene aperto, viene visualizzata la stessa finestra di dialogo e consente di scaricare un singolo file di log.

![](assets/download-logs2.png)

## Download dei registri per il servizio di anteprima {#download-preview-service}

Segui i passaggi riportati di seguito per scaricare i registri del servizio Preview

1. Passa alla scheda **Ambienti** dalla pagina **Panoramica** di Cloud Manager.

1. Seleziona **Download Logs** dal **...Menu** .

1. Dal menu a discesa **Servizio**, seleziona **Anteprima** o **Anteprima Dispatcher**, quindi fai clic sull&#39;icona di download.

   >[!NOTE]
   >Puoi eseguire questa azione anche dalla pagina dei dettagli dell’ambiente .

   ![](assets/download-preview.png)


## Effettua l’accesso tramite API {#logs-through-api}

Oltre a scaricare i registri tramite l’interfaccia utente, i registri saranno disponibili tramite l’API e l’interfaccia della riga di comando.

Ad esempio, per scaricare i file di registro per un ambiente specifico, il comando è qualcosa di unico nelle righe di

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

Il seguente comando consente la coda dei log:

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Per ottenere l’ID ambiente (in questo caso 1884) e le opzioni del servizio o del nome di registro disponibili puoi utilizzare:

```java
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

>[!NOTE]
>Mentre i **Log Downloads** (Download dei registri) saranno disponibili sia dall’interfaccia utente che tramite l’API, **Log Tailing** (Coda del registro) è accessibile solo con API/CLI.

### Risorse aggiuntive {#resources}

Per ulteriori informazioni sull’API di Cloud Manager e su Adobe I/O CLI, consulta le seguenti risorse aggiuntive:

* [Documentazione API di Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
