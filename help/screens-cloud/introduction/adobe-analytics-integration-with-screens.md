---
title: Integrazione di Adobe Analytics con AEM Screens Cloud
description: Segui questa pagina per scoprire l’integrazione predefinita di AEM Screens con Adobe Analytics e ti fornisce una prova di riproduzione.
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
docset: aem65
role: Admin, Developer
level: Intermediate
exl-id: e22242ce-e5ce-4486-bba4-e6a89ac4fb5e
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Integrazione di Adobe Analytics con AEM Screens Cloud {#adobe-analytics-integration-with-aem-screens}

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

Un cliente AEM Screens vuole capire quale contenuto è stato mostrato in che momento e per quanto tempo (aggregato). Si tratta di una funzionalità comune della soluzione di signage. Invece di creare le nostre analisi, AEM Screens utilizza Adobe Analytics e con questo puoi ottenere qualcosa di unico nel mercato: l’analisi cross-channel che consente di correlare i contenuti mostrati nella posizione con altre origini dati.

Il diagramma architetturale seguente spiega l’integrazione di Adobe Analytics con AEM Screens:

![Integrazione con Adobe Analytics](/help/screens-cloud/assets/analytics-architecture.png)

## Abilitazione di Adobe Analytics in AEM Screens Cloud {#enabling-adobe-analytics-in-aem-screens-cloud}

Contatta il tuo Adobe Relationship Manager per abilitare Adobe Analytics in Screens Cloud.

## Utilizzo del servizio Adobe Analytics in AEM Screens Cloud {#using-adobe-analytics-service-in-aem-screens}

Questo scenario richiama l’API di Analytics tramite chiamate REST da un servizio di analisi nei componenti core delle schermate firmware e strumento per creare e inviare in modo esplicito eventi specifici per un particolare caso d’uso, consentendo al contempo l’estensibilità in cui qualsiasi messaggio personalizzato può essere inviato ad Analytics da un canale sviluppato personalizzato.

Gli eventi di Analytics vengono archiviati offline in indexedDB e successivamente bloccati e inviati al cloud.

>[!NOTE]
>Per ulteriori informazioni sul sequenziamento e sul modello dati standard per gli eventi, consulta [Configurazione di Adobe Analytics per AEM Screens](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/administering/analytics-integration/configuring-adobe-analytics-aem-screens.html) per i dettagli.
