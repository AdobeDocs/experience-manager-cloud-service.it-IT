---
title: Condividi Assets in [!DNL the Content Hub]
description: Condividi Assets in [!DNL the Content Hub]
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Si applica ad AEM Assets)."
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 2%

---

# Condividere risorse in Content Hub {#search-assets-as-a-link}

Crea un collegamento alle risorse selezionate per condividerle facilmente con altri utenti. In qualità di utente [!DNL Content Hub] autorizzato, seleziona una o più risorse disponibili nell&#39;ambiente [!DNL Content Hub], genera un collegamento e invialo ad altri utenti pubblici o privati.

>[!VIDEO](https://video.tv.adobe.com/v/3474890/?learn=on&enablevpops=on){transcript=true}

## Prerequisiti {#prerequisites}

[Gli utenti di Content Hub](deploy-content-hub.md#onboard-content-hub-users) possono creare un collegamento alle risorse selezionate e condividerlo con altri utenti.

## Condividere le risorse {#share-assets}

Per condividere una o più risorse con utenti privati o pubblici, effettua le seguenti operazioni:

1. Passa alla home page di [!DNL Content Hub], seleziona una o più risorse e fai clic su ![condividi](/help/assets/assets/share.svg) **[!UICONTROL Condividi]** per visualizzare una singola risorsa selezionata o un elenco di più risorse selezionate nella finestra di dialogo **[!UICONTROL Condividi risorse]**.

   Puoi anche selezionare e condividere le risorse disponibili in ![raccolte](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL raccolte]**.

1. Visualizza una risorsa o controlla l&#39;elenco delle risorse disponibili nella finestra di dialogo **[!UICONTROL Condividi risorse]**. Fai clic su ![deseleziona](/help/assets/assets/Close.svg) accanto a una risorsa per rimuoverla dall&#39;elenco.

1. Specifica un titolo e una descrizione facoltativa che definisca il set di risorse selezionate.

1. Seleziona **[!UICONTROL Periodo di scadenza]**.

1. Nel menu a discesa **[!UICONTROL Chi può accedere]**, seleziona le opzioni di accesso e fai clic su **[!UICONTROL Ottieni collegamento]** per generare un collegamento da condividere con gli utenti selezionati. Gli utenti privati devono accedere al proprio ambiente [!DNL Content Hub] per accedere alla pagina delle risorse condivise. Gli utenti pubblici, invece, come ospiti possono accedere alla pagina delle risorse condivise senza accedere a [!DNL Content Hub].

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![collegamento pubblico e privato](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> [Abilita la condivisione di collegamenti pubblici dalla pagina di configurazione](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) per visualizzare **[!UICONTROL Collegamento pubblico]** nella finestra di dialogo **[!UICONTROL Condividi risorse]**.

## Condividere una risorsa dalla sua pagina di anteprima {#share-asset-from-preview-page}

Per condividere una risorsa durante l’anteprima, esegui la procedura seguente:

1. Passa alla home page di [!DNL Content Hub] e fai clic sulla miniatura della risorsa per visualizzare l&#39;anteprima della risorsa e le opzioni di menu nel riquadro a destra della finestra di dialogo.
1. Seleziona ![condividi](/help/assets/assets/share.svg) per visualizzare il pannello **[!UICONTROL Condividi]**.
   ![condividi risorsa durante l&#39;anteprima](/help/assets/assets/share-link-asset-preview.png)
1. Segui i passaggi da 3 a 5 nella sezione [Condividi risorse](#share-assets) per generare e condividere il collegamento alle risorse (privato o pubblico) da questo pannello **[!UICONTROL Condividi]**.

## Accedere alle risorse condivise {#access-shared-assets}

Accedi alla pagina delle risorse condivise tramite il collegamento ed effettua le seguenti operazioni:

* Seleziona una o più risorse e fai clic su ![scarica](/help/assets/assets/download-icon.svg) **[!UICONTROL Scarica]** per selezionare le rappresentazioni **[!UICONTROL Originale]**, **[!UICONTROL Statico]** o entrambe dalle opzioni di download disponibili.
  ![](/help/assets/assets/download-shared-assets.png)
* Fai clic sulla miniatura della risorsa per visualizzarne i metadati.
* Nella pagina delle risorse condivise ([a cui si accede tramite un collegamento privato](#share-assets)), fai clic sulla miniatura di una risorsa e seleziona ![scarica](/help/assets/assets/download-icon.svg) per selezionare e visualizzare le rappresentazioni dinamiche disponibili della risorsa nel pannello **[!UICONTROL Scarica]** prima di selezionarle e scaricarle.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)

## Domande frequenti {#faqs-share-assets-content-hub}

### Cosa significa la condivisione di risorse in AEM Assets Content Hub?

La condivisione di risorse in AEM Assets Content Hub consente agli utenti autorizzati di condividere facilmente una o più risorse o intere raccolte con altri utenti generando un collegamento. Questo collegamento può essere inviato a utenti privati (che devono effettuare l&#39;accesso) o pubblici (che possono accedere come ospiti), consentendo ai destinatari di accedere direttamente alla visualizzazione e al download delle risorse selezionate.

### Come posso condividere risorse o raccolte con altri tramite AEM Assets Content Hub?

Per condividere risorse o raccolte in Content Hub, passa alla home page di Content Hub, seleziona una o più risorse (oppure passa alla scheda Raccolte per le raccolte) e fai clic sull’icona Condividi. Nella finestra di dialogo Condividi puoi visualizzare in anteprima le risorse, rimuoverle se necessario, aggiungere un titolo e una descrizione, selezionare chi può accedere al collegamento (privato o pubblico), impostare un periodo di scadenza e quindi fare clic su Ottieni collegamento per generare e copiare l’URL condivisibile. Il collegamento può quindi essere inviato ai membri del gruppo o alle parti interessate.

### Quali opzioni di accesso sono disponibili per la condivisione di risorse in AEM Assets Content Hub, e quali sono le loro differenze?

Content Hub consente di scegliere tra due opzioni di accesso per i collegamenti condivisi: privato e pubblico. I collegamenti privati richiedono ai destinatari di accedere al proprio ambiente Content Hub per visualizzare e scaricare le risorse, garantendo così una maggiore sicurezza. Chiunque disponga del collegamento può accedere ai collegamenti pubblici senza richiedere l’accesso. Ogni tipo di collegamento viene fornito con impostazioni di scadenza personalizzate, ad esempio da 24 ore a una settimana per i collegamenti pubblici e date personalizzate per i collegamenti privati.

### Esiste una configurazione gestita dall’amministratore per poter generare collegamenti pubblici per le risorse in AEM Assets Content Hub?

Sì, gli amministratori possono abilitare o disabilitare l&#39;interruttore **Abilita collegamento pubblico** disponibile nella scheda **Raccolte e condivisione** dell&#39;interfaccia utente di configurazione per gestire la generazione di collegamenti pubblici per le risorse in AEM Assets Content Hub.

### Posso impostare le date di scadenza per i collegamenti alle risorse condivise in AEM Assets Content Hub, e perché è importante?

Sì, puoi impostare le date di scadenza per i collegamenti condivisi pubblici e privati in Content Hub. Per i collegamenti pubblici, puoi scegliere tra predefiniti come 24 ore fino a una settimana, mentre i collegamenti privati consentono di selezionare tra predefiniti o impostare una data di scadenza personalizzata. Le date di scadenza sono importanti perché una volta scaduto il collegamento non può più essere utilizzato per accedere o scaricare le risorse, il che consente di mantenere la sicurezza e il controllo dei contenuti.

### Che cosa possono fare i destinatari con il collegamento alle risorse condivise creato utilizzando AEM Assets Content Hub e quali sono le opzioni per scaricare rappresentazioni diverse?

I destinatari che ricevono un collegamento a una risorsa condivisa possono aprirlo nel browser per visualizzare in anteprima, selezionare e scaricare le risorse fornite. Se in Content Hub sono abilitate le rappresentazioni delle risorse, i destinatari possono scegliere quali copie trasformate (ad esempio Originale o Statica) scaricare. Le risorse e le rappresentazioni vengono scaricate come file zip e i metadati possono essere visualizzati facendo clic sulla miniatura della risorsa. Il collegamento rimane funzionante fino alla data di scadenza impostata.




