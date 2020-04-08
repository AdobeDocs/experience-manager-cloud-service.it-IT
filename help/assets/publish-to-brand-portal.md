---
title: Pubblicare risorse, cartelle e raccolte in Brand Portal
description: Pubblicate risorse, cartelle e raccolte in Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: c2088896eacfc1f0e4c5b7a1f566ce3c8f99388b

---


# Publish assets to Brand Portal {#publish-assets-to-brand-portal}

In qualità di amministratore di Risorse Adobe Experience Manager (AEM), puoi pubblicare risorse, cartelle e raccolte nell’istanza del Brand Portal di AEM Assets. Inoltre, potete pianificare il flusso di lavoro di pubblicazione di una risorsa o di una cartella in una data o in un&#39;ora successive. Dopo la pubblicazione, gli utenti di Brand Portal possono accedere e distribuire ulteriormente le risorse, le cartelle e le raccolte ad altri utenti.

Tuttavia, devi prima configurare AEM Assets con il Portale marchio. Per informazioni dettagliate, consultate [Configurare AEM Assets con il Portale](configure-aem-assets-with-brand-portal.md)marchio.

Se effettui modifiche successive alla risorsa, alla cartella o alla raccolta originale in Risorse AEM, le modifiche non verranno riportate nel Portale marchio fino alla ripubblicazione da Risorse AEM. Questa funzione garantisce che le modifiche in corso non siano disponibili in Brand Portal. Solo le modifiche approvate pubblicate da un amministratore sono disponibili in Brand Portal.

