---
title: Modernizzatore dell'archivio
description: Scopri come ristrutturare i pacchetti di progetto esistenti e renderli compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 5%

---

# Modernizzatore dell&#39;archivio {#repo-modernizer}

Repository Modernizer è un’utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti distinti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service introduce molte nuove funzioni e opportunità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. Ad alto livello, l&#39;AEM richiede una separazione tra **contenuto** e **codice** in pacchetti secondari discreti per rispettare la suddivisione tra contenuto mutabile e immutabile. Consulta [Struttura dei progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=it) per maggiori dettagli sulla nuova struttura di progetto AEM per il Cloud Service.

Repository Modernizer crea una struttura di progetto AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

* `ui.apps` il pacchetto viene distribuito in `/apps` e contiene tutto il codice

* `ui.content` distribuisce il pacchetto in aree scrivibili di runtime (ad esempio, `/content`, `/conf`, `/home`, o tutto ciò che non `/apps`) e contiene tutto il contenuto e la configurazione.

* `all` pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

>[!NOTE]
>La struttura del progetto si basa su *Archetipo 24* per i colli e il loro `pom.xml/filter.xml files`. Consulta [Archetipo 24](https://github.com/adobe/aem-project-archetype) per ulteriori dettagli.

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Ad Adobe I/O, CLI : si consiglia di utilizzare il Modernizzatore dell’archivio tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in per il refactoring del codice as a Cloud Service AEM per Adobe I/O CLI).

  Consulta **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** in questo modo puoi imparare a installare e utilizzare il plug-in.

* Come utility autonoma: Repository Modernizer può anche essere eseguito come utility autonoma.

  Consulta **[Risorsa Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** così potete imparare a usare questo strumento.

  >[!NOTE]
  >
  >Il Modernizzatore dell’archivio viene sviluppato utilizzando NodeJS. Si consiglia di installare NodeJS 10.0+.
