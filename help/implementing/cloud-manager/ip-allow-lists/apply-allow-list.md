---
title: Applicazione e rimozione degli elenchi IP consentiti
description: Scopri come applicare e rimuovere gli elenchi IP consentiti dagli ambienti.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
source-git-commit: d1b2226a1deec2e71056c43c84672cb4a358bc8c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 81%

---


# Applicazione e rimozione degli elenchi IP consentiti {#apply-allow-list}

Quando si applica un elenco IP consentiti, tutti gli intervalli IP inclusi nella definizione dell’elenco vengono associati a un servizio d authoring o pubblicazione all’interno di un ambiente. La rimozione di un elenco costituisce il processo inverso.

## Applicazione degli elenchi IP consentiti {#applying}

L’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può applicare un elenco IP consentiti seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** , selezionare il programma.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina dei dettagli dell’ambiente specifico, quindi accedi alla tabella **Elenco IP consentiti**.
1. Utilizza i campi di input nella parte superiore della tabella per selezionare l’elenco consentiti IP e il servizio Author o Publish a cui desideri applicarlo.
   * Per poter applicare l’elenco IP consentiti, l’elenco deve esistere in Cloud Manager.
1. Fai clic su **Applica** e conferma quanto inserito.

## Rimozione degli elenchi Consentiti {#un-applying}

L’utente con il ruolo **Proprietario business** o **Responsabile della distribuzione** può rimuovere un elenco IP consentiti seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Dalla schermata **Ambienti**, accedi alla pagina dei dettagli dell’ambiente specifico, quindi accedi alla tabella **Elenco IP consentiti**.
1. Identifica la riga dell’elenco consentiti IP che desideri rimuovere.
1. Seleziona il pulsante con i puntini di sospensione all’estrema destra della riga.
1. Seleziona l’opzione **Rimuovi** e conferma quanto inserito.
