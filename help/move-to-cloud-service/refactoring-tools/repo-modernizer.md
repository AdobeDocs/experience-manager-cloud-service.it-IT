---
title: Repository Modernizer
description: Repository Modernizer
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 4%

---


# Repository Modernizer {#repo-modernizer}

Repository Modernizer è un&#39;utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo da essere compatibile con la struttura di progetto definita come Cloud Service per Adobe Experience Manager.

## Introduzione {#introduction}

Adobe Experience Manager come Cloud Service offre molte nuove funzionalità e opportunità nei vostri progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per essere compatibili con AEM Cloud Service. A un livello elevato, AEM richiede una separazione di **contenuto** e **codice** in sottopacchetti discreti per rispettare la divisione tra contenuto mutabile e immutabile. Per ulteriori dettagli sulla nuova struttura del progetto AEM per Cloud Service, fare riferimento a [AEM Struttura](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) progetto.

Repository Modernizer crea una struttura di progetto AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

* `ui.apps` distribuisce il pacchetto a `/apps` e contiene tutto il codice

* `ui.content` distribuisce pacchetti alle aree scrivibili in fase di esecuzione (ad es. `/content`, `/conf`, `/home`o altro `/apps`) e contiene tutto il contenuto e la configurazione.

* `all` pacchetto è un pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

>[!NOTE]
>La struttura del progetto è basata su *Archetype 24* per i pacchetti e i relativi `pom.xml/filter.xml files`. Per ulteriori informazioni, fare riferimento a [Archetype 24](https://github.com/adobe/aem-project-archetype) .

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

* Tramite  Adobe I/O CLI: Si consiglia di utilizzare Repository Modernizer tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM come plug-in di refactoring del codice di Cloud Service per l&#39;interfaccia CLI di  Adobe I/O).

   Fare riferimento a Risorse **[Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per imparare come installare e usare il plug-in.

* Come utilità indipendente : Repository Modernizer può essere eseguito anche come utilità indipendente.

   Fare riferimento a Risorse **[Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** per imparare a utilizzare questo strumento.

   >[!NOTE]
   >
   >Repository Modernizer è sviluppato utilizzando NodeJS. È consigliabile installare NodeJS 10.0+.
