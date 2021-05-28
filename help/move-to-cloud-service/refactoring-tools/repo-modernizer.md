---
title: Modernizzatore dell'archivio
description: Modernizzatore dell'archivio
exl-id: b89156a8-3d7d-4d36-89a2-beeda35bbc01
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Modernizzatore archivio {#repo-modernizer}

Repository Modernizer è un&#39;utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo che sia compatibile con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service introduce molte nuove funzioni e possibilità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche per rendere i progetti Adobe Experience Manager Maven compatibili con il Cloud Service AEM. Ad alto livello, AEM una separazione di **content** e **code** in pacchetti secondari distinti per rispettare la suddivisione tra contenuto mutabile e immutabile. Per ulteriori informazioni sulla nuova struttura del progetto AEM per il Cloud Service, consulta [AEM Struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) .

Il Repository Modernizer crea una struttura di progetto di Cloud Service AEM compatibile creando la seguente struttura di distribuzione:

* `ui.apps` distribuisce i pacchetti in  `/apps` e contiene tutto il codice

* `ui.content` implementazioni di pacchetti in aree scrivibili in fase di esecuzione (ad esempio  `/content`,  `/conf`,  `/home`, o qualsiasi altra cosa  `/apps`) e contiene tutti i contenuti e la configurazione.

* `all` pacchetto contenitore che contiene i pacchetti secondari  `ui.apps` e  `ui.content`.

>[!NOTE]
>La struttura del progetto si basa su *Archetype 24* per i pacchetti e i relativi `pom.xml/filter.xml files`. Per ulteriori informazioni, consulta [Archetype 24](https://github.com/adobe/aem-project-archetype) .

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Tramite Adobe I/O CLI : Si consiglia di utilizzare Repository Modernizer tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM come plug-in di refactoring del codice di Cloud Service per l’interfaccia CLI di Adobe I/O).

   Fai riferimento a **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e utilizzare il plug-in.

* Come utility indipendente : Il Repository Modernizer può essere eseguito anche come utility indipendente.

   Fai riferimento a **[Risorsa Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** per scoprire come utilizzare questo strumento.

   >[!NOTE]
   >
   >Il Repository Modernizer viene sviluppato utilizzando NodeJS. Si consiglia di installare NodeJS 10.0+.
