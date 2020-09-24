---
title: Repository Modernizer
description: Repository Modernizer
translation-type: tm+mt
source-git-commit: fd70f5b6a17666d411a64a8fb3961555a42a5430
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 3%

---


# Repository Modernizer {#repo-modernizer}

Repository Modernizer è un&#39;utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo da essere compatibile con la struttura di progetto definita come Cloud Service per Adobe Experience Manager.

## Introduzione {#introduction}

Adobe Experience Manager come Cloud Service offre molte nuove funzionalità e opportunità nei vostri progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per essere compatibili con AEM Cloud Service. A un livello elevato, AEM richiede una separazione di **contenuto** e **codice** in sottopacchetti discreti per rispettare la divisione tra contenuto mutabile e immutabile. Per ulteriori dettagli sulla nuova struttura del progetto AEM per Cloud Service, fare riferimento a [AEM Struttura](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) progetto.

Repository Modernizer crea una struttura di progetto AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

* `ui.apps` distribuisce il pacchetto a `/apps` e contiene tutto il codice

* `ui.content` distribuisce pacchetti alle aree scrivibili in fase di esecuzione (ad es. `/content`, `/conf`, `/home`o altro `/apps`) e contiene tutto il contenuto e la configurazione.

* `all` pacchetto è un pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

* Tramite CLI I/O  Adobe: Si consiglia di utilizzare Repository Modernizer tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM come plug-in per il refactoring del codice di Cloud Service per l&#39;interfaccia CLI I/O di  Adobe).

   Fare riferimento a Risorse **[Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per imparare come installare e usare il plug-in.

* Come utilità indipendente : Repository Modernizer può essere eseguito anche come utilità indipendente.

   Fare riferimento a Risorse **[Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** per imparare a utilizzare questo strumento.
