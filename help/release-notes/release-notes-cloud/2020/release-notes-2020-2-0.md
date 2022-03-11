---
title: Note sulla versione 2020.2.0
description: Note sulla versione 2020.2.0
exl-id: 005c4756-44c6-4af5-9b0c-0fc07bd211a0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 100%

---

# AEM as a Cloud Service: note sulla versione di 2020.2.0 {#release-notes}

Questa pagina illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.2.0.

## Data di pubblicazione {#release-date}

La data di rilascio per Experience Manager as a Cloud Service 2020.2.0 è il giovedì 13 febbraio 2020.

## Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.2.0.

### Novità {#what-is-new}

* La versione dell’archetipo di Adobe Experience Manager è stata aggiornata alla versione 22.
* Gli ambienti di stage e produzione nei programmi Sandbox/Demo ora possono essere aggiornati tramite l’interfaccia utente di Cloud Manager.
* Gli URL utilizzati nelle notifiche di Experience Cloud sono stati ottimizzati per evitare un reindirizzamento aggiuntivo.
* I passaggi di esecuzione della pipeline interrotti a causa di timeout ora vengono segnalati in modo esplicito.
* Il passaggio di analisi del codice ora include un registro scaricabile.
* Il foglio di calcolo che contiene i problemi rilevati durante la scansione del codice ora include una colonna con un collegamento alla documentazione per la regola specifica.

### Correzioni di bug  {#bug-fixes}

* Talvolta, i criteri di sicurezza del browser impedivano il corretto funzionamento di alcuni pulsanti nella schermata di esecuzione della pipeline.
* I collegamenti Panoramica, Ambienti e Attività talvolta erano disponibili nella pagina di destinazione di Cloud Manager.
* Alcuni errori durante l’implementazione potevano impedire erroneamente la creazione di nuove pipeline.
