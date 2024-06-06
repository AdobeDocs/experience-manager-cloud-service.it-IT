---
title: Informazioni di accesso all’archivio
description: Scopri come accedere e gestire gli archivi Git gestiti da Adobe utilizzando la gestione self-service dell’account Git di Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0b39fc4dcaf86d436547d3941b1f12bca8c5bc9b
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 11%

---


# Informazioni di accesso all’archivio {#accessing-repos}

Scopri come accedere e gestire gli archivi Git gestiti da Adobe utilizzando la gestione self-service dell’account Git di Cloud Manager.

## Accesso alle informazioni dell’archivio dalla pagina Panoramica {#overview-page}

Cloud Manager consente di recuperare facilmente le informazioni di accesso all’archivio per gli archivi gestiti da Adobe utilizzando **Accedi a dati archivio** disponibile nella scheda pipeline.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi a **Pipeline** scheda dal tuo **Panoramica del programma** pagina.

   ![Pulsante Accedi a dati archivio nella scheda Ambienti](assets/pipelines-card.png)

1. Tocca o fai clic su **Accedi a dati archivio** per aprire **Informazioni archivio** finestra di dialogo e visualizzazione:

   * Il nome utente di Git.
   * La password Git.
   * L’URL dell’archivio Git di Cloud Manager.
   * Comandi Git predefiniti per aggiungere rapidamente un remoto all’archivio Git e inviare il codice.

   ![Finestra Informazioni archivio](assets/repository-info.png)

1. Per accedere alla password, è necessario generare una nuova password. Per farlo, tocca o fai clic su **Genera password** pulsante.

1. Conferma generazione password in **Continuare?** toccando o facendo clic su **Genera password**.

   ![Conferma generazione password](assets/confirm-password-generation.png)

1. La password viene generata ed è visibile per la copia in **Password** campo.

   * La generazione di una password invalida la password precedente.
   * Cloud Manager non salverà la password. È tua responsabilità salvare la password in modo sicuro.
   * Poiché Cloud Manager non salva la password, se la perdi è necessario rigenerarne una nuova.

   ![Esempio di password generata](assets/generated-password.png)

Utilizzando queste credenziali, puoi clonare una copia locale dell’archivio, apportare modifiche all’archivio locale e, una volta pronto, eseguire il commit di eventuali modifiche al codice nell’archivio del codice remoto in Cloud Manager.

>[!NOTE]
>
>* L’opzione **Accedi a dati archivio** è visibile agli utenti con i ruoli **Sviluppatore** o **Responsabile dell’implementazione**.
>* Il **Accedi a dati archivio** Questo pulsante visualizza solo le informazioni di accesso al repository per i repository gestiti da Adobe. Accedere alle informazioni su [archivi privati](private-repositories.md) non è disponibile in Cloud Manager.

## Accesso alle informazioni dell&#39;archivio dalla finestra Archivi {#repositories-window}

Un **Accedi a dati archivio** è disponibile anche nella barra degli strumenti del [**Archivi** finestra.](managing-repositories.md) vengono visualizzate le stesse informazioni sull’accesso agli archivi gestiti da Adobe.

## Revoca di una password di accesso {#revoke-password}

Puoi revocare una password di accesso in qualsiasi momento. Per farlo, [crea un ticket di supporto per questa richiesta.](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

Il biglietto sarà trattato con priorità alta e dovrebbe essere revocato entro un giorno.
