---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: come inviare un’e-mail per un modulo adattivo, Azione di invio e-mail, E-mail modulo adattivo, E-mail di invio modulo, Guida all’invio e-mail
feature: Adaptive Forms, Core Components
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: Come si configura un’azione di invio per un modulo adattivo?
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 3%

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
* Consente di semplificare il flusso di lavoro integrando direttamente l’invio dei moduli nelle notifiche e-mail.
* Aiuta le organizzazioni a personalizzare il contenuto delle e-mail, adattandolo quindi a specifiche esigenze di comunicazione.

## Configurare l’azione di invio dell’e-mail di invio {#steps-to-configure-send-email-submit-action}

Per configurare l’azione di invio:

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

## Best practice {#best-practices}

* Si consiglia di mantenere il contenuto dell’e-mail chiaro e conciso. Gli utenti devono comprendere lo scopo dell’e-mail e tutte le azioni da intraprendere.
* Si consiglia di assegnare nomi elementi univoci a tutti i campi modulo, anche se sono posizionati in pannelli diversi all’interno di un modulo adattivo.
* Quando si utilizza AEM as a Cloud Service, i messaggi e-mail in uscita richiedono la crittografia. Per impostazione predefinita, la funzionalità e-mail in uscita è disabilitata. Per attivarlo, invia un ticket di supporto a [richiedi l&#39;accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=it#sending-email).


## Articoli correlati

{{af-submit-action}}
