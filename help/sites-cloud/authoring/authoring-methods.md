---
title: Metodi per creare contenuti in AEM
description: Scopri i diversi modi in cui puoi creare contenuti in AEM e le loro differenze.
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Metodi per creare contenuti in AEM {#authoring-methods}

Scopri i diversi modi in cui puoi creare contenuti in AEM, come differiscono e quando potresti utilizzarne uno rispetto all’altro.

## Flessibilità nell&#39;authoring AEM {#authoring-flexibility}

AEM as a Cloud Service offre diversi editor per modificare diversi tipi di contenuto e supportare diversi casi di utilizzo di authoring.

* [Authoring WYSIWYG tramite Editor pagina](#page-editor) - L&#39;Editor pagina è l&#39;editor classico per la creazione di contenuti in AEM, provato e affidabile per migliaia di siti Web.
* [Authoring WYSIWYG con Universal Editor](#universal-editor) - L&#39;Universal Editor è un&#39;interfaccia utente moderna che consente di creare contenuti AEM in modo indipendente dai contenuti ed è disponibile per progetti AEM che sfruttano i Edge Delivery Services.
* [Authoring basato su documenti](#document-based) - Se utilizzi i servizi di Edge Delivery, puoi scegliere di creare i contenuti come documenti convenzionali, come Microsoft Word o Google Docs, completamente al di fuori delle console AEM.
* [Editor frammento di contenuto AEM](#cf-editor) - Questo è l&#39;editor preferito per la creazione di contenuti headless.

A causa della natura integrata e scalabile dell’AEM, questi metodi possono essere utilizzati esclusivamente o in combinazione tra loro a seconda delle esigenze del progetto.

Se non sai quali opzioni di authoring sono disponibili o se desideri esplorarne di nuove, rivolgiti all’amministratore di sistema o al project manager.

## Authoring WYSIWYG tramite l’Editor pagina {#page-editor}

Questo è l&#39;editor classico per la creazione di contenuti in AEM, provato e affidabile per migliaia e migliaia di siti web.

![Editor pagina AEM](assets/authoring-methods-page-editor.png)

L’editor di pagine dell’AEM presenta un ambiente integrato per la creazione dei contenuti mediante l’interfaccia WYSIWYG (What-you-see-is-what-you-get). Trascina i componenti predefiniti per creare la pagina e modificarne i contenuti direttamente.

Per ulteriori informazioni sull&#39;editor pagina AEM, vedere il documento [Editor pagina AEM.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Authoring WYSIWYG con l’editor universale {#universal-editor}

L’editor universale è una moderna interfaccia utente che consente di creare contenuti AEM in modo indipendente dai contenuti ed è la prima scelta per i progetti AEM che sfruttano i Edge Delivery Services.

![L’editor universale](assets/authoring-methods-ue.png)

L’editor universale è accessibile tramite la console Sites all’interno di AEM, ma offre la potenza e la flessibilità indipendente dai contenuti per l’authoring non solo dei contenuti AEM, ma anche dei contenuti esterni dotati di strumenti adeguati.

Per ulteriori informazioni sull&#39;editor universale, vedere il documento [Creazione di contenuti con l&#39;editor universale.](/help/sites-cloud/authoring/universal-editor/authoring.md)

## Authoring basato su documenti  {#document-based}

Se si utilizzano i servizi di Edge Delivery, è possibile scegliere di creare i contenuti come documenti convenzionali, ad esempio Microsoft Word o Google Docs, completamente al di fuori della console [AEM **Sites**.](/help/sites-cloud/authoring/sites-console/introduction.md)

![Modifica di contenuti basati su documenti](assets/authoring-methods-document.jpg)

Con l’authoring basato su documenti, gli autori possono utilizzare gli strumenti già noti e beneficiare ancora della velocità e delle prestazioni dei Edge Delivery Services AEM per pubblicare i propri contenuti. L’authoring basato su documenti non richiede l’utilizzo della console AEM.

Per ulteriori informazioni sull&#39;authoring basato su documenti, vedere il documento [Authoring e pubblicazione di contenuti.](/help/edge/docs/authoring.md)

## Editor frammento di contenuto AEM {#cf-editor}

L’editor dei frammenti di contenuto dell’AEM è l’editor preferito per la creazione di contenuti headless.

![Editor frammento di contenuto AEM](assets/authoring-methods-cf-editor.png)

L’editor dei frammenti di contenuto dell’AEM presenta una chiara interfaccia per la creazione e la gestione di contenuti strutturati, ideali per la distribuzione headless.

Per ulteriori informazioni sull&#39;editor dei frammenti di contenuto AEM, consulta i documenti [Gestione dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md) e [Authoring dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>L&#39;editor *new* evidenziato in questa sezione non è disponibile durante lo sviluppo locale per AEM as a Cloud Service.
>
>È inoltre disponibile l&#39;editor dei frammenti di contenuto [*original*](/help/assets/content-fragments/content-fragments-variations.md).
