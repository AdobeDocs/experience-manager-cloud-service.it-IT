---
title: Accesso agli archivi
description: Scopri come accedere e gestire l’archivio Git con la gestione self-service dell’account Git da Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 85%

---


# Accesso agli archivi {#accessing-repos}

Scopri come accedere e gestire l’archivio Git con la gestione self-service dell’account Git da Cloud Manager.

## Utilizzo della gestione self-service dell’account dell’archivio {#self-service-repos}

Cloud Manager consente di recuperare facilmente le informazioni sull’archivio tramite il pulsante **Accedi a dati archivio** disponibile nella scheda Pipeline.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e individua il pulsante **Accedi a dati archivio** per accedere e gestire il tuo archivio Git.

   ![Pulsante Accedi a dati archivio nella scheda Ambienti](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Fai clic sul pulsante **Visualizza informazioni archivio** per aprire una finestra di dialogo e visualizzare:

   * L’URL dell’archivio Git di Cloud Manager.
   * Il nome utente di Git.
   * La password di Git, il cui valore viene visualizzato quando fai clic sul pulsante **Genera password**.

   ![Visualizzazione informazioni sull’archivio](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Con queste credenziali l’utente può clonare una copia locale dell’archivio, apportare qui le modifiche e, una volta terminato, riconfermarle nell’archivio del codice remoto in Cloud Manager.

L’opzione **Accedi a dati archivio** è disponibile anche nella scheda delle pipeline **non di produzione** della scheda **Pipeline**.

![Pulsante Accedi a dati archivio nella scheda non di produzione](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>L’opzione **Accedi a dati archivio** è visibile agli utenti con i ruoli **Sviluppatore** o **Responsabile dell’implementazione**.

## Revoca di una password di accesso {#revoke-password}

Puoi revocare una password di accesso in qualsiasi momento. Per farlo, [crea un ticket di supporto per questa richiesta.](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

Il biglietto sarà trattato con priorità alta e dovrebbe essere revocato entro un giorno.
