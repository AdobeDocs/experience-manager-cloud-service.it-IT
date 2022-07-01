---
title: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
description: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: d763bacb0844a438ebea6ef206dfa184a49993fe
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---

# Note sulla versione [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

La sezione seguente illustra le note generali sulla versione di [!DNL Workfront for Experience Manager enhanced connector].

## Data di pubblicazione {#release-date}

Data di rilascio dell’ultima versione 1.9.1 di [!DNL Workfront for Experience Manager enhanced connector] è l’1 luglio 2022.

## Funzioni principali {#release-highlights}

La versione più recente del [!DNL Workfront for Experience Manager enhanced connector] include i seguenti miglioramenti e correzioni di bug:

* È stato aggiunto il supporto per l’autenticazione tra le applicazioni Experience Manager e Workfront tramite la chiave API Workfront per le istanze migrate ad Adobe IMS.

* Quando si collegano file o cartelle esterni, l&#39;applicazione Workfront visualizza la `SERVER_ERROR` messaggio di errore. Il messaggio di errore fa riferimento a un&#39;eccezione non autorizzata a causa di una mancata corrispondenza nelle chiavi API.

* Quando esegui un flusso di lavoro Crea attività per una risorsa, nei messaggi di registro viene visualizzata l’eccezione Null Pointer.

* Quando si abilita la `Replace Spaces with DASH` l&#39;opzione di configurazione in Impostazioni avanzate in Experience Manager si traduce in creazione di cartelle duplicate in Workfront.

>[!IMPORTANT]
>
>L’Adobe consiglia di [aggiornamento alla versione più recente 1.9.1](../assets/update-workfront-enhanced-connector.md) del [!DNL Workfront for Experience Manager enhanced connector].

## Problemi noti {#known-issues}

* Durante la configurazione di cartelle collegate a un progetto con AEM 6.4, Experience Manager non salva i valori per **[!UICONTROL sottocartelle]** e **[!UICONTROL Crea cartella collegata in progetti con portfolio]** campi. Il valore per **[!UICONTROL sottocartelle]** aggiornamenti dei campi in **[!UICONTROL indefinito]** e il valore per **[!UICONTROL Crea cartella collegata in progetti con portfolio]** aggiornamenti dei campi in **[!UICONTROL Portfolio predefinito]** automaticamente dopo il salvataggio della configurazione.

* Quando utilizzi l’esperienza Workfront classica, la **[!UICONTROL Invia a]** opzione disponibile in **[!UICONTROL Altro]** l’elenco a discesa non consente di selezionare la destinazione all’interno di Experience Manager. La **[!UICONTROL Invia a]** funziona correttamente utilizzando **[!UICONTROL Azioni documento]** elenco a discesa. La **[!UICONTROL Invia a]** funziona correttamente per **[!UICONTROL Altro]** l’elenco a discesa e **[!UICONTROL Azioni documento]** elenco a discesa disponibile nella nuova esperienza Workfront.

## Versioni precedenti {#previous-releases}

### Versione di giugno 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* Quando effettui il caricamento tramite una cartella collegata o utilizzi la `Send To` azione disponibile in Workfront per caricare le risorse in Experience Manager as a Cloud Service, le risorse vengono danneggiate e non possono essere aperte in Adobe Photoshop.

### Versione di marzo 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* È ora possibile creare cartelle collegate tra Adobe Workfront e AEM Assets as a Cloud Service anche se sono presenti più configurazioni di cartelle collegate al progetto.

* È stato aggiunto il supporto per l’impaginazione dell’abbonamento a eventi.

* È stato aggiunto il supporto per AEM 6.4.x.

* È stato aggiunto il supporto per gli ambienti proxy.

* Diverse correzioni di bug si basano sul feedback di partner e clienti.

>[!MORELIKETHIS]
>
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

