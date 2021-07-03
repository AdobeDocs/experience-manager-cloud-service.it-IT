---
title: Archiviare e estrarre i file in [!DNL Assets]
description: Scopri come estrarre le risorse da modificare e archiviarle nuovamente al termine delle modifiche.
contentOwner: AG
feature: Gestione risorse
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Archiviazione e estrazione dei file in [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] consente di estrarre le risorse da modificare e di archiviarle nuovamente dopo aver completato le modifiche. Dopo aver estratto una risorsa, puoi modificarla, annotarla, pubblicarla, spostarla o eliminarla. Il ritiro di una risorsa blocca la risorsa. Altri utenti non possono eseguire nessuna di queste operazioni sulla risorsa finché non ricontrolli la risorsa in [!DNL Assets]. Tuttavia, possono comunque modificare i metadati della risorsa bloccata.

Per poter estrarre/inserire le risorse, è necessario disporre dell’accesso in scrittura.

Questa funzione consente di impedire ad altri utenti di ignorare le modifiche apportate da un autore, in cui più utenti collaborano alla modifica dei flussi di lavoro tra più team.

## Estrarre risorse {#checking-out-assets}

1. Dall’interfaccia utente di [!DNL Assets] , seleziona la risorsa da estrarre. È inoltre possibile selezionare più risorse da estrarre.

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Checkout]**. L&#39;opzione **[!UICONTROL Checkout]** passa a **[!UICONTROL Check-in]**.
Per verificare se altri utenti possono modificare la risorsa estratta, accedi come un altro utente. L’icona ![Blocco di pagamento](assets/do-not-localize/checkout_lock.png) viene visualizzata sulla miniatura della risorsa estratta.

   ![icona di pagamento nella vista a schede](assets/checkout-icon-card-view.png)

   Seleziona la risorsa. Nella barra degli strumenti non sono visualizzate opzioni che consentono di modificare, annotare, pubblicare o eliminare la risorsa.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Per modificare i metadati della risorsa bloccata, fai clic su **[!UICONTROL Visualizza proprietà]**.

1. Fai clic su **[!UICONTROL Modifica]** per aprire la risorsa in modalità di modifica.

1. Modifica la risorsa e salva le modifiche. Ad esempio, ritaglia l’immagine e salva. Puoi anche scegliere di annotare o pubblicare la risorsa.

1. Seleziona la risorsa modificata dall&#39;interfaccia [!DNL Assets] e fai clic su **[!UICONTROL Archivia]** nella barra degli strumenti. La risorsa modificata viene archiviata in [!DNL Assets] ed è disponibile per la modifica ad altri utenti.

## Check-in forzato {#forced-check-in}

Gli amministratori possono archiviare le risorse estratte da altri utenti.

1. Accedi a [!DNL Assets] come amministratore.
1. Dall’interfaccia utente di [!DNL Assets] , seleziona una o più risorse che sono state estratte da altri utenti.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Rilascia blocco]**. La risorsa viene archiviata ed è disponibile per la modifica ad altri utenti.

## Best practice e limitazioni {#tips-limitations}

* È possibile eliminare una *cartella* contenente file di risorse estratti. Prima di eliminare una cartella, accertati che gli utenti non abbiano estratto risorse digitali.

>[!MORELIKETHIS]
>
>* [Informazioni sull’app  [!DNL Experience Manager] indesktop di check-in e check-out](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Esercitazione video per comprendere il check-in e il check-out [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

