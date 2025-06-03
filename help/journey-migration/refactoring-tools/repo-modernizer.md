---
title: Modernizzatore dell'archivio
description: Scopri come ristrutturare i pacchetti di progetto esistenti e renderli compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 6920651420da9b427510518b7add0637479adef5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# Modernizzatore dell&#39;archivio {#repo-modernizer}

Repository Modernizer è un’utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti distinti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service introduce molte nuove funzioni e opportunità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. A un livello avanzato, AEM richiede una separazione di **contenuto** e **codice** in pacchetti secondari discreti per rispettare la suddivisione tra contenuto mutabile e immutabile. Per ulteriori dettagli sulla nuova struttura di progetto AEM per Cloud Service, consulta [Struttura di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=it).

Repository Modernizer crea una struttura di progetto di AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

* Il pacchetto `ui.apps` viene distribuito in `/apps` e contiene tutto il codice

* Il pacchetto `ui.content` viene distribuito in aree scrivibili di runtime (ad esempio, `/content`, `/conf`, `/home` o qualsiasi elemento diverso da `/apps`) e contiene tutto il contenuto e la configurazione.

* Il pacchetto `all` è un pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

>[!NOTE]
>
>La struttura del progetto si basa su *Archetipo 24* per i pacchetti e i relativi `pom.xml/filter.xml files`. Per ulteriori dettagli, vedere [Archetipo 24](https://github.com/adobe/aem-project-archetype).

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Tramite Adobe I/O CLI: Adobe consiglia di utilizzare Repository Modernizer tramite `aio-cli-plugin-aem-cloud-service-migration` (plug-in di refactoring del codice AEM as a Cloud Service per Adobe I/O CLI).

  Consulta **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per informazioni su come installare e utilizzare il plug-in.

* Come utility autonoma: Repository Modernizer può anche essere eseguito come utility autonoma.

  Consulta **[Risorsa Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** per scoprire come utilizzare questo strumento.

  >[!NOTE]
  >
  >Il Modernizzatore dell’archivio viene sviluppato utilizzando NodeJS. Si consiglia di installare NodeJS 10.0+.
