---
title: Carica le risorse approvate dal tuo marchio in [!DNL Content Hub]
description: Scopri come caricare le risorse approvate dal marchio in Content Hub
role: User
source-git-commit: c85b4e1c828ed1fb7f4063f965fe116215ca0244
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Caricare risorse approvate dal marchio in Content Hub {#upload-brand-approved-assets-content-hub}

[Gli utenti di Content Hub con i diritti per aggiungere risorse](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) possono aggiungere risorse a Content Hub dal file system locale o importare risorse da OneDrive o da origini dati di Dropbox. Tutte le risorse vengono visualizzate al livello superiore in Content Hub, indipendentemente dalla struttura di cartelle disponibile nel file system locale o nelle origini dati di OneDrive e di Dropbox, per migliorare le funzionalità di ricerca.

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

   Come best practice, l’Adobe consiglia di specificare i valori negli altri campi e di migliorare l’esperienza di ricerca delle risorse caricate.

1. Definisci allo stesso modo i valori per i campi **[!UICONTROL Parole chiave]**, **[!UICONTROL Canali]**, **[!UICONTROL Intervallo temporale]** e **[!UICONTROL Area]**. Assegnare tag e raggruppare le risorse per parole chiave, canali e posizione consente a tutti coloro che utilizzano il contenuto aziendale approvato di trovare tali risorse e mantenerle organizzate.

1. Fai clic su **[!UICONTROL Carica]** per caricare le risorse in Content Hub. [!UICONTROL Visualizza dettagli] viene visualizzata la casella di conferma. Fai clic su [!UICONTROL Continua].

1. Avvia il caricamento di Assets. Fai clic su [!UICONTROL Nuovo caricamento] per riavviare la procedura di caricamento. Fai clic su [!UICONTROL Fine] per completare il caricamento.

Gli amministratori possono anche configurare i campi obbligatori e facoltativi da visualizzare durante il caricamento delle risorse, ad esempio il nome della campagna, le parole chiave, i canali e così via. Per ulteriori informazioni, vedere [Configurare l&#39;interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## Aggiungere risorse a Content Hub da origini dati OneDrive o di Dropbox {#add-assets-onedrive-dropbox}

Per aggiungere risorse a Content Hub da origini dati OneDrive o Dropbox:

1. Fai clic su **[!UICONTROL Aggiungi Assets]** per visualizzare la finestra di dialogo **[!UICONTROL Aggiungi risorse approvate]** che consente di importare risorse da OneDrive o dal Dropbox.

1. Fai clic su **[!UICONTROL OneDrive]** o **[!UICONTROL Dropbox]** per avviare il processo di importazione. Content Hub richiede di accedere all&#39;account di OneDrive o di Dropbox e quindi visualizza la struttura delle cartelle di OneDrive o di Dropbox nel riquadro a sinistra.

1. Fai clic sull’icona + accanto al file o al nome della cartella per visualizzare l’elemento nell’elenco Elementi selezionati. Dopo aver selezionato tutti i file da aggiungere al portale Content Hub, ripetere i passaggi da 3 a 6 di [Aggiungi risorse a Content Hub dal file system locale](#add-assets-local-file-system) per completare il processo di caricamento.

   ![Carica risorse in Content Hub da OneDrive o Dropbox](assets/add-assets-onedrive-dropbox.png)

Gli amministratori possono anche configurare i campi obbligatori e facoltativi da visualizzare durante il caricamento delle risorse, ad esempio il nome della campagna, le parole chiave, i canali e così via. Per ulteriori informazioni, vedere [Configurare l&#39;interfaccia utente di Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