* [Pubblicare risorse su Brand Portal](#publish-assets-to-bp)
* [Pubblicare le cartelle su Brand Portal](#publish-folders-to-brand-portal)
* [Pubblicare raccolte in Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe consiglia la pubblicazione scaglionata, preferibilmente nelle ore non di picco, in modo che l’autore di AEM non occupi risorse in eccesso.


## Publish assets to Brand Portal {#publish-assets-to-bp}

Di seguito sono riportati i passaggi per pubblicare risorse da Risorse AEM al Portale dei marchi:

1. Dalla console Risorse, aprite la cartella principale e selezionate tutte le risorse da pubblicare, quindi fate clic sull’opzione Pubblicazione **** rapida nella barra degli strumenti.

   ![publish2bp-2](assets/publish2bp.png)

1. Di seguito sono riportati due modi per pubblicare le risorse:
   * [Pubblica ora](#publish-to-bp-now) (Pubblica subito le risorse)
   * [Pubblicare in un secondo momento](#publish-to-bp-later) (pianificare le risorse di pubblicazione)

### Pubblica subito le risorse {#publish-to-bp-now}

Per pubblicare le risorse selezionate in Brand Portal, effettuate una delle seguenti operazioni:

* Dalla barra degli strumenti, selezionate Pubblicazione **** rapida. Dal menu, fate clic su **[!UICONTROL Pubblica su Brand Portal]**.

* Dalla barra degli strumenti, selezionate **[!UICONTROL Gestisci pubblicazione]**.

   1. In **[!UICONTROL Azione]**, selezionate **[!UICONTROL Pubblica su Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, selezionate **[!UICONTROL Ora]**.

      Fai clic su **[!UICONTROL Avanti]**.

   2. Conferma la selezione nell’ **[!UICONTROL ambito]** e fai clic su **[!UICONTROL Pubblica sul portale]** del marchio.

Viene visualizzato un messaggio che informa che le risorse sono state messe in coda per la pubblicazione sul Brand Portal. Per visualizzare le risorse pubblicate, effettuate l’accesso all’interfaccia del Portale marchio.

### Pubblicare le risorse in un secondo momento {#publish-to-bp-later}

Per pianificare la pubblicazione delle risorse su Brand Portal in una data o un’ora successiva:

1. Selezionate le risorse da pianificare per la pubblicazione e fate clic su **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti nella parte superiore.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione]** , seleziona **[!UICONTROL Pubblica su Brand Portal]** dall’ **[!UICONTROL azione]**.

   Selezionare **[!UICONTROL Più tardi]** da **[!UICONTROL Pianificazione]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Selezionate una data **[!UICONTROL di]** attivazione e specificate l&#39;ora. Fai clic su **[!UICONTROL Avanti]**.

1. Selezionate una data **di** attivazione e specificate l&#39;ora. Fai clic su **Avanti**.

1. Specificate un titolo **** Flusso di lavoro in **[!UICONTROL Flussi di lavoro]**. Fate clic su **[!UICONTROL Pubblica più tardi]**.

   ![publishworkflow](assets/publishworkflow.png)

Effettuate l’accesso all’interfaccia del Portale marchio per visualizzare le risorse pubblicate (a seconda della data o dell’ora pianificata).

![bp_landing_page](assets/bp_landing_page.png)


## Publish folders to Brand Portal {#publish-folders-to-brand-portal}

Potete pubblicare o annullare la pubblicazione immediata delle cartelle di risorse oppure pianificare la pubblicazione in un secondo momento o ora.

### Publish folders to Brand Portal {#publish-folders-to-bp}

1. Dalla console Risorse, selezionate le cartelle da pubblicare e fate clic sull’opzione Pubblicazione **** rapida nella barra degli strumenti.

   ![publish2bp](assets/publish2bp.png)

1. **Pubblica le cartelle ora**

   Per pubblicare le cartelle selezionate in Brand Portal, effettuate una delle seguenti operazioni:

   * Dalla barra degli strumenti, selezionate Pubblicazione **** rapida.

      Dal menu, selezionate **[!UICONTROL Pubblica su Brand Portal]**.

   * Dalla barra degli strumenti, selezionate **[!UICONTROL Gestisci pubblicazione]**.

      1. In **[!UICONTROL Azione]**, selezionate **[!UICONTROL Pubblica su Brand Portal]**.

         In **[!UICONTROL Pianificazione]**, selezionate **[!UICONTROL Ora]**.

         Fai clic su **Avanti.**

      1. Conferma la selezione nell’ **[!UICONTROL ambito]** e fai clic su **[!UICONTROL Pubblica sul portale]** del marchio.
   Viene visualizzato un messaggio che informa che la cartella è stata messa in coda per la pubblicazione sul Brand Portal. Accedete all’interfaccia Brand Portal per visualizzare la cartella pubblicata.

1. **Pubblicare le cartelle in un secondo momento**

   Per pianificare la pubblicazione delle cartelle delle risorse in una data o in un’ora successiva:

   1. Selezionate le cartelle da pianificare per la pubblicazione, quindi selezionate **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti nella parte superiore.
   1. In **[!UICONTROL Azione]**, selezionate **[!UICONTROL Pubblica su Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, selezionate **[!UICONTROL Più tardi]**.

   1. Selezionate una data **[!UICONTROL di]** attivazione e specificate l&#39;ora. Fai clic su **[!UICONTROL Avanti]**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Conferma la selezione nell’ **[!UICONTROL ambito]**. Fai clic su **[!UICONTROL Avanti]**.

   1. Specificate un titolo del flusso di lavoro in **[!UICONTROL Flussi di lavoro]**. Fate clic su **[!UICONTROL Pubblica più tardi]**.

      ![manageschedulepub](assets/manageschedulepub.png)

### Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

Per rimuovere una qualsiasi cartella di risorse pubblicata nel Portale marchio, annulla la pubblicazione dall’istanza di Risorse AEM. Dopo l’annullamento della pubblicazione della cartella originale, la relativa copia non sarà più disponibile per gli utenti di Brand Portal.

Potete annullare la pubblicazione immediata delle cartelle di risorse da Brand Portal oppure pianificare la pubblicazione in un secondo momento e ora.

Per annullare la pubblicazione delle cartelle di risorse da Brand Portal:

1. Dalla console Risorse, selezionate le cartelle di risorse da pubblicare e fate clic sull’opzione **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti.

   ![publish2bp-1](assets/publish2bp.png)

1. **Annulla pubblicazione cartelle risorse**

   Per annullare immediatamente la pubblicazione della cartella di risorse selezionata dal Brand Portal:

   1. Dalla barra degli strumenti, selezionate **[!UICONTROL Gestisci pubblicazione]**.

   1. In **[!UICONTROL Azione]** , selezionate **[!UICONTROL Annulla pubblicazione da Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, selezionate **[!UICONTROL Ora]**.

      Fai clic su **[!UICONTROL Avanti]**.

   1. Confermate la selezione nell&#39; **[!UICONTROL ambito]** e fate clic su **[!UICONTROL Annulla pubblicazione dal portale]** marchio.

      ![confirm-unpublish](assets/confirm-unpublish.png)

1. **Annullare la pubblicazione delle cartelle delle risorse in un secondo momento**

   Per pianificare l’annullamento della pubblicazione di una cartella di risorse in una data e in un’ora successive:

   1. Dalla barra degli strumenti, selezionate **[!UICONTROL Gestisci pubblicazione]**.

   1. In **[!UICONTROL Azione]**, selezionate **[!UICONTROL Annulla pubblicazione da Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, selezionate **[!UICONTROL Più tardi]**.

   1. Selezionate una data **[!UICONTROL di]** attivazione e specificate l’ora. Fai clic su **[!UICONTROL Avanti]**.

   1. Conferma la selezione nell’ **[!UICONTROL ambito]** e fai clic su **[!UICONTROL Avanti]**.

   1. Specificate un titolo **** Flusso di lavoro in **[!UICONTROL Flussi di lavoro]**. Fate clic su **[!UICONTROL Annulla pubblicazione più tardi]**.

      ![flussi di lavoro non pubblicati](assets/unpublishworkflows.png)

## Publish collections to Brand Portal {#publish-collections-to-brand-portal}

Puoi pubblicare o annullare la pubblicazione delle raccolte dall’istanza cloud di AEM Assets.

>[!NOTE]
>
>I frammenti di contenuto non possono essere pubblicati sul Brand Portal. Pertanto, se selezioni frammenti di contenuto in Risorse AEM, l’azione **[!UICONTROL Pubblica su Portale]** marchio non è disponibile.
>
>Se le raccolte contenenti frammenti di contenuto sono pubblicate da Risorse AEM al Portale del marchio, tutto il contenuto della cartella tranne i frammenti di contenuto viene replicato nell&#39;interfaccia del Portale del marchio.


### Pubblicare le raccolte {#publish-collections}

Seguono i passaggi per pubblicare le raccolte da Risorse AEM al Brand Portal:

1. Nell’interfaccia utente di Risorse AEM, fai clic sul logo AEM.

1. From **Navigation** page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

1. Dalla console **Raccolte** , selezionate le raccolte che desiderate pubblicare sul portale del marchio.

   ![select_collection](assets/select_collection.png)

1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Pubblica su Brand Portal]**.

1. Nella finestra di dialogo di conferma, fate clic su **[!UICONTROL Pubblica]**.

1. Chiudi il messaggio di conferma.

   Accedete a Brand Portal come amministratore. La raccolta pubblicata è disponibile nella console Raccolte.

   ![raccolta pubblicata](assets/published_collection.png)

### Annullamento della pubblicazione delle raccolte {#unpublish-collections}

Potete rimuovere qualsiasi raccolta pubblicata in Brand Portal annullarne la pubblicazione dall&#39;istanza di AEM Assets. Dopo aver annullato la pubblicazione della raccolta originale, la relativa copia non è più disponibile per gli utenti di Brand Portal.

Di seguito sono riportati i passaggi per annullare la pubblicazione di una raccolta:

1. Dalla console **Raccolte** dell’istanza Risorse AEM, quindi selezionate la raccolta da annullare la pubblicazione.

   ![select_collection-1](assets/select_collection-1.png)

1. Dalla barra degli strumenti, fate clic sull’icona **[!UICONTROL Rimuovi da Brand Portal]** .
1. Nella finestra di dialogo, fate clic su **[!UICONTROL Annulla pubblicazione]**.
1. Chiudi il messaggio di conferma. La raccolta viene rimossa dall&#39;interfaccia Brand Portal.

Consultate la documentazione [di](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) Brand Portal per ulteriori informazioni sulla distribuzione di risorse, cartelle e raccolte agli utenti finali.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
