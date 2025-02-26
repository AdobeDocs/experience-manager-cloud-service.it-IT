---
title: Azioni di invio
description: Configurare le azioni di invio per il modulo adattivo.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 3%

---

# Azione di invio modulo adattivo

Un’azione di invio specifica la destinazione dei dati raccolti tramite un modulo adattivo. Il processo di invio inizia quando l&#39;utente fa clic sul pulsante **[!UICONTROL Invia]** nel modulo. AEM Forms offre due tipi di azioni di invio descritte di seguito e consente di creare e utilizzare azioni di invio personalizzate per soddisfare esigenze specifiche. Le azioni di invio predefinite sono:

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [Invia all’endpoint REST](#rest-endpoint-submission-ue)
* [Invia e-mail](#email-submission-ue)


### Invia all’endpoint REST {#rest-endpoint-submission-ue}

L’azione Invia a endpoint REST viene utilizzata per inviare i dati del modulo inviati a un endpoint REST specificato. L’endpoint può appartenere a un server interno in cui il modulo è ospitato o a un server esterno utilizzando un percorso relativo o un percorso assoluto. Per inviare i dati al server AEM che ospita il modulo, utilizza un percorso relativo corrispondente al percorso principale del server AEM. Ad esempio, `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizzare il percorso assoluto.

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



Per configurare un endpoint REST:

1. Apri il modulo adattivo in **[!UICONTROL Editor]**.
1. Seleziona **[!UICONTROL Blocco modulo adattivo]**.
1. Fai clic sull&#39;icona delle proprietà ![proprietà](/help/forms/assets/Smock_Properties_18_N.svg).
1. Selezionare **[!UICONTROL Invia a un endpoint REST]** dall&#39;elenco a discesa **[!UICONTROL Azione di invio]**.
1. Specifica l’URL dell’endpoint REST.
1. Puoi anche **abilitare la richiesta POST** e fornire un URL per pubblicare la richiesta.

![Abilita richiesta post per moduli adattivi](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * Per pubblicare i dati su un server interno, specifica il percorso della risorsa. I dati vengono inseriti nel percorso della risorsa. Ad esempio, `/content/restEndPoint`. Per tali richieste successive, vengono utilizzate le informazioni di autenticazione della richiesta di invio.
> * Per pubblicare dati su un server esterno, fornisci un URL. Il formato dell&#39;URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

### Invia e-mail {#email-submission-ue}

Invia azione di invio e-mail consente di inviare un messaggio e-mail a uno o più destinatari in seguito all’invio corretto del modulo. La configurazione Invia e-mail consente di creare un messaggio e-mail che può includere i dati del modulo in un formato predefinito. Ad esempio, considera il seguente modello in cui il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviato. [Ulteriori informazioni sui modelli e-mail in Forms adattivo](/help/forms/html-email-templates-in-adaptive-forms.md). Alcuni vantaggi della configurazione di un modulo adattivo con l’azione di invio Invia e-mail sono:

1. Consente una comunicazione rapida in quanto i dati del modulo vengono inviati direttamente ai destinatari e-mail designati.
1. Consente di semplificare il flusso di lavoro integrando direttamente l’invio dei moduli nelle notifiche e-mail.
1. Aiuta le organizzazioni a personalizzare il contenuto delle e-mail, adattandolo quindi a specifiche esigenze di comunicazione.

![Proprietà modulo adattivo nell&#39;editor universale](/help/forms/assets/submit-actions-ue.png)


Per configurare un’azione di invio come E-mail per l’invio del modulo:

1. Apri il modulo adattivo in **Editor**.
1. Seleziona il **[!UICONTROL blocco modulo adattivo]**.
1. Fai clic sull&#39;icona delle proprietà ![proprietà](/help/forms/assets/Smock_Properties_18_N.svg).
1. Selezionare l&#39;opzione **[!UICONTROL Invia e-mail]** dall&#39;elenco a discesa **[!UICONTROL Invia azione]**.
1. Dopo aver selezionato l’opzione Invia e-mail, puoi configurare le seguenti proprietà come mostrato nell’immagine seguente.

<table>
  <thead>
    <tr>
      <th>Immagine</th>
      <th>Proprietà</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="Configurazione e-mail"></td> 
    <td><b>Da</td>
    <td>Specifica l'indirizzo e-mail del mittente.</td>
    </tr>
    <tr>
      <td><b>A</td>
      <td>Specifica i destinatari principali dell’e-mail. È possibile aggiungere più indirizzi e-mail, separati da virgole.</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>Specifica i destinatari che devono ricevere una copia per conoscenza (CC) dell’e-mail.</td>
    </tr>
    <tr>
      <td><b>CCN</td>
      <td>Specifica i destinatari che devono ricevere una copia per conoscenza nascosta (Ccn) dell’e-mail.</td>
    </tr>
    <tr>
      <td><b>Oggetto</td>
      <td>Specifica l’oggetto dell’e-mail.</td>
    </tr>
    <tr>
      <td><b>Usa modello esterno</td>
      <td>Consente di utilizzare un modello e-mail esterno per la formattazione del contenuto dell’e-mail. Specifica l’URL o il percorso del modello esterno per integrare un modello e-mail predefinito ospitato nella cartella di AEM Assets.</td>
    </tr>
    <tr>
      <td><b>Includi allegato</td>
      <td>Specifica se i dati del modulo inviato devono includere nell'e-mail un allegato inviato tramite il modulo. I formati di allegati supportati sono PDF, XML e JSON.</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## Mostra un messaggio di ringraziamento personalizzato all’invio di un modulo adattivo {#submit-action-message-ue}

L’opzione All’invio consente di configurare un messaggio di azione di invio all’invio di un modulo adattivo. Per configurare un messaggio di azione di invio per il modulo:

1. Apri il modulo adattivo in **Editor**.
1. Seleziona il **[!UICONTROL blocco modulo adattivo]**.
1. Fai clic sull&#39;icona delle proprietà ![proprietà](/help/forms/assets/Smock_Properties_18_N.svg).
1. Al clic, viene visualizzata la seguente opzione:
   * **[!UICONTROL All&#39;invio]**: all&#39;invio consente di personalizzare un messaggio da visualizzare all&#39;invio di un modulo. Per impostazione predefinita, quando un modulo viene inviato correttamente, all’utente viene visualizzato il messaggio personalizzato &quot;Grazie per l’invio del modulo&quot;.
Puoi anche personalizzare il messaggio di ringraziamento all&#39;invio del modulo selezionando l&#39;opzione per **[!UICONTROL Mostra messaggio]** e aggiungere/modificare il messaggio nel **Editor** Rich Text.


## Consulta anche

{{universal-editor-see-also}}

