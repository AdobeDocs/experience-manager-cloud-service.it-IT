---
title: Gestione registri - Servizio Cloud
description: Gestione registri - Servizio Cloud
translation-type: tm+mt
source-git-commit: 5913151c4e2bebb84bd68377d64f43e07caaf2dd

---


# Accesso e gestione dei registri {#manage-logs}

Gli utenti possono accedere a un elenco dei file di registro disponibili per l&#39;ambiente selezionato utilizzando la scheda Ambiente.  Gli utenti possono accedere a un elenco dei file di registro disponibili per l’ambiente selezionato.

Questi file possono essere scaricati tramite l’interfaccia utente, dalla pagina **Panoramica** .

![](assets/manage-logs1.png)

Oppure, la pagina **Ambienti** :

![](assets/manage-logs2.png)

>[!Note]
>Indipendentemente da dove viene aperto, viene visualizzata la stessa finestra di dialogo e è possibile scaricare un singolo file di registro.

![](assets/manage-logs3.png)


## Esegue il login tramite l&#39;API {#logs-thorugh-api}

Oltre a scaricare i file di registro tramite l’interfaccia utente, i file di registro saranno disponibili tramite l’API e l’interfaccia della riga di comando.

Ad esempio, per scaricare i file di registro per un ambiente specifico, il comando potrebbe essere solo delle righe di

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

Il seguente comando consente la coda dei registri:

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Per ottenere l&#39;ID ambiente (in questo caso 1884) e le opzioni del servizio o del nome di registro disponibili è possibile utilizzare:

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

>[!Note]
>Mentre i **Log Downloads** (Download dei registri) saranno disponibili sia dall’interfaccia utente che tramite l’API, **Log Tailing** (Coda del registro) è accessibile solo con API/CLI.

### Additional Resources {#resources}

Per ulteriori informazioni sull&#39;API di Cloud Manager e l&#39;interfaccia CLI di Adobe I/O, fare riferimento alle seguenti risorse aggiuntive:

* [Documentazione API di Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [CLI I/O di Adobe](https://github.com/adobe/aio-cli-plugin-cloudmanager)