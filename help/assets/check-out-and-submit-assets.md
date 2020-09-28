---
title: Archiviare e estrarre i file [!DNL Assets]
description: Scoprite come estrarre le risorse per la modifica e archiviarle nuovamente al termine delle modifiche.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---


# Archiviazione e estrazione di file in risorse {#check-in-and-check-out-files-in-assets}

Risorse Adobe Experience Manager (AEM) consente di estrarre le risorse per modificarle e archiviarle nuovamente dopo aver completato le modifiche. Dopo aver estratto una risorsa, potete solo modificare, annotare, pubblicare, spostare o eliminare la risorsa. Il check-out di una risorsa blocca la risorsa. Altri utenti non possono eseguire nessuna di queste operazioni sulla risorsa finché non ricontrollate la risorsa in  AEM Assets. Tuttavia, possono comunque modificare i metadati della risorsa bloccata.

Per poter estrarre/archiviare le risorse, è necessario disporre dell&#39;accesso in scrittura.

Questa funzione consente di impedire ad altri utenti di ignorare le modifiche apportate da un autore, in cui più utenti collaborano ai flussi di lavoro di modifica tra più team.

## Estrazione delle risorse {#checking-out-assets}

1. Nell’interfaccia utente Risorse, seleziona la risorsa da estrarre. Potete anche selezionare più risorse da estrarre.

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Estrai]** .

   ![chlimage_1-469](assets/chlimage_1-469.png)

   Osservate che l&#39;icona **[!UICONTROL Checkout]** si sposta sull&#39;icona **[!UICONTROL Check]** con il blocco aperto.

   ![chlimage_1-470](assets/chlimage_1-470.png)

   Per verificare se altri utenti possono modificare la risorsa estratta, effettuate l’accesso come un altro utente. L’icona Blocca viene visualizzata sulla miniatura della risorsa estratta.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Selezionate la risorsa. Nella barra degli strumenti non sono visualizzate opzioni che consentono di modificare, annotare, pubblicare o eliminare la risorsa.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Potete tuttavia fare clic o toccare l’icona **[!UICONTROL Visualizza proprietà]** per modificare i metadati della risorsa bloccata.

1. Tocca o fai clic sull’icona Modifica per aprire la risorsa in modalità di modifica.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Modificate la risorsa e salvate le modifiche. Ad esempio, ritagliate l’immagine e salvate.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Potete anche scegliere di inserire delle annotazioni o pubblicare la risorsa.

1. Seleziona la risorsa modificata dall’interfaccia utente Assets, quindi tocca o fai clic sull’icona **[!UICONTROL Registra]** della barra degli strumenti.

   ![chlimage_1-475](assets/chlimage_1-475.png)

   La risorsa modificata viene archiviata in  AEM Assets ed è disponibile per la modifica da parte di altri utenti.

## Check-In forzato {#forced-check-in}

Gli amministratori possono archiviare le risorse sottoposte a Check-Out da altri utenti.

1. Accedete a  AEM Assets come amministratore.
1. Nell’interfaccia utente delle risorse, seleziona una o più risorse che sono state sottoposte a check-out da parte di altri utenti.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dalla barra degli strumenti, tocca o fai clic sull’icona **[!UICONTROL Rilascia blocco]** . La risorsa viene archiviata e può essere modificata da altri utenti.

   ![chlimage_1-477](assets/chlimage_1-477.png)