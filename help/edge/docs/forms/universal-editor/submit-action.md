---
title: Azioni di invio
description: Configura le azioni di invio per modulo adattivo.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
hide: true
hidefromToC: true
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 100%

---

# Azione di invio per modulo adattivo

## Panoramica

L’invio di un modulo è il passaggio finale critico nel percorso dell’utente, dove i dati raccolti vengono elaborati e vengono intraprese azioni. Questo documento fornisce una guida completa alla configurazione e alla gestione delle azioni di invio per moduli adattivi nell’editor universale.

### Che cosa imparerai

Alla fine di questo documento comprenderai come:

- Configurare diversi tipi di azioni di invio per i moduli
- Configurare gli invii di endpoint REST per l’integrazione con i sistemi esterni
- Configurare gli invii di e-mail per le risposte ai moduli
- Implementare azioni di invio personalizzate per esigenze aziendali specifiche
- Gestire gli scenari di errore e convalida del modulo durante l’invio

### Pubblico target

Questa guida è progettata per:

- **Sviluppatori di moduli** che implementano la logica di invio
- **Integratori di sistema** che collegano i moduli ai sistemi di back-end
- **Analisti ziendali** che definiscono i flussi di lavoro del modulo
- **Architetti tecnici** che progettano i processi di invio del modulo

### Azioni di invio disponibili

L’editor universale fornisce due tipi di azioni di invio principali:

1. **Invio all’endpoint REST** * Invia dati del modulo agli endpoint API
2. **Invio di e-mail** * Invia risposte del modulo tramite e-mail

### Prerequisiti

Prima di configurare le azioni di invio, verifica di disporre di:

- Accesso all’editor universale
- Autorizzazioni appropriate per la configurazione del modulo
- Informazioni sull’endpoint di invio di destinazione o sulla configurazione e-mail

Un’azione di invio specifica la destinazione dei dati raccolti tramite un modulo adattivo. Il processo di invio inizia quando l’utente fa clic sul pulsante **[!UICONTROL Invia]** nel modulo. AEM Forms offre due tipi di azioni di invio descritte di seguito e consente di creare e utilizzare azioni di invio personalizzate per soddisfare esigenze specifiche. Le azioni di invio predefinite sono:

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

- [Invia a endpoint REST](#rest-endpoint-submission-ue)
- [Invia e-mail](#email-submission-ue)


### Invia a endpoint REST {#rest-endpoint-submission-ue}

L’azione Invia a endpoint REST viene utilizzata per inviare i dati del modulo a un endpoint REST specificato. L’endpoint può appartenere a un server interno in cui il modulo è ospitato oppure a un server esterno utilizzando rispettivamente un percorso relativo o un percorso assoluto. Per inviare i dati al server AEM che ospita il modulo, utilizza un percorso relativo corrispondente al percorso principale del server AEM. Ad esempio, `/content/forms/af/SampleForm.html`. Per inviare dati a qualsiasi altro server, utilizza un percorso assoluto.

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
- It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
- Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
- Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



Per configurare un endpoint REST:

1. Apri il modulo adattivo in **[!UICONTROL Editor]**.
1. Seleziona **[!UICONTROL Blocco modulo adattivo]**.
1. Fai clic sull’icona delle proprietà ![proprietà](/help/forms/assets/Smock_Properties_18_N.svg).
1. Seleziona **[!UICONTROL Invia a un endpoint REST]** dall’elenco a discesa **[!UICONTROL Azione di invio]**.
1. Specifica l’URL dell’endpoint REST.
1. Puoi anche selezionare **Abilita richiesta POST** e fornire un URL per pubblicare la richiesta.

![Schermata del pannello delle proprietà dell’editor universale che mostra i campi di configurazione dell’endpoint REST, inclusi l’input dell’URL e il pulsante di attivazione/disattivazione della richiesta POST per l’invio del modulo](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> - Per pubblicare i dati su un server interno, specifica il percorso della risorsa. I dati vengono inseriti nel percorso della risorsa. Ad esempio, `/content/restEndPoint`. Per tali richieste POST, vengono utilizzate le informazioni di autenticazione della richiesta di invio.
> - Per pubblicare dati su un server esterno, fornisci un URL. Il formato dell’URL è `https://host:port/path_to_rest_end_point`. Assicurati di configurare il percorso per gestire la richiesta POST in modo anonimo.

### Invia e-mail {#email-submission-ue}

L’azione di invio Invia e-mail consente di inviare un messaggio e-mail a uno o più destinatari in seguito all’invio corretto del modulo. La configurazione Invia e-mail consente di creare un messaggio e-mail che può includere i dati del modulo in un formato predefinito. Ad esempio, considera il seguente modello in cui il nome del cliente, l’indirizzo di spedizione, il nome dello stato e il codice postale vengono recuperati dai dati del modulo inviato. [Ulteriori informazioni sui modelli e-mail in moduli adattivi](/help/forms/html-email-templates-in-adaptive-forms.md). Alcuni vantaggi della configurazione di un modulo adattivo con l’azione di invio Invia e-mail sono:

1. Comunicazione rapida, in quanto i dati del modulo vengono inviati direttamente ai destinatari e-mail designati.
1. Flusso di lavoro più semplice, integrando direttamente l’invio dei moduli nelle notifiche e-mail.
1. Personalizzazione del contenuto delle e-mail agevolata, adatta a specifiche esigenze di comunicazione.

![Proprietà modulo adattivo nell’editor universale](/help/forms/assets/submit-actions-ue.png)


Per configurare un’azione di invio come e-mail per l’invio del modulo:

1. Apri il modulo adattivo nell’**editor**.
1. Seleziona il **[!UICONTROL Blocco per moduli adattivi]**.
1. Fai clic sull’icona delle proprietà ![proprietà](/help/forms/assets/Smock_Properties_18_N.svg).
1. Seleziona l’opzione **[!UICONTROL Invia e-mail]** dall’elenco a discesa **[!UICONTROL Azione di invio]**.
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
    <td>Specifica l’indirizzo e-mail del mittente.</td>
    </tr>
    <tr>
      <td><b>A</td>
      <td>Specifica i destinatari principali dell’e-mail. È possibile aggiungere più indirizzi e-mail, separati da virgole.</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>Specifica i destinatari che devono ricevere una copia per conoscenza (Cc) dell’e-mail.</td>
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
      <td>Consente di utilizzare un modello e-mail esterno per la formattazione del contenuto dell’e-mail. Indica l’URL o il percorso del modello esterno per integrare un modello e-mail predefinito ospitato nella cartella di AEM Assets.</td>
    </tr>
    <tr>
      <td><b>Includi allegato</td>
      <td>Specifica se i dati del modulo inviato devono includere nell’e-mail un allegato inviato tramite il modulo. I formati di allegati supportati sono PDF, XML e JSON.</td>
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

    ![Screenshot of the Universal Editor email configuration panel showing fields for From, To, CC, BCC, Subject, and options for external templates and attachments](/help/forms/assets/email-config-ue.png)

-->

## Mostrare un messaggio di ringraziamento personalizzato dopo l’invio di un modulo adattivo {#submit-action-message-ue}

L’opzione All’invio consente di configurare un messaggio di azione di invio quando viene inviato un modulo adattivo. Per configurare tale messaggio:

1. Apri il modulo adattivo nell’**editor**.
1. Seleziona il **[!UICONTROL Blocco per moduli adattivi]**.
1. Fai clic sull’icona delle proprietà ![proprietà](/help/forms/assets/Smock_Properties_18_N.svg).
1. Quando fai clic, viene visualizzata la seguente opzione:
   - **[!UICONTROL All’invio]**: all’invio consente di personalizzare un messaggio da visualizzare all’invio di un modulo. Per impostazione predefinita, quando un modulo viene inviato correttamente, all’utente viene mostrato il messaggio personalizzato “Grazie per l’invio del modulo”.
Puoi anche personalizzare il messaggio di ringraziamento all’invio del modulo selezionando l’opzione **[!UICONTROL Mostra messaggio]** e aggiungendo/modificando il messaggio nell’**editor** Rich Text.



