---
title: Modernizzatore dell'archivio
description: Modernizzatore dell'archivio
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 4%

---

# Modernizzatore dell&#39;archivio {#repo-modernizer}

Repository Modernizer è un&#39;utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo che sia compatibile con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service introduce molte nuove funzionalità e opportunità nei progetti di AEM. Tuttavia, sono necessarie alcune modifiche per rendere i progetti Adobe Experience Manager Maven compatibili con AEM Cloud Service. Ad un livello elevato, AEM richiede una separazione **content** e **codice** in pacchetti secondari distinti per rispettare la suddivisione tra contenuto mutabile e immutabile. Fai riferimento a [AEM struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) per ulteriori dettagli sulla nuova struttura di progetto AEM per Cloud Service.

Il Repository Modernizer crea una struttura di progetto AEM Cloud Service compatibile creando la seguente struttura di distribuzione:

* `ui.apps` implementazioni dei pacchetti in `/apps` e contiene tutto il codice

* `ui.content` implementazioni di pacchetti in aree scrivibili in fase di esecuzione (ad esempio `/content`, `/conf`, `/home`o altro `/apps`) e contiene tutti i contenuti e la configurazione.

* `all` pacchetto contenitore che contiene i pacchetti secondari `ui.apps` e `ui.content`.

>[!NOTE]
>La struttura del progetto si basa su *Archetipo 24* per i colli e i loro `pom.xml/filter.xml files`. Fai riferimento a [Archetipo 24](https://github.com/adobe/aem-project-archetype) per ulteriori dettagli.

## Utilizzo di Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Tramite Adobe I/O CLI : Si consiglia di utilizzare Repository Modernizer tramite `aio-cli-plugin-aem-cloud-service-migration` (AEM plug-in di refactoring del codice as a Cloud Service per l’interfaccia CLI di Adobe I/O).

   Fai riferimento a **[Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** per scoprire come installare e utilizzare il plug-in.

* Come utility indipendente : Il Repository Modernizer può essere eseguito anche come utility indipendente.

   Fai riferimento a **[Risorsa Git: Modernizzatore dell&#39;archivio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** per scoprire come utilizzare questo strumento.

   >[!NOTE]
   >
   >Il Repository Modernizer viene sviluppato utilizzando NodeJS. Si consiglia di installare NodeJS 10.0+.
