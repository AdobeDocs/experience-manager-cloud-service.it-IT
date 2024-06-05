---
title: Metodi per creare contenuti in AEM
description: Scopri i diversi modi in cui puoi creare contenuti in AEM e le loro differenze.
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Metodi per creare contenuti in AEM {#authoring-methods}

Scopri i diversi modi in cui puoi creare contenuti in AEM, come differiscono e quando potresti utilizzarne uno rispetto all’altro.

## Flessibilità nell&#39;authoring AEM {#authoring-flexibility}

AEM as a Cloud Service offre diversi editor per modificare diversi tipi di contenuti e supportare diversi casi di utilizzo di authoring.

* [Authoring basato su AEM tramite l’Editor pagina](#page-editor) - L’Editor pagina è l’editor classico per la creazione di contenuti in AEM, testato e affidabile per migliaia di siti web.
* [Authoring basato su AEM con Universal Editor](#universal-editor) - L’Editor universale è una moderna interfaccia utente che consente di creare contenuti AEM in modo indipendente dai contenuti ed è disponibile per progetti AEM che sfruttano i Edge Delivery Services.
* [Authoring basato su documenti](#document-based) - Se utilizzi i servizi di consegna Edge, puoi scegliere di creare i contenuti come documenti convenzionali, come Microsoft Word o Google Docs, interamente al di fuori delle console AEM.
* [Editor frammento di contenuto AEM](#cf-editor) : editor preferito per la creazione di contenuti headless.

A causa della natura integrata e scalabile dell’AEM, questi metodi possono essere utilizzati esclusivamente o in combinazione tra loro a seconda delle esigenze del progetto.

Se non sai quali opzioni di authoring sono disponibili o se desideri esplorarne di nuove, rivolgiti all’amministratore di sistema o al project manager.

## Authoring basato su AEM tramite l’Editor pagina {#page-editor}

Questo è l&#39;editor classico per la creazione di contenuti in AEM, provato e affidabile per migliaia e migliaia di siti web.

![Editor pagina AEM](assets/authoring-methods-page-editor.png)

L’editor di pagine dell’AEM presenta un ambiente integrato per la creazione dei contenuti mediante l’interfaccia WYSIWYG (What-you-see-is-what-you-get). Trascina i componenti predefiniti per creare la pagina e modificarne i contenuti direttamente.

Per ulteriori informazioni sull’editor di pagine dell’AEM, consulta il documento [Editor pagina AEM.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Authoring basato su AEM con Universal Editor {#universal-editor}

L’editor universale è una moderna interfaccia utente che consente di creare contenuti AEM in modo indipendente dai contenuti ed è la prima scelta per i progetti AEM che sfruttano i Edge Delivery Services.

![L’editor universale](assets/authoring-methods-ue.png)

L’editor universale è accessibile tramite la console Sites all’interno di AEM, ma offre la potenza e la flessibilità indipendente dai contenuti per l’authoring non solo dei contenuti AEM, ma anche dei contenuti esterni dotati di strumenti adeguati.

Per ulteriori informazioni sull’editor universale, consulta il documento [Authoring di contenuti con l’Editor universale.](/help/sites-cloud/authoring/universal-editor/authoring.md)

## Authoring basato su documenti  {#document-based}

Se utilizzi i servizi di consegna Edge, puoi scegliere di creare i contenuti come documenti tradizionali come Microsoft Word o Google Docs completamente al di fuori del [AEM **Sites** console.](/help/sites-cloud/authoring/sites-console/introduction.md)

![Modifica di contenuti basati su documenti](assets/authoring-methods-document.jpg)

Con l’authoring basato su documenti, gli autori possono utilizzare gli strumenti già noti e beneficiare ancora della velocità e delle prestazioni dei Edge Delivery Services AEM per pubblicare i propri contenuti. L’authoring basato su documenti non richiede l’utilizzo della console AEM.

Per ulteriori informazioni sull’authoring basato su documenti, consulta il documento [Authoring e pubblicazione dei contenuti.](/help/edge/docs/authoring.md)

## Editor frammento di contenuto AEM {#cf-editor}

L’editor dei frammenti di contenuto dell’AEM è l’editor preferito per la creazione di contenuti headless.

![Editor frammento di contenuto AEM](assets/authoring-methods-cf-editor.png)

L’editor dei frammenti di contenuto dell’AEM presenta una chiara interfaccia per la creazione e la gestione di contenuti strutturati, ideali per la distribuzione headless.

Per ulteriori informazioni sull’editor dei frammenti di contenuto dell’AEM, consulta la documentazione [Gestione dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md) e [Creazione di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>Il *nuovo* L’editor evidenziato in questa sezione non è disponibile quando si sviluppa localmente per AEM as a Cloud Service.
>
>Il [*originale* Editor frammento di contenuto](/help/assets/content-fragments/content-fragments-variations.md) è disponibile anche.
