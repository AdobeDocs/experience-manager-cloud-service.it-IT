---
title: Modernizzatore dell'archivio
description: Modernizzatore dell'archivio
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 6%

---

# Modernizzatore dell&#39;archivio {#repo-modernizer}

Repository Modernizer è un’utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti distinti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service introduce molte nuove funzioni e possibilità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. Ad alto livello, l&#39;AEM richiede una separazione tra **contenuto** e **codice** in pacchetti secondari discreti per rispettare la suddivisione tra contenuto mutabile e immutabile. Fare riferimento a [Struttura dei progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) per maggiori dettagli sulla nuova struttura di progetto AEM per il Cloud Service.

Repository Modernizer crea una struttura di progetto AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

* `ui.apps` il pacchetto viene distribuito in `/apps` e contiene tutto il codice

* `ui.content` distribuisce il pacchetto in aree scrivibili di runtime (ad esempio, `/content`, `/conf`, `/home`, o tutto ciò che non `/apps`) e contiene tutto il contenuto e la configurazione.

* `all` pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

>[!NOTE]
>La struttura del progetto si basa su *Archetipo 24* per i colli e il loro `pom.xml/filter.xml files`. Fai riferimento a [Archetipo 24](https://github.com/adobe/aem-project-archetype) per ulteriori dettagli.

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Tramite CLI di Adobe I/O : si consiglia di utilizzare Repository Modernizer tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in per il refactoring del codice as a Cloud Service AEM per Adobe I/O CLI).

   Fai riferimento a **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e utilizzare il plug-in.

* Come utility autonoma: Repository Modernizer può anche essere eseguito come utility autonoma.

   Fai riferimento a **[Risorsa Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** per scoprire come utilizzare questo strumento.

   >[!NOTE]
   >
   >Il Modernizzatore dell’archivio viene sviluppato utilizzando NodeJS. Si consiglia di installare NodeJS 10.0+.
