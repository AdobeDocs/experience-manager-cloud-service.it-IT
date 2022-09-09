---
title: Accesso e gestione dei registri
description: Scopri come accedere ai registri e gestirli per facilitare il processo di sviluppo in AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 8%

---


# Accesso e gestione dei registri {#manage-logs}

Scopri come accedere ai registri e gestirli per facilitare il processo di sviluppo in AEM as a Cloud Service.

Puoi accedere a un elenco dei file di registro disponibili per l’ambiente selezionato utilizzando **Ambienti** scheda da **Panoramica** pagina o pagina Dettagli ambiente.

## Download dei registri {#download-logs}

Segui questi passaggi per scaricare i registri.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** scheda da **Panoramica** pagina.

1. Seleziona **Download dei registri** dal menu ellissi.

   ![Voce di menu dei registri di download](assets/download-logs1.png)

1. In **Download dei registri** seleziona la finestra di dialogo appropriata **Servizio** dal menu a discesa

   ![Finestra di dialogo Download Logs (Registri di download)](assets/download-preview.png)

1. Dopo aver selezionato il servizio, fai clic sull&#39;icona di download accanto al registro che desideri recuperare.

Puoi anche accedere ai tuoi registri da **Ambienti** pagina.

![Registri dalla schermata Ambienti](assets/download-logs.png)

## Registri tramite API {#logs-through-api}

Oltre a scaricare i registri tramite l’interfaccia utente, i registri sono disponibili tramite l’API e l’interfaccia della riga di comando.

Per scaricare i file di registro per un ambiente specifico, il comando sarà simile al seguente.

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

È inoltre possibile visualizzare i registri tramite l’interfaccia della riga di comando.

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Per ottenere l&#39;ID ambiente (1884 in questo esempio) e le opzioni del servizio o del nome di registro disponibili, puoi utilizzare i seguenti comandi.

```shell
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

### Risorse aggiuntive {#resources}

Per ulteriori informazioni sull’API di Cloud Manager e su Adobe I/O CLI, consulta le seguenti risorse aggiuntive:

* [Documentazione API di Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
