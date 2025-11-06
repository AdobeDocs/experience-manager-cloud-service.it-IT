---
title: Informazioni di accesso all’archivio
description: Scopri come accedere e gestire gli archivi Git gestiti da Adobe utilizzando la gestione account Git self-service da Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 96%

---


# Informazioni di accesso all’archivio {#accessing-repos}

Scopri come accedere e gestire gli archivi Git gestiti da Adobe utilizzando la gestione account Git self-service da Cloud Manager.

## Accedere alle informazioni del repository dalla pagina Panoramica {#overview-page}

Cloud Manager consente di recuperare facilmente le informazioni di accesso agli archivi gestiti da Adobe mediante **Accedi a dati archivio** dalla scheda **Pipeline**.

La finestra di dialogo **Informazioni archivio** consente di visualizzare le seguenti informazioni di accesso per gli archivi gestiti da Adobe:

* Il nome utente di Git.
* La password di Git.
* L’URL dell’archivio Git di Cloud Manager.
* Comandi Git predefiniti per aggiungere rapidamente un remoto all’archivio Git e inviare il codice.

![Finestra dati archivio](assets/repository-info.png)

L’accesso alle informazioni degli [archivi privati](private-repositories.md) non è disponibile in Cloud Manager.

La funzione **Accedi a dati archivio** è visibile agli utenti con i ruoli **Sviluppatore** o **Responsabile dell’implementazione**.

**Per accedere alle informazioni dell’archivio dalla pagina Panoramica:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, nella scheda **Pipeline**, fai clic su **Accedi a dati archivio**.

   ![Accedi a dati archivio nella scheda Pipeline](assets/pipelines-card.png)

1. Per accedere alla password, è necessario generare una nuova password. Nella finestra di dialogo **Informazioni archivio**, seleziona **Genera password**.

1. Nella finestra di dialogo di conferma, seleziona **Genera password**.

   ![Conferma la generazione della password](assets/confirm-generated-password.png)

1. A destra del campo **Password**, fai clic sull’![icona Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare la password negli appunti.

   * La generazione di una password invalida la password precedente.
   * Cloud Manager non salverà la password. È tua responsabilità salvare la password in modo sicuro.
   * Se la password viene persa, è necessario rigenerarne una nuova, poiché Cloud Manager non la salva.

   ![Copia password nella finestra di dialogo Informazioni archivio](/help/implementing/cloud-manager/managing-code/assets/repository-copy-password.png)

Con queste credenziali puoi clonare una copia locale dell’archivio, apportare qui le modifiche e, una volta terminato, riconfermarle nell’archivio del codice remoto in Cloud Manager.

## Accedere alle informazioni dell’archivio dalla pagina Archivi {#repositories-window}

La funzione **Accedi a dati archivio** è disponibile anche nella pagina [**Archivi**](managing-repositories.md). Visualizza le stesse informazioni sull’accesso agli archivi gestiti da Adobe.

## Revoca di una password di accesso {#revoke-password}

Puoi revocare una password di accesso in qualsiasi momento.

Per farlo, [crea un ticket di supporto per questa richiesta](https://experienceleague.adobe.com/?support-solution=Experience+Manager&support-tab=home?lang=it#support). Il ticket sarà trattato con priorità alta e solitamente revocato nell’arco di una giornata.
