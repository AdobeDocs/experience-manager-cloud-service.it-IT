---
title: Informazioni di accesso all’archivio
description: Scopri come accedere e gestire gli archivi Git gestiti da Adobe utilizzando la gestione account Git self-service da Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f2364de6237ca9f0285815b581bcf3881488188d
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 44%

---


# Informazioni di accesso all’archivio {#accessing-repos}

Scopri come accedere e gestire gli archivi Git gestiti da Adobe utilizzando la gestione account Git self-service da Cloud Manager.

## Accedere alle informazioni del repository dalla pagina Panoramica {#overview-page}

Cloud Manager semplifica il recupero delle informazioni di accesso all&#39;archivio per gli archivi gestiti da Adobe utilizzando **Accedi a dati archivio** dalla scheda **Pipeline**.

La finestra di dialogo **Informazioni archivio** consente di visualizzare le seguenti informazioni di accesso per gli archivi gestiti da Adobe:

* Il nome utente di Git.
* La password di Git.
* L’URL dell’archivio Git di Cloud Manager.
* Comandi Git predefiniti per aggiungere rapidamente un remoto all’archivio Git e inviare il codice.

![Finestra dati archivio](assets/repository-info.png)

L’accesso alle informazioni degli [archivi privati](private-repositories.md) non è disponibile in Cloud Manager.

La funzionalità **Accedi a dati archivio** è visibile agli utenti con i ruoli **Sviluppatore** o **Responsabile della distribuzione**.

**Per accedere alle informazioni del repository dalla pagina Panoramica:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, nella scheda **Pipeline**, fai clic su **Accedi a dati archivio**.

   ![Accedi a dati archivio sulla scheda delle pipeline](assets/pipelines-card.png)

1. Per accedere alla password, è necessario generare una nuova password. Nella finestra di dialogo **Informazioni archivio**, selezionare **Genera password**.

1. Nella finestra di dialogo di conferma, selezionare **Genera password**.

   ![Conferma la generazione della password](assets/confirm-generated-password.png)

1. A destra del campo **Password**, fai clic su ![Copia icona](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare la password negli Appunti.

   * La generazione di una password invalida la password precedente.
   * Cloud Manager non salva la password. È tua responsabilità salvare la password in modo sicuro.
   * Poiché Cloud Manager non salva la password, se questa viene persa è necessario rigenerarne una nuova.

   ![Copia password nella finestra di dialogo Informazioni archivio](/help/implementing/cloud-manager/managing-code/assets/repository-copy-password.png)

Con queste credenziali puoi clonare una copia locale dell’archivio, apportare qui le modifiche e, una volta terminato, riconfermarle nell’archivio del codice remoto in Cloud Manager.

## Accedere alle informazioni dell’archivio dalla pagina Archivi {#repositories-window}

La funzionalità **Accedi a dati archivio** è disponibile anche nella pagina [**Archivi**](managing-repositories.md). Visualizza le stesse informazioni sull’accesso agli archivi gestiti da Adobe.

## Revoca di una password di accesso {#revoke-password}

Puoi revocare una password di accesso in qualsiasi momento.

Per farlo, [crea un ticket di supporto per questa richiesta](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&support-tab=home?lang=it#support). Il biglietto viene trattato con priorità alta e di solito viene revocato entro un giorno.
