---
title: Applicare e rimuovere Elenchi consentiti IP
description: Scopri come applicare e rimuovere gli Elenchi consentiti IP dagli ambienti Cloud Manager.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 18%

---


# Applicare e annullare l’applicazione degli Elenchi consentiti IP {#apply-allow-list}

Quando si applicano Elenchi consentiti IP, tutti gli intervalli IP inclusi nella definizione dell’elenco vengono associati a un servizio Author o Publish all’interno di un ambiente. La rimozione di un elenco costituisce il processo inverso.

{{add-cm-allowlist-frontend-pipeline}}

## Applicare Elenchi consentiti IP {#applying}

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può applicare un Elenco consentiti IP seguendo la procedura riportata di seguito.

**Per applicare Elenchi consentiti IP:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Seleziona l’organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Dalla pagina **Panoramica**, passa alla schermata **Ambienti**.
1. Nella schermata **Ambienti**, passa alla pagina dei dettagli dell&#39;ambiente specifico.
1. Passare alla tabella **Elenco consentiti IP**.
1. Utilizza i campi di input nella parte superiore della tabella per selezionare l’Elenco consentiti IP e il servizio Author o Publish a cui applicarlo.
L’Elenco consentiti IP deve esistere già in Cloud Manager per applicarlo. Vedi [Aggiungi Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).
1. Fai clic su **Applica** e conferma quanto inserito.

## Annulla applicazione Elenchi consentiti IP {#un-applying}

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può rimuovere un Elenco consentiti IP seguendo la procedura riportata di seguito.

**Per annullare l&#39;applicazione degli Elenchi consentiti IP:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Seleziona l’organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.
1. Nella schermata **Ambienti**, accedi alla pagina dei dettagli dell&#39;ambiente specifico.1. Passare alla tabella **Elenco consentiti IP**.
1. Identifica la riga dell’Elenco consentiti IP da rimuovere.
1. Sul lato destro della riga identificata, fai clic sul pulsante con i puntini di sospensione, quindi seleziona **Annulla applicazione**.
1. Conferma quanto inserito.
