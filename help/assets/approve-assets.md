---
title: Approvare le risorse in Experience Manager
description: Scopri come approvare le risorse in [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# Approvare le risorse in [!DNL Experience Manager]

I Brand Manager e gli addetti al marketing mantengono un controllo rigoroso sulle risorse del brand. È disponibile per l’uso solo la versione approvata e più recente della risorsa, che garantisce la coerenza del brand su tutti i canali e le applicazioni.

Puoi approvare le risorse in AEM Assets per semplificare la gestione delle risorse, garantendo un processo controllato ed efficiente per la loro gestione.

## Prima di iniziare {#pre-requisites}

Devi avere accesso ad AEM Assets as a Cloud Service e alle autorizzazioni per modificare **[!UICONTROL Stato revisione]** per una risorsa.

## Configurazione

Prima di approvare una risorsa, devi effettuare un aggiornamento una tantum dello schema di metadati applicabile nella visualizzazione Amministratore. Puoi saltare questa configurazione per la vista Assets. Per configurare lo schema metadati, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona lo schema metadati applicabile e fai clic su **[!UICONTROL Modifica]**. <br>Il **[!UICONTROL Editor modulo schema metadati]** si apre con **[!UICONTROL Base]** scheda evidenziata.
1. Scorri verso il basso e fai clic su **[!UICONTROL Stato revisione]**.
1. Fai clic su **[!UICONTROL Regole]** sul pannello laterale destro.
1. Deseleziona **[!UICONTROL Disattiva modifica]** e fai clic su **[!UICONTROL Salva]**.
Se è necessario visualizzare la proprietà che **[!UICONTROL Stato revisione]** è mappato a, passa a **[!UICONTROL Impostazioni]** e visualizzare `./jcr:content/metadata/dam:status` valore in **[!UICONTROL Mappa su proprietà]** campo.

>[!NOTE]
>
>Se le risorse o le cartelle hanno uno schema predefinito diverso, assicurati di effettuare questo aggiornamento in quello specifico schema.

## Approvare le risorse {#approve-assets}

Puoi approvare le risorse in entrambi [!DNL Experience Manager] e [!DNL Experience Manager Assets]. Per approvare le risorse in [!DNL Experience Manager], effettua le seguenti operazioni:

1. Seleziona le risorse e fai clic su **[!UICONTROL Proprietà]** nel riquadro superiore.
1. In **[!UICONTROL Base]** , scorri verso il basso fino a **[!UICONTROL Stato revisione]**.
1. Modifica lo stato della revisione in **[!UICONTROL Approvato]**.
   ![immagine](/help/assets/assets/approve-old-ui.png)
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   Allo stesso modo, puoi approvare le risorse utilizzando [nuova vista Assets](/help/assets/manage-organize-assets-view.md).

## Approva in blocco le risorse {#bulk-approve-assets}

Semplifica il flusso di lavoro approvando rapidamente più risorse contemporaneamente. Puoi approvare in blocco le risorse per accelerare il processo di approvazione, risparmiando tempo e migliorando la produttività.
<br>Segui questi passaggi per approvare risorse in blocco in [!DNL Experience Manager]:

1. Crea una cartella nell’ambiente di authoring (https://author-pXXX-eYYY.adobeaemcloud.com). Sostituisci _XXX_ con il tuo ID programma e _AAAA_ con l’ID ambiente dell’Experience Manager.
1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Profili metadati]**.
1. Clic **[!UICONTROL Crea]** in alto a destra.
1. Aggiungi un titolo profilo e fai clic su **[!UICONTROL Crea]**. Il profilo metadati è stato creato correttamente.
1. Seleziona il nuovo profilo di metadati creato e fai clic su **[!UICONTROL Modifica _e)_]**. <br>Il **[!UICONTROL Modifica profilo metadati]**viene aperto un modulo con **[!UICONTROL Base]**scheda evidenziata.
1. Trascina una **[!UICONTROL Campo di testo a riga singola]** dal **[!UICONTROL Genera modulo]** sezione a destra della sezione Metadati nel modulo.
1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel **[!UICONTROL Impostazioni]** pannello:
   1. Modificare il **[!UICONTROL Etichetta campo]** a _Assets approvato_.
   1. Aggiornare il **[!UICONTROL Mappa su proprietà]** a _./jcr:content/metadata/dam:status_.
   1. Modifica il valore predefinito in _approvato_.

1. Fai clic su **[!UICONTROL Salva]**.
1. In **[!UICONTROL Profili metadati]** , selezionare il profilo metadati appena creato.
1. Clic **[!UICONTROL Applica profilo metadati a cartelle]** dalla barra delle azioni superiore.
1. Seleziona le cartelle da approvare e fai clic su **[!UICONTROL Applica]**.
   <br> L’autorizzazione per l’intera cartella viene impostata per l’approvazione e tutte le risorse caricate in questa cartella vengono approvate automaticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Questo approccio approva le nuove risorse create nella cartella. Per le risorse esistenti nella cartella, devi selezionarle e approvarle manualmente. <br> In alternativa, è possibile utilizzare **[!UICONTROL Rielabora]** per applicare le modifiche dal profilo metadati alle risorse precedenti.

Allo stesso modo, per approvare in blocco le risorse all’interno di una cartella nella vista Assets:

1. Seleziona le risorse e fai clic su **[!UICONTROL Modifica in blocco dei metadati]**.

1. Seleziona **[!UICONTROL Approvato]** nel **[!UICONTROL Stato]** campo disponibile nel [!UICONTROL Proprietà] nel riquadro di destra.

1. Fai clic su **[!UICONTROL Salva]**.

## Copiare l’URL di consegna per le risorse approvate {#copy-delivery-url-approved-assets}

L’URL di consegna per tutte le risorse approvate nell’archivio è disponibile se disponi di [!UICONTROL Dynamic Medie con funzionalità OpenAPI] nell’istanza di AEM as a Cloud Service.

Per copiare l’URL di consegna di una risorsa approvata all’interno dell’archivio:

1. Seleziona la risorsa e fai clic su **[!UICONTROL Dettagli]**.

1. Fai clic sull’icona Rappresentazioni disponibile nel riquadro a destra.

1. Seleziona **[!UICONTROL Dynamic Medie con OpenAPI]** disponibile in **[!UICONTROL Dinamico]** sezione.

1. Clic **[!UICONTROL Copia URL]** per copiare l’URL di consegna della risorsa.
   ![copia URL di consegna](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >L’opzione per copiare l’URL di consegna per le risorse approvate è disponibile nella vista Assets.

