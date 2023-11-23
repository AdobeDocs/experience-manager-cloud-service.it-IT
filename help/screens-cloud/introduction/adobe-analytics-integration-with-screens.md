---
title: Integrazione di Adobe Analytics con AEM Screens
seo-title: Adobe Analytics Integration with AEM Screens
description: Segui questa pagina per scoprire l’integrazione predefinita di AEM Screens con Adobe Analytics e ti fornisce una prova di riproduzione.
seo-description: Follow this page to learn about out of the box integration of AEM Screens with Adobe Analytics and provides you with a proof of play.
uuid: 80d61af7-bf4d-46ca-a026-99a666c2e1a0
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
discoiquuid: b1a0e00e-0368-42c9-8bcd-5f00b4d0990c
docset: aem65
role: Admin, Developer
level: Intermediate
source-git-commit: bf0a841a5cd5eb278fd3d59484c84d1cee172b4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Integrazione di Adobe Analytics con AEM Screens {#adobe-analytics-integration-with-aem-screens}

Questa sezione tratta i seguenti argomenti:

* **Panoramica**
* **Dettagli dell’architettura**

## Panoramica {#overview}

***AEM Screens*** sfrutta Adobe Analytics e con questo puoi ottenere qualcosa di unico nel mercato: analisi cross-channel che consentono di correlare i contenuti mostrati nella posizione con altre origini dati.

AEM Screens fornisce un’integrazione standard con Adobe Analytics e una bozza di riproduzione.

Questa sezione descrive le seguenti funzionalità relative alla connessione di un progetto AEM Screens con Adobe Analytics:

* Consente di creare report di prova di riproduzione per dispositivo
* Consente di creare report proof of play per risorsa
* Garantisce che tutti gli eventi del lettore vengano acquisiti e contrassegnati con marca temporale
* Garantisce che tutti gli eventi del lettore siano archiviati localmente se la riproduzione non è collegata a una rete
* Consente la creazione di cicli di feedback per tenere traccia degli eventi di riproduzione nel tempo
* Consente al sistema di modificare il contenuto e i layout in base ai criteri di successo definiti dall’autore del contenuto

L’integrazione di Adobe Analytics con AEM Screens applica quindi quanto segue *obiettivi*:

* Abilitare il ROI dalle implementazioni di digital signage
* Integrare Analytics come base per l’abilitazione futura della raccolta e dell’analisi delle informazioni sull’utilizzo

## Dettagli dell’architettura {#architectural-details}

Un cliente AEM Screens vuole capire quale contenuto è stato mostrato in che momento e per quanto tempo (aggregato). Si tratta di una funzionalità comune della soluzione di signage. Invece di creare le nostre analisi, AEM Screens sfrutterà Adobe Analytics e con questo possiamo ottenere qualcosa di unico nel mercato: l’analisi cross-channel che consente di correlare i contenuti mostrati sul posto con altre origini dati.

Il diagramma architetturale seguente spiega l’integrazione di Adobe Analytics con AEM Screens:

![Integrazione con Adobe Analytics](/help/screens-cloud/assets/analytics-architecture.png)

## Abilitazione di Adobe Analytics nel cloud AEM Screens {#enabling-adobe-analytics-in-aem-screens-cloud}

Contatta il tuo Adobe Relationship Manager per abilitare Adobe Analytics in Screens Cloud.

## Screens Analytics: Flusso di abilitazione {#screens-analytics-enablement-flow}

>[!CAUTION]
>
>Prima di configurare le proprietà, contatta l’Adobe Relationship Manager per creare un ticket per ottenere un **Chiave API di Analytics** e **Progetto Analytics** da utilizzare con AEM Screens.

## Utilizzo del servizio Adobe Analytics in AEM Screens {#using-adobe-analytics-service-in-aem-screens}

Questo scenario richiama l’API di Analytics tramite chiamate REST da un servizio di analisi nei componenti core delle schermate firmware e strumento per creare e inviare in modo esplicito eventi specifici per un particolare caso d’uso, consentendo al contempo l’estensibilità in cui qualsiasi messaggio personalizzato può essere inviato ad Analytics da un canale sviluppato personalizzato.

Gli eventi di Analytics vengono archiviati offline in indexedDB e successivamente bloccati e inviati al cloud.
