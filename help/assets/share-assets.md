---
title: Condivisione di risorse, cartelle e raccolte come collegamento
description: Questo articolo descrive come condividere risorse, cartelle e raccolte in Experience Manager Assets come collegamento ipertestuale.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Condivisione e distribuzione delle risorse gestite in Experience Manager {#share-assets-from-aem}

Risorse Adobe Experience Manager (AEM) consente di condividere risorse, cartelle e raccolte con membri dell’organizzazione ed entità esterne, inclusi partner e fornitori. Per condividere le risorse da Experience Manager Assets come servizio Cloud, puoi usare i seguenti metodi:

* Condividi come collegamento
* Scaricare le risorse
* Condivisione tramite l&#39;app desktop AEM
* Condividi tramite Adobe Asset Link
* (Funzionalità in arrivo) Condivisione tramite Brand Portal

## Condividere le risorse come collegamento {#sharelink}

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura sul `/var/dam/share` posto possono visualizzare i collegamenti condivisi con tali utenti. La condivisione di risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili a soggetti esterni senza dover prima accedere a Risorse AEM.

>[!NOTE]
>
>* È necessario disporre dell’autorizzazione Modifica ACL per la cartella o la risorsa da condividere come collegamento.
>* Prima di condividere un collegamento con gli utenti, assicurarsi che Day CQ Mail Service sia configurato. In caso contrario, si verifica un errore.


1. Nell’interfaccia utente Risorse, seleziona la risorsa da condividere come collegamento.
1. Dalla barra degli strumenti, tocca o fai clic su **[!UICONTROL Condividi collegamento]**.

   Nel campo **[!UICONTROL Condividi collegamento]** viene creato automaticamente un collegamento a una risorsa. Copiate questo collegamento e condividetelo con gli utenti. Il tempo di scadenza predefinito per il collegamento è un giorno.

   In alternativa, esegui i passaggi 3-7 di questa procedura per aggiungere i destinatari e-mail, configurare l’ora di scadenza del collegamento e inviarlo dalla finestra di dialogo.

   >[!NOTE]
   >
   >Se una risorsa condivisa viene spostata in un percorso diverso, il collegamento non funziona più. Create nuovamente il collegamento e condividete nuovamente con gli utenti.

1. Dalla console Web, aprite la configurazione **[!UICONTROL Day CQ Link Externalizer]** e modificate le seguenti proprietà nel campo **[!UICONTROL Domains]** con i valori indicati per ciascuno:

   * locale
   * author
   * pubblicazione
   Per le proprietà locale e di authoring, fornite l’URL rispettivamente per l’istanza locale e per l’istanza di creazione. Le proprietà locali e di authoring hanno lo stesso valore se si esegue una singola istanza di creazione AEM. Per la pubblicazione, fornite l’URL per l’istanza di pubblicazione.

1. Nella casella dell’indirizzo e-mail della finestra di dialogo Condivisione **** collegamento, digitate l’ID e-mail dell’utente con cui desiderate condividere il collegamento. Potete anche condividere il collegamento con più utenti.

   Se l’utente è membro dell’organizzazione, selezionate l’ID e-mail dell’utente dagli ID e-mail suggeriti che vengono visualizzati nell’elenco al di sotto dell’area di digitazione. Per un utente esterno, digitate l’ID e-mail completo e selezionatelo dall’elenco.

   Per abilitare l&#39;invio di e-mail agli utenti, configurate i dettagli del server SMTP in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >Se immettete un ID e-mail di un utente che non è membro dell’organizzazione, le parole &quot;Utente esterno&quot; hanno il prefisso &quot;ID e-mail dell’utente.

1. Nella casella **[!UICONTROL Oggetto]** , inserite l’oggetto della risorsa da condividere.
1. Nella casella **[!UICONTROL Messaggio]** , immettere un messaggio facoltativo.
1. Nel campo **[!UICONTROL Scadenza]** , specifica una data e un&#39;ora di scadenza per il collegamento utilizzando il selettore data. Per impostazione predefinita, la data di scadenza è impostata per una settimana dalla data di condivisione del collegamento.
1. Per consentire agli utenti di scaricare l&#39;immagine originale insieme alle rappresentazioni, selezionate **[!UICONTROL Consenti download del file]** originale.

   >[!NOTE]
   >
   >Per impostazione predefinita, gli utenti possono scaricare solo le rappresentazioni della risorsa condivisa come collegamento.

1. Fate clic su **[!UICONTROL Condividi]**. Un messaggio conferma la condivisione del collegamento con gli utenti tramite e-mail.
1. Per visualizzare la risorsa condivisa, toccate o fate clic sul collegamento contenuto nell&#39;e-mail inviata all&#39;utente. La risorsa condivisa viene visualizzata nella pagina **[!UICONTROL Adobe Marketing Cloud]** .

   Per passare alla vista a elenco, toccate o fate clic sull’icona del layout nella barra degli strumenti.

1. Per generare un’anteprima della risorsa, toccate o fate clic sulla risorsa condivisa. Per chiudere l&#39;anteprima e tornare alla pagina **[!UICONTROL Marketing Cloud]** , tocca o fai clic su **[!UICONTROL Indietro]** nella barra degli strumenti. Se avete condiviso una cartella, toccate o fate clic su Cartella **** principale per tornare alla cartella principale.

   >[!NOTE]
   >
   >AEM supporta la generazione dell’anteprima delle risorse di questi tipi MIME: JPG, PNG, GIF, BMP, INDD, PDF e PPT. Potete scaricare solo le risorse degli altri tipi MIME.

1. Per scaricare la risorsa condivisa, tocca o fai clic su **[!UICONTROL Seleziona]** dalla barra degli strumenti, tocca o fai clic sulla risorsa, quindi tocca o fai clic su **[!UICONTROL Scarica]** dalla barra degli strumenti.
1. Per visualizzare le risorse condivise come collegamenti, accedete all’interfaccia utente delle risorse e toccate o fate clic sull’icona di navigazione globale. Scegliere **[!UICONTROL Navigazione]** dall&#39;elenco per visualizzare il riquadro di navigazione.
1. Nel riquadro di navigazione, scegliete Collegamenti **** condivisi per visualizzare un elenco delle risorse condivise.
1. Per annullare la condivisione di una risorsa, selezionatela e toccate o fate clic su **[!UICONTROL Annulla condivisione]** nella barra degli strumenti.

Viene visualizzato un messaggio di conferma dell’annullamento della condivisione della risorsa. Inoltre, la voce relativa alla risorsa viene rimossa dall’elenco.

## Scaricare e condividere le risorse {#download-and-share-assets}

Gli utenti possono scaricare alcune risorse e condividerle al di fuori di Experience Manager. Per ulteriori informazioni, consultate [come cercare risorse](/help/assets/search-assets.md), [scaricare risorse](/help/assets/download-assets-from-aem.md)e [scaricare raccolte](manage-collections.md#download-a-collection)

## Condivisione di risorse con creativi professionisti {#share-with-creatives}

Gli addetti al marketing e gli utenti della linea di business possono condividere facilmente le risorse approvate con i loro creativi professionisti che utilizzano,

* **App** desktop AEM: L&#39;app funziona su Windows e Mac. Consultate Panoramica delle app [desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html). Per sapere in che modo qualsiasi utente desktop autorizzato può accedere facilmente alle risorse condivise, consultate [sfogliare, cercare e visualizzare in anteprima le risorse](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Gli utenti desktop possono creare nuove risorse e condividerle con colleghi utenti AEM, ad esempio caricando nuove immagini. Consultate [Caricare le risorse tramite l’app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)desktop.

* **Collegamento** risorse Adobe: I creativi professionisti possono cercare e utilizzare le risorse direttamente da Adobe InDesign, Adobe Illustrator e Adobe Photoshop.

### Best practices and troubleshooting {#bestpractices}

* Le cartelle di risorse o le raccolte che contengono uno spazio vuoto nel loro nome potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verificate con il vostro amministratore AEM i limiti [di](/help/assets/configure-asset-sharing.md#maxdatasize) download.
* Se non potete inviare e-mail con collegamenti a risorse condivise o se gli altri utenti non possono ricevere l’e-mail, verificate con l’amministratore AEM se il servizio [e-](/help/assets/configure-asset-sharing.md#configmailservice) mail è configurato o meno.
* Se non potete condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti, accertatevi di disporre delle autorizzazioni appropriate. Consultate [Condividere le risorse](#sharelink).

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
