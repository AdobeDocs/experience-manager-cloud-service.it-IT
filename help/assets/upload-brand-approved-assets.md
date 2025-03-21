---
title: Carica le risorse approvate dal tuo marchio in [!DNL Content Hub]
description: Scopri come caricare le risorse approvate dal marchio in Content Hub
role: User
exl-id: f1be7cfc-1803-4c17-bb58-947104aa883c
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 17%

---

# Caricare risorse approvate dal brand in Content Hub {#upload-brand-approved-assets-content-hub}

>[!CONTEXTUALHELP]
>id="upload_assets_content_hub"
>title="Caricare risorse approvate dal brand in Content Hub"
>abstract="Aggiungi risorse approvate a Content Hub dal file system locale o importa risorse di origini di dati da OneDrive o di Dropbox. Tutte le risorse vengono visualizzate al livello superiore in Content Hub, indipendentemente dalla struttura della cartella, per migliorare le funzionalità di ricerca."

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza l’Assistente IA di Adobe Acrobat per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub - PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

[Gli utenti di Content Hub con i diritti per aggiungere risorse](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) possono aggiungere risorse a Content Hub dal file system locale o importare risorse da origini dati OneDrive o Dropbox. Tutte le risorse vengono visualizzate al livello superiore in Content Hub, indipendentemente dalla struttura di cartelle disponibile nel file system locale o dalle origini dati di OneDrive e Dropbox, per migliorare le funzionalità di ricerca.

Le risorse contrassegnate come `Approved` in Assets as a Cloud Service sono automaticamente disponibili in Content Hub. Per ulteriori informazioni, consulta [Approvare le risorse per Content Hub](/help/assets/approve-assets-content-hub.md).

Per migliorare ulteriormente la ricerca delle risorse, Content Hub consente di:

* Definisci i dettagli chiave rilevanti per il caricamento delle risorse, ad esempio il nome della campagna, le parole chiave, i canali e così via.

* Genera automaticamente più proprietà per ogni risorsa al momento del caricamento, ad esempio dimensione del file, formato, risoluzione e altre proprietà.

* Utilizza l&#39;intelligenza artificiale fornita da [Adobe Sensei](https://www.adobe.com/it/sensei.html) per applicare automaticamente tag rilevanti a tutte le risorse caricate. Questi tag, o tag avanzati, consentono di velocizzare le attività relative ai contenuti dei progetti grazie alla possibilità di trovare rapidamente le risorse rilevanti.

Assicurati di caricare solo le risorse approvate dal marchio [ in Content Hub](/help/assets/approve-assets.md).

![Carica risorse approvate dal marchio](assets/upload-brand-approved-assets.png)

## Prerequisiti {#prerequisites-add-assets}

[Gli utenti di Content Hub con i diritti per aggiungere risorse](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) possono caricare risorse in Content Hub.

## Aggiungere risorse a Content Hub dal file system locale {#add-assets-local-file-system}

Per aggiungere risorse a Content Hub, effettua le seguenti operazioni:

1. Fai clic su **[!UICONTROL Aggiungi Assets]** per visualizzare la finestra di dialogo **[!UICONTROL Aggiungi risorse approvate]** che consente di creare e caricare.

1. Nella sezione **[!UICONTROL Trascina qui i file o le cartelle]** disponibile nel riquadro di destra, puoi trascinare le risorse dal file system locale oppure fare clic su **[!UICONTROL Sfoglia]** per selezionare manualmente i file o le cartelle disponibili nel file system locale. Questo elenco di file che fanno parte del caricamento è disponibile come elenco.


   È inoltre possibile visualizzare in anteprima le immagini selezionate utilizzando le miniature e fare clic sull&#39;icona X per rimuovere una particolare immagine dall&#39;elenco. L’icona X viene visualizzata solo quando passi il cursore del mouse sul nome o sulle dimensioni dell’immagine. Puoi anche fare clic su **[!UICONTROL Rimuovi tutti]** per eliminare tutti gli elementi dall&#39;elenco di caricamento.

   Per completare il processo di caricamento e abilitare il pulsante **[!UICONTROL Carica]**, è necessario raggruppare le risorse sotto un nome di campagna.

   ![Carica risorse in Content Hub](assets/upload-assets-content-hub.png)

