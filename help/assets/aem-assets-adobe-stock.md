---
title: Gestire  [!DNL Adobe Stock] le risorse in [!DNL Assets].
description: Cercare, recuperare, ottenere licenze e gestire risorse [!DNL Adobe Stock] dall'interno di [!DNL Adobe Experience Manager]. Utilizzate le risorse con licenza come qualsiasi altra risorsa digitale.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 5%

---


# Utilizzare risorse [!DNL Adobe Stock] in [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Le organizzazioni possono integrare il piano aziendale [!DNL Adobe Stock] con [!DNL Experience Manager Assets] per garantire che le risorse su licenza siano ampiamente disponibili per i loro progetti creativi e di marketing, con le potenti funzionalità di gestione delle risorse di [!DNL Experience Manager].

[!DNL Adobe Stock]Il servizio offre a designer e aziende l’accesso a milioni di foto, immagini vettoriali, illustrazioni, video, modelli e risorse 3D di alta qualità, curate ed esenti da royalty, per qualsiasi progetto creativo. [!DNL Experience Manager] gli utenti possono trovare, visualizzare in anteprima e concedere in licenza  [!DNL Adobe Stock] le risorse salvate in  [!DNL Experience Manager]senza uscire dall&#39; [!DNL Experience Manager] interfaccia.

## Integrare [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Per consentire la comunicazione tra [!DNL Experience Manager] e [!DNL Adobe Stock], creare una configurazione IMS e una configurazione [!DNL Adobe Stock] in [!DNL Experience Manager].

>[!NOTE]
>
>L&#39;integrazione può essere eseguita solo dagli amministratori [!DNL Experience Manager] e dagli amministratori [!DNL Admin Console] di un&#39;organizzazione, in quanto richiede privilegi di amministratore.

### Creare una configurazione IMS {#create-an-ims-configuration}

1. Nell&#39;interfaccia utente [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni IMS  Adobe]**. Fai clic su **[!UICONTROL Crea]** e seleziona **[!UICONTROL Soluzione cloud]** > **[!UICONTROL Adobe Stock]**.
1. Riutilizzare un certificato esistente o selezionare **[!UICONTROL Crea nuovo certificato]**.
1. Fai clic su **[!UICONTROL Crea certificato]**. Una volta creata, scaricate la chiave pubblica. Fai clic su **[!UICONTROL Avanti]**.
1. Aggiungi la chiave pubblica scaricata al tuo account di servizio [!DNL Adobe Developer Console]. Fai clic su **[!UICONTROL Avanti]**. Lasciate aperta la schermata [!UICONTROL  Adobe IMS Technical Account Configuration] per fornire i valori a breve.
1. Accedi a [ Adobe Developer Console](https://console.adobe.io). Assicuratevi che l&#39;account disponga delle autorizzazioni di amministratore per l&#39;organizzazione per la quale è richiesta l&#39;integrazione.
1. Fare clic su **[!UICONTROL Crea nuovo progetto]** e fare clic su **[!UICONTROL Aggiungi API]**. Selezionare **[!UICONTROL Adobe Stock]** dall&#39;elenco delle API disponibili. Selezionare [!UICONTROL OAUTH 2.0 Web]. Configurare e copiare i vari valori presentati.
1. In [!DNL Experience Manager] fornire i valori nei campi denominati **[!UICONTROL Titolo]**, **[!UICONTROL Server di autorizzazione]**, **[!UICONTROL Chiave API]**, **[!UICONTROL Segreto cliente]** e **[!UICONTROL Payload]**. Per informazioni dettagliate su questi valori, vedere [Avvio rapido dell&#39;autenticazione JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Crea configurazione [!DNL Adobe Stock] in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Fate clic su **[!UICONTROL Crea]** per creare una configurazione e associarla alla configurazione IMS esistente. Selezionare `PROD` come parametro di ambiente.
1. Nel campo **[!UICONTROL Percorso risorse con licenza]**, lasciare una posizione invariata. Non modificate la posizione in cui desiderate memorizzare le risorse [!DNL Adobe Stock].
1. Completate la creazione aggiungendo tutte le proprietà richieste. Fai clic su **[!UICONTROL Salva e chiudi]**.
1. Aggiungete utenti o gruppi [!DNL Experience Manager] che possono ottenere la licenza per le risorse.

>[!NOTE]
>
>Se sono presenti più configurazioni [!DNL Adobe Stock], selezionate la configurazione desiderata nel pannello Preferenze utente. Per accedere al pannello dalla home page  Experience Manager, fare clic sull&#39;icona utente, quindi fare clic su **[!UICONTROL Preferenze utente]** > **[!UICONTROL Configurazione stock]**.

## Utilizzare e gestire le risorse [!DNL Adobe Stock] in [!DNL Experience Manager] {#usemanage}

Grazie a questa funzionalità, le organizzazioni possono consentire agli utenti di utilizzare le risorse [!DNL Adobe Stock] in [!DNL Experience Manager Assets]. Dall&#39;interfaccia utente di [!DNL Experience Manager], gli utenti possono cercare [!DNL Adobe Stock] risorse e ottenere la licenza per le risorse necessarie.

Una volta ottenuta la licenza di una risorsa [!DNL Adobe Stock] in [!DNL Experience Manager], questa può essere utilizzata e gestita come una risorsa tipica. In [!DNL Experience Manager], gli utenti possono cercare e visualizzare in anteprima le risorse; copiare e pubblicare le risorse; condividere le risorse su [!DNL Brand Portal]; accedere e utilizzare le risorse tramite l&#39;app desktop [!DNL Experience Manager]; e così via.

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### Trova risorse {#find-assets}

Gli utenti [!DNL Experience Manager] possono cercare risorse sia in [!DNL Experience Manager] che in [!DNL Adobe Stock]. Quando il percorso di ricerca non è limitato a [!DNL Adobe Stock], vengono visualizzati i risultati di ricerca di [!DNL Experience Manager] e [!DNL Adobe Stock].

* Per cercare le risorse [!DNL Adobe Stock], fare clic su **[!UICONTROL Navigazione]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cerca  Adobe Stock]**.

* Per cercare risorse tra [!DNL Adobe Stock] e [!DNL Experience Manager Assets], fare clic su Cerca ![search](assets/do-not-localize/search_icon.png).

In alternativa, iniziate a digitare `Location: Adobe Stock` nella barra di ricerca per selezionare le risorse [!DNL Adobe Stock]. [!DNL Experience Manager] offre funzionalità di filtro avanzate sulle risorse ricercate, che consentono agli utenti di accedere rapidamente alle risorse necessarie tramite filtri, quali tipi di risorse supportate, orientamento delle immagini e stato della licenza.

>[!NOTE]
>
>Le risorse ricercate da [!DNL Adobe Stock] vengono visualizzate in [!DNL Experience Manager]. [!DNL Adobe Stock] le risorse vengono recuperate e memorizzate nell’ [!DNL Experience Manager] archivio solo dopo che un utente  [salva una ](/help/assets/aem-assets-adobe-stock.md#saveassets) risorsa o  [le licenze e salva una risorsa](/help/assets/aem-assets-adobe-stock.md#licenseassets). Le risorse già memorizzate in [!DNL Experience Manager] vengono visualizzate ed evidenziate per semplificare il riferimento e l&#39;accesso. Inoltre, le risorse [!DNL Stock] vengono salvate con alcuni metadati aggiuntivi per indicare l&#39;origine come [!DNL Stock].

![Filtri di ricerca in  Experience Manager ed evidenziati  risorse Adobe Stock nei risultati di ricerca](assets/aem-search-filters2.jpg)

*Figura: Consente di cercare filtri  [!DNL Experience Manager] e  [!DNL Adobe Stock] risorse evidenziate nei risultati della ricerca.*

### Salvare e visualizzare le risorse necessarie {#saveassets}

Selezionate una risorsa da salvare in [!DNL Experience Manager]. Fate clic su [!UICONTROL Salva] nella barra degli strumenti nella parte superiore e fornite il nome e la posizione della risorsa. Le risorse senza licenza vengono salvate localmente con una filigrana.

La prossima volta che ricercate le risorse, queste vengono evidenziate con un contrassegno, per indicare che sono disponibili in [!DNL Experience Manager Assets].

>[!NOTE]
>
>Le risorse aggiunte di recente visualizzano un nuovo contrassegno invece del contrassegno Con licenza.

### Risorse di licenza {#licenseassets}

Gli utenti possono ottenere la licenza per le risorse [!DNL Adobe Stock] utilizzando la quota del proprio piano aziendale [!DNL Adobe Stock]. Quando si concede la licenza per una risorsa, questa viene salvata senza filigrana ed è disponibile per la ricerca e l&#39;utilizzo in [!DNL Experience Manager Assets].

![Finestra di dialogo per ottenere la licenza e salvare  risorse Adobe Stock in  risorse Experience Manager](assets/aem-stock_licenseandsave.jpg)

*Figura: Finestra di dialogo per ottenere la licenza e salvare  [!DNL Adobe Stock] le risorse in  [!DNL Experience Manager Assets].*

### Accesso a metadati e proprietà delle risorse {#access-metadata-and-asset-properties}

Gli utenti possono accedere ai metadati e visualizzarne l&#39;anteprima, comprese le proprietà dei metadati [!DNL Adobe Stock] per le risorse salvate in [!DNL Experience Manager], e aggiungere **[!UICONTROL Riferimenti alle licenze]** per una risorsa. Tuttavia, gli aggiornamenti al riferimento della licenza non vengono sincronizzati tra il sito Web [!DNL Experience Manager] e [!DNL Adobe Stock].

Gli utenti possono visualizzare le proprietà per risorse con licenza e senza licenza.

![Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate](assets/metadata_properties.jpg)

*Figura: Visualizzare e accedere ai metadati e ai riferimenti di licenza delle risorse salvate.*

## Limitazioni note {#known-limitations}

* **L&#39;avviso dell&#39;immagine editoriale non viene visualizzato**: Quando si concede la licenza a un’immagine, gli utenti non possono verificare se un’immagine è solo di uso editoriale. Per evitare possibili abusi, gli amministratori possono disattivare l’accesso alle risorse editoriali dal Admin Console .

* **Viene visualizzato** un tipo di licenza errato: È possibile che venga visualizzato un tipo di licenza non corretto  [!DNL Experience Manager] per una risorsa. Gli utenti possono accedere al sito Web [!DNL Adobe Stock] per visualizzare il tipo di licenza.

* **I campi e i metadati di riferimento non sono sincronizzati**: Quando un utente aggiorna un campo di riferimento della licenza, le informazioni di riferimento della licenza vengono aggiornate  [!DNL Experience Manager] ma non sul  [!DNL Adobe Stock] sito Web. Analogamente, se l&#39;utente aggiorna i campi di riferimento nel sito Web [!DNL Adobe Stock], gli aggiornamenti non vengono sincronizzati in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Esercitazione video sull’uso  risorse Adobe Stock con  risorse Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [ del piano aziendale Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Domande frequenti su  Adobe Stock](https://helpx.adobe.com/stock/faq.html)

