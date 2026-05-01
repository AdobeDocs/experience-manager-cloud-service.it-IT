---
title: Applicare ritagli avanzati video ai video approvati
description: Dynamic Media con funzionalità OpenAPI consente di generare automaticamente output Video Smart Cropped per risorse video approvate in Adobe Experience Manager (AEM).
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Si applica ad AEM Assets)."
exl-id: video-smartcrop-dmwoapi
source-git-commit: 8ddd2ade491069e4592becf3b77c04e6bbb2c06a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---


# Applicare ritagli avanzati video ai video approvati {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities] consente di generare automaticamente output di ritaglio avanzato video per risorse video in [!DNL Adobe Experience Manager (AEM)]. I ritagli avanzati video analizzano il contenuto video e regolano dinamicamente l’inquadratura per mantenere l’oggetto chiave visibile tra diversi rapporti di aspetto e dispositivi.

I ritagli avanzati video vengono generati automaticamente quando la funzione è abilitata e la risorsa video viene approvata

## Prima di iniziare {#prerequisites-for-video-smart-crops}

Assicurati di disporre di:

* Accesso a [!DNL AEM Assets as a Cloud Service].
* Autorizzazione per la modifica degli schemi di metadati.
* Dynamic Media con funzionalità OpenAPI abilitate per il tuo ambiente.
* Risorse video contrassegnate come **[!UICONTROL Approvate]**.

## Abilita ritagli avanzati video per video {#enable-video-smart-crops}

Per abilitare i ritagli avanzati video, configura lo schema metadati utilizzato per le risorse video:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
2. Apri lo schema metadati applicabile (ad esempio, **default**).
3. Seleziona il modulo **Video** e fai clic su **[!UICONTROL Modifica]**.
4. Aggiungi un nuovo **[!UICONTROL campo a discesa]** e configura quanto segue:

   * **Etichetta Campo**: Crea Smartcrop Video
   * **Mappa sulla proprietà**: `./jcr:content/dam:applyVideoSmartCrop`

5. Aggiungi manualmente i seguenti valori:

   * Sì → vero
   * Nessuna → false

6. Salva lo schema.

L&#39;opzione **Crea smartcrop video** è ora disponibile nel modulo dei metadati delle risorse video.

![Crea campo Smartcrop video](/help/assets/assets/video-smartcrop-metadata-field.png)

## Applicare ritagli avanzati video ai video approvati {#apply-video-smart-crops}

Per applicare ritagli video avanzati alle risorse video, abilita il campo metadati e approva la risorsa.

Esegui i passaggi seguenti:

1. In [!DNL Assets View], seleziona **[!UICONTROL Assets]** e passa alla cartella.
2. Seleziona la risorsa video.
3. Fare clic su **[!UICONTROL Dettagli]**.
4. Nel pannello metadati, individua **[!UICONTROL Crea ritagli smart video]**.
5. Imposta il valore su **Sì**, quindi fai clic su **[!UICONTROL Salva]**.
6. Imposta lo stato della risorsa su **[!UICONTROL Approvato]**.

Una volta approvata la risorsa, gli output Video Smart Cropped vengono generati automaticamente.

## Visualizzare gli output ritagliati con ritaglio avanzato video {#view-video-smart-crops}

Una volta generati i ritagli avanzati video:

* Le uscite sono disponibili durante la riproduzione del video.
* Il visualizzatore Dynamic Media seleziona automaticamente il ritaglio più appropriato in base al dispositivo e alle proporzioni.
* La riproduzione del video viene regolata dinamicamente per mantenere il soggetto chiave a fuoco.

## Usare video ritagliati con ritagli avanzati {#use-video-smart-crops}

Puoi utilizzare gli output Ritagliati video avanzati ovunque venga distribuita la risorsa video, ad esempio:

* Pagine web
* Applicazioni
* Lettori video incorporati

Il visualizzatore applica automaticamente il ritaglio avanzato appropriato durante la riproduzione.

>[!NOTE]
>
>* I ritagli avanzati video vengono generati solo per **risorse video approvate**.
>* Prima di approvare la risorsa, assicurati che il campo **Create Video Smartcrop** sia impostato su **Yes**.
>* I ritagli avanzati video non modificano la risorsa originale. Il ritaglio viene applicato in modo dinamico durante la riproduzione.