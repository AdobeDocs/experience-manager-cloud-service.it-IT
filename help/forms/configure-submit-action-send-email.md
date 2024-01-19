---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: come inviare un’e-mail per un modulo adattivo, Azione di invio e-mail, E-mail modulo adattivo, E-mail di invio modulo, Guida all’invio e-mail
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Configurare l’azione di invio Invia e-mail per un modulo adattivo

Il **[!UICONTROL Invia e-mail]** Azione di invio consente di inviare un messaggio e-mail a uno o più destinatari dopo l’invio corretto del modulo. Questa azione di invio consente di creare un messaggio e-mail che può includere i dati del modulo in un formato predefinito. Ad esempio, considera il seguente modello in cui il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviato:


    &quot;
    Ciao ${customer_Name},
    
    Di seguito è riportato l&#39;indirizzo di spedizione predefinito:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Cordiali saluti
    WKND
    
    &quot;


## Vantaggi

Alcuni vantaggi della configurazione di un modulo adattivo con l’azione di invio Invia e-mail sono:

* Consente una comunicazione rapida in quanto i dati del modulo vengono inviati direttamente ai destinatari e-mail designati.
* Consente di semplificare il flusso di lavoro integrando direttamente l’invio dei moduli nelle notifiche e-mail.
* Aiuta le organizzazioni a personalizzare il contenuto delle e-mail, adattandolo quindi a specifiche esigenze di comunicazione.

## Configurare l’azione di invio dell’e-mail di invio {#steps-to-configure-send-email-submit-action}

Per configurare l’azione di invio:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic su  **[!UICONTROL Invio]** scheda.
1. Dalla sezione **[!UICONTROL Azione di invio]** elenco a discesa, seleziona **[!UICONTROL Invia e-mail]**.

   ![Configurazione dell’azione Invia e-mail](/help/forms/assets/send-email-action-configuration.gif)
1. Specifica l&#39;ID e-mail del mittente in **[!UICONTROL Da]** casella di testo.
1. Aggiungi l’ID e-mail del destinatario in **[!UICONTROL A]** casella di testo. Puoi aggiungere più destinatari facendo clic sul pulsante **[!UICONTROL Aggiungi]** pulsante.
1. [Facoltativo] Aggiungere il destinatario per CC e Ccn facendo clic sul pulsante **[!UICONTROL Aggiungi]** pulsante.
1. Specifica un oggetto nella **[!UICONTROL Oggetto]** casella di testo.
1. Aggiungi un modello e-mail per configurare l’azione di invio dell’e-mail.
   * Puoi specificare il percorso del modello e-mail esterno salvato nelle risorse AEM utilizzando **[!UICONTROL Percorso modello esterno]** opzione.
   * Puoi anche aggiungere un modello e-mail personalizzato per l’invio del modulo nel **[!UICONTROL Modello e-mail]** casella di testo.
1. [Facoltativo] Il **[!UICONTROL Invia e-mail]** L&#39;azione di invio fornisce l&#39;opzione per includere allegati e un [Documento record (DoR)](generate-document-of-record-core-components.md) con l’e-mail.
1. Clic **[!UICONTROL Fine]**.

## Best practice {#best-practices}

* Si consiglia di mantenere il contenuto dell’e-mail chiaro e conciso. Gli utenti devono comprendere lo scopo dell’e-mail e tutte le azioni da intraprendere.
* Si consiglia di assegnare nomi elementi univoci a tutti i campi modulo, anche se sono posizionati in pannelli diversi all’interno di un modulo adattivo.
* Quando si utilizza AEM as a Cloud Service, i messaggi e-mail in uscita richiedono la crittografia. Per impostazione predefinita, la funzionalità e-mail in uscita è disabilitata. Per attivarlo, invia un ticket di supporto a [richiedi accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


## Articoli correlati

{{af-submit-action}}


