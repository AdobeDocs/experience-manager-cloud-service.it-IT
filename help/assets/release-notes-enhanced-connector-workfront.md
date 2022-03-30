---
title: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
description: Note sulla versione [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 02df53e47d2b8617c9a81f5c438814996af92340
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 5%

---


# Note sulla versione [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

La sezione seguente illustra le note generali sulla versione di [!DNL Workfront for Experience Manager enhanced connector].

## Data di pubblicazione {#release-date}

Data di rilascio dell’ultima versione di [!DNL Workfront for Experience Manager enhanced connector] è il 28 marzo 2022.

## Funzioni principali {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] ora include i seguenti aggiornamenti:

* È ora possibile creare cartelle collegate tra Adobe Workfront e AEM Assets as a Cloud Service anche se sono presenti più configurazioni di cartelle collegate al progetto.

* È stato aggiunto il supporto per l’impaginazione dell’abbonamento a eventi.

* È stato aggiunto il supporto per AEM 6.4.x.

* È stato aggiunto il supporto per gli ambienti proxy.

* Diverse correzioni di bug si basano sul feedback di partner e clienti.

## Problemi noti {#known-issues}

* Durante la configurazione di cartelle collegate a un progetto con AEM 6.4, Experience Manager non salva i valori per **[!UICONTROL sottocartelle]** e **[!UICONTROL Crea cartella collegata in progetti con portfolio]** campi. Il valore per **[!UICONTROL sottocartelle]** aggiornamenti dei campi in **[!UICONTROL indefinito]** e il valore per **[!UICONTROL Crea cartella collegata in progetti con portfolio]** aggiornamenti dei campi in **[!UICONTROL Portfolio predefinito]** automaticamente dopo il salvataggio della configurazione.

* Quando utilizzi l’esperienza Workfront classica, la **[!UICONTROL Invia a]** opzione disponibile in **[!UICONTROL Altro]** l’elenco a discesa non consente di selezionare la destinazione all’interno di Experience Manager. La **[!UICONTROL Invia a]** funziona correttamente utilizzando **[!UICONTROL Azioni documento]** elenco a discesa. La **[!UICONTROL Invia a]** funziona correttamente per **[!UICONTROL Altro]** l’elenco a discesa e **[!UICONTROL Azioni documento]** elenco a discesa disponibile nella nuova esperienza Workfront.

>[!MORELIKETHIS]
>
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrare [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)


