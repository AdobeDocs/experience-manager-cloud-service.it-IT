---
title: Approvare le risorse in Experience Manager
description: Scopri come approvare le risorse in [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---

# Approvare le risorse in [!DNL Experience Manager]

I Brand Manager e gli addetti al marketing mantengono un controllo rigoroso sulle risorse del brand. È disponibile per l’uso solo la versione approvata e più recente della risorsa, che garantisce la coerenza del brand su tutti i canali e le applicazioni.

Puoi approvare le risorse in AEM Assets per semplificare la gestione delle risorse, garantendo un processo controllato ed efficiente per la loro gestione.

## Prima di iniziare {#pre-requisites}

Devi avere accesso ad AEM Assets as a Cloud Service e alle autorizzazioni per modificare **[!UICONTROL Stato revisione]** per una risorsa.

## Configurazione

È necessario effettuare un aggiornamento una tantum allo schema metadati applicabile nella sezione [!DNL Experience Manager] prima di poter approvare una risorsa. Puoi saltare questa configurazione per [!DNL Experience Manager Assets]. Per configurare lo schema metadati, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona lo schema metadati applicabile e fai clic su **[!UICONTROL Modifica]**. <br>Il **[!UICONTROL Editor modulo schema metadati]** si apre con **[!UICONTROL Base]** scheda evidenziata.
1. Scorri verso il basso e fai clic su **[!UICONTROL Stato revisione]**.
1. Fai clic su **[!UICONTROL Regole]** sul pannello laterale destro.
1. Deseleziona **[!UICONTROL Disattiva modifica]** e fai clic su **[!UICONTROL Salva]**.

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

   Allo stesso modo, puoi approvare le risorse utilizzando [nuova vista Risorse](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-organize.html?lang=en#manage-asset-status).

## Approva in blocco le risorse {#bulk-approve-assets}

Semplifica il flusso di lavoro approvando rapidamente più risorse contemporaneamente. Puoi approvare in blocco le risorse per accelerare il processo di approvazione, risparmiando tempo e migliorando la produttività.
<br>Segui questi passaggi per approvare risorse in blocco in [!DNL Experience Manager]:

1. Crea una cartella nell’ambiente di authoring (https://author-pXXX-eYYY.adobeaemcloud.com). Sostituisci _XXX_ con il tuo ID programma e _AAAA_ con l’ID ambiente dell’Experience Manager.
1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]**.
1. Clic **[!UICONTROL Crea]** in alto a destra.
1. Aggiungi un titolo profilo e fai clic su **[!UICONTROL Crea]**. Il profilo metadati è stato creato correttamente.
1. Seleziona il nuovo profilo di metadati creato e fai clic su **[!UICONTROL Modifica _e)_]**. <br>Il **[!UICONTROL Modifica profilo metadati]**viene aperto un modulo con **[!UICONTROL Base]**scheda evidenziata.
1. Trascina una **[!UICONTROL Campo di testo a riga singola]** dal **[!UICONTROL Genera modulo]** sezione a destra della sezione Metadati nel modulo.
1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel **[!UICONTROL Impostazioni]** pannello:
   1. Modificare il **[!UICONTROL Etichetta campo]** a _Risorse approvate_.
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
