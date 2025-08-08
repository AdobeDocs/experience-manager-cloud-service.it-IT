---
description: Esplora il processo per impostare le notifiche e-mail durante l’invio di un modulo adattivo.
keywords: come inviare un’e-mail per un modulo adattivo, Azione di invio e-mail, E-mail modulo adattivo, E-mail di invio modulo, Guida all’invio e-mail
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 7%

---

# Configurare l’azione di invio Invia e-mail per un modulo adattivo

L&#39;azione di invio **[!UICONTROL Invia e-mail]** consente di inviare un messaggio e-mail a uno o più destinatari dopo l&#39;invio del modulo. Questa azione di invio consente di creare un messaggio e-mail che può includere i dati del modulo in un formato predefinito. Ad esempio, considera il seguente modello in cui il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviato:


    &quot;
    Ciao ${customer_Name},
    
    L&#39;indirizzo di spedizione predefinito è:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Cordiali saluti,
    WKND
    &quot;

## Vantaggi

Alcuni vantaggi della configurazione di un modulo adattivo con l’azione di invio Invia e-mail sono:

* Consente una comunicazione rapida in quanto i dati del modulo vengono inviati direttamente ai destinatari e-mail designati.
* Flusso di lavoro più semplice, integrando direttamente l’invio dei moduli nelle notifiche e-mail.
* Personalizzazione del contenuto delle e-mail agevolata, adatta a specifiche esigenze di comunicazione.

>[!BEGINTABS]

>[!TAB Componente di base]

Per configurare un’azione di invio Invia e-mail per il componente di base:

1. Apri il modulo adattivo per la modifica e passa alla sezione **[!UICONTROL Invio]** delle proprietà Contenitore modulo adattivo.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Invia e-mail]**.

   ![Configurazione azione di Invia e-mail](/help/forms/assets/send-email-fc.png)

1. Specifica l&#39;ID e-mail del mittente nella casella di testo **[!UICONTROL Da]**.
1. Aggiungi l&#39;ID e-mail del destinatario nella casella di testo **[!UICONTROL A]**. Per aggiungere più destinatari, fare clic sul pulsante **[!UICONTROL Aggiungi]**.
1. [Facoltativo] Aggiungere il destinatario per CC e Ccn facendo clic sul pulsante **[!UICONTROL Aggiungi]**.
1. Specificare un oggetto nella casella di testo **[!UICONTROL Oggetto]**.
1. Aggiungi un modello e-mail per configurare l’azione di invio dell’e-mail.
   * Puoi specificare il percorso del modello e-mail esterno salvato nelle risorse AEM utilizzando l&#39;opzione **[!UICONTROL Percorso modello esterno]**.
   * Puoi anche aggiungere un modello e-mail personalizzato per l&#39;invio del modulo nella casella di testo **[!UICONTROL Modello e-mail]**.
1. [Facoltativo] L&#39;azione di invio **[!UICONTROL Invia e-mail]** consente di includere allegati e un [documento di record (DoR)](generate-document-of-record-core-components.md) con l&#39;e-mail.
1. Fai clic su **[!UICONTROL Fine]**.

>[!TAB Componente core]

Per configurare l’azione di invio Invia e-mail per il componente core:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Invia azione]**, selezionare **[!UICONTROL Invia e-mail]**.

   ![Configurazione azione di Invia e-mail](/help/forms/assets/send-email-action-configuration.gif)
1. Specifica l&#39;ID e-mail del mittente nella casella di testo **[!UICONTROL Da]**.
1. Aggiungi l&#39;ID e-mail del destinatario nella casella di testo **[!UICONTROL A]**. Per aggiungere più destinatari, fare clic sul pulsante **[!UICONTROL Aggiungi]**.
1. [Facoltativo] Aggiungere il destinatario per CC e Ccn facendo clic sul pulsante **[!UICONTROL Aggiungi]**.
1. Specificare un oggetto nella casella di testo **[!UICONTROL Oggetto]**.
1. Aggiungi un modello e-mail per configurare l’azione di invio dell’e-mail.
   * Puoi specificare il percorso del modello e-mail esterno salvato nelle risorse AEM utilizzando l&#39;opzione **[!UICONTROL Percorso modello esterno]**.
   * Puoi anche aggiungere un modello e-mail personalizzato per l&#39;invio del modulo nella casella di testo **[!UICONTROL Modello e-mail]**.
1. [Facoltativo] L&#39;azione di invio **[!UICONTROL Invia e-mail]** consente di includere allegati e un [documento di record (DoR)](generate-document-of-record-core-components.md) con l&#39;e-mail.
1. Fai clic su **[!UICONTROL Fine]**.

>[!TAB Editor universale]

Per configurare l’azione Invia e-mail in Universal Editor:

1. Apri il modulo adattivo per la modifica.
1. Fai clic sull&#39;estensione **Modifica proprietà modulo** nell&#39;editor.
Viene visualizzata la finestra di dialogo **Proprietà modulo**.

   >[!NOTE]
   >
   > * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
   > * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).


1. Fai clic sulla scheda **Invio** e seleziona **[!UICONTROL Invia e-mail]** azione di invio.

   ![Invia e-mail all&#39;editor universale](/help/forms/assets/send-email-ue.png)

1. Specifica l&#39;ID e-mail del mittente nella casella di testo **[!UICONTROL Da]**.
1. Aggiungi l&#39;ID e-mail del destinatario nella casella di testo **[!UICONTROL A]**. Per aggiungere più destinatari, fare clic sul pulsante **[!UICONTROL Aggiungi]**.
1. [Facoltativo] Aggiungere il destinatario per CC e Ccn facendo clic sul pulsante **[!UICONTROL Aggiungi]**.
1. Specificare un oggetto nella casella di testo **[!UICONTROL Oggetto]**.
1. Aggiungi un modello e-mail per configurare l’azione di invio dell’e-mail.
   * Puoi specificare il percorso del modello e-mail esterno salvato nelle risorse AEM utilizzando l&#39;opzione **[!UICONTROL Percorso modello esterno]**.
   * Puoi anche aggiungere un modello e-mail personalizzato per l&#39;invio del modulo nella casella di testo **[!UICONTROL Modello e-mail]**.
1. [Facoltativo] L&#39;azione di invio **[!UICONTROL Invia e-mail]** consente di includere allegati e un [documento di record (DoR)](generate-document-of-record-core-components.md) con l&#39;e-mail.
1. Fai clic su **[!UICONTROL Salva&amp;Chiudi]**.

>[!ENDTABS]

## Best practice {#best-practices}

* Si consiglia di mantenere il contenuto dell’e-mail chiaro e conciso. Gli utenti devono comprendere lo scopo dell’e-mail e tutte le azioni da intraprendere.
* Si consiglia di assegnare nomi elementi univoci a tutti i campi modulo, anche se sono posizionati in pannelli diversi all’interno di un modulo adattivo.
* Quando si utilizza AEM as a Cloud Service, i messaggi e-mail in uscita richiedono la crittografia. Per impostazione predefinita, la funzionalità e-mail in uscita è disabilitata. Per attivarlo, invia un ticket di supporto a [richiedi l&#39;accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

## Articoli correlati

{{af-submit-action}}