1. Definisci il nome per il caricamento utilizzando il campo **[!UICONTROL Nome campagna]**. Puoi usare un nome esistente o crearne uno nuovo. Il Content Hub offre più opzioni quando si digita il nome. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Come best practice, Adobe consiglia di specificare i valori negli altri campi e di migliorare l’esperienza di ricerca delle risorse caricate.

1. Definisci allo stesso modo i valori per i campi **[!UICONTROL Parole chiave]**, **[!UICONTROL Canali]**, **[!UICONTROL Intervallo temporale]** e **[!UICONTROL Area]**. Assegnare tag e raggruppare le risorse per parole chiave, canali e posizione consente a tutti coloro che utilizzano il contenuto aziendale approvato di trovare tali risorse e mantenerle organizzate.

1. Fai clic su **[!UICONTROL Carica]** per caricare le risorse in Content Hub. [!UICONTROL Visualizza dettagli] viene visualizzata la casella di conferma. Fai clic su [!UICONTROL Continua].

1. Avvia il caricamento di Assets. Fai clic su [!UICONTROL Nuovo caricamento] per riavviare la procedura di caricamento. Fai clic su [!UICONTROL Fine] per completare il caricamento.

Gli amministratori possono anche configurare i campi obbligatori e facoltativi da visualizzare durante il caricamento delle risorse, ad esempio il nome della campagna, le parole chiave, i canali e così via. Per ulteriori informazioni, vedere [Configurare l&#39;interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## Aggiungere risorse a Content Hub da origini dati OneDrive o Dropbox {#add-assets-onedrive-dropbox}

Per aggiungere risorse a Content Hub da origini dati OneDrive o Dropbox:

1. Fai clic su **[!UICONTROL Aggiungi Assets]** per visualizzare la finestra di dialogo **[!UICONTROL Aggiungi risorse approvate]** che consente di importare risorse da OneDrive o Dropbox.

1. Fai clic su **[!UICONTROL OneDrive]** o **[!UICONTROL Dropbox]** per avviare il processo di importazione. Content Hub richiede di accedere all&#39;account OneDrive o Dropbox e quindi visualizza la struttura delle cartelle di OneDrive o Dropbox nel riquadro a sinistra.

1. Fai clic sull’icona + accanto al file o al nome della cartella per visualizzare l’elemento nell’elenco Elementi selezionati. Dopo aver selezionato tutti i file da aggiungere al portale Content Hub, ripetere i passaggi da 3 a 6 di [Aggiungi risorse a Content Hub dal file system locale](#add-assets-local-file-system) per completare il processo di caricamento.

   ![Carica risorse in Content Hub da OneDrive o Dropbox](assets/add-assets-onedrive-dropbox.png)

Gli amministratori possono anche configurare i campi obbligatori e facoltativi da visualizzare durante il caricamento delle risorse, ad esempio il nome della campagna, le parole chiave, i canali e così via. Per ulteriori informazioni, vedere [Configurare l&#39;interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

## Gestire le risorse caricate tramite Content Hub {#manage-assets-uploaded-using-content-hub}

[Gli utenti di Content Hub con diritti di aggiunta risorse](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) possono [aggiungere risorse a Content Hub](/help/assets/upload-brand-approved-assets.md) dal file system locale o importare risorse da origini dati OneDrive o Dropbox. Tutte le risorse vengono visualizzate al livello superiore in Content Hub, indipendentemente dalla struttura di cartelle disponibile nel file system locale o dalle origini dati di OneDrive e Dropbox, per migliorare le funzionalità di ricerca.

La visualizzazione delle risorse caricate tramite Content Hub dipende dal fatto che sia stato abilitato [l&#39;interruttore di approvazione automatica](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Se il pulsante **[!UICONTROL Approvazione automatica]** è attivato, le risorse caricate tramite Content Hub sono automaticamente disponibili.

* Se il pulsante **[!UICONTROL Approvazione automatica]** è disattivato, le risorse caricate tramite Content Hub non vengono visualizzate automaticamente. Le risorse sono disponibili nella cartella `hydrated-assets` dell’ambiente Assets as a Cloud Service. Passa alla cartella e [modifica in blocco](#bulk-approve-assets-content-hub) lo stato di tali risorse in `Approved` per consentirne la visualizzazione in Content Hub.

![Processo di approvazione Content Hub](/help/assets/assets/content-hub-approval.png)
