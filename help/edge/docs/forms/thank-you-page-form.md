---
title: Mostrare un messaggio di ringraziamento personalizzato dopo l’invio del modulo
description: Scopri come configurare le pagine di ringraziamento e il reindirizzamento per il Blocco moduli per ottimizzare l’esperienza utente e semplificare i percorsi di utenti.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 25%

---

# Mostrare un messaggio di ringraziamento personalizzato dopo l’invio del modulo

Dopo che un utente ha inviato un modulo, è fondamentale fornire un’esperienza fluida attraverso un messaggio di ringraziamento. Non solo conferma la corretta presentazione, ma migliora anche la soddisfazione degli utenti e li guida ulteriormente nel loro percorso.

* **Messaggio di ringraziamento**: un messaggio di ringraziamento è una pietra miliare dell&#39;esperienza utente, che offre rassicurazione e trasmissione di informazioni importanti rafforzando al contempo l&#39;identità del marchio. Serve come riconoscimento diretto dell&#39;azione dell&#39;utente, promuovendo un senso di completamento e soddisfazione.

* **Reindirizzamento**: un reindirizzamento ha un ruolo fondamentale nel guidare gli utenti verso destinazioni rilevanti, nell&#39;ottimizzare il coinvolgimento e, infine, nell&#39;aumentare i tassi di conversione. Guidando gli utenti alla fase successiva del percorso, un reindirizzamento garantisce un’esperienza di navigazione fluida. Ad esempio, reindirizzando l’utente alla pagina dei pagamenti dopo la raccolta dei dettagli iniziali.

Il comportamento predefinito del Blocco moduli adattivi consiste nella visualizzazione del seguente messaggio di ringraziamento all’invio. Il messaggio viene visualizzato nella parte superiore del modulo in caso di invio corretto del modulo.

![messaggio di ringraziamento predefinito](/help/edge/assets/thank-you-message.png)

Tuttavia, puoi personalizzare questa esperienza in base alle tue esigenze specifiche. Le opzioni includono:

* Mostrare un messaggio di ringraziamento personalizzato dopo l’invio del modulo
* Reindirizza gli utenti a un’altra pagina dopo l’invio per ulteriori azioni

>[!NOTE]
>
> Per personalizzare il messaggio di ringraziamento in base alle proprie esigenze, è possibile fare riferimento al seguente [foglio di calcolo delle richieste](/help/edge/docs/forms/assets/enquiry.xlsx).

## Configurare un messaggio di ringraziamento personalizzato

Se desideri visualizzare un messaggio di ringraziamento personalizzato dopo l’invio corretto del modulo, puoi configurare il foglio di calcolo per visualizzarlo.

Per configurare un messaggio di ringraziamento personalizzato per il Blocco moduli adattivi, effettua le seguenti operazioni:

1. Vai alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.
1. Aggiungere un messaggio di ringraziamento personalizzato nella colonna `value` per il tipo di campo `submit` nel foglio di calcolo.

   ![Messaggio di ringraziamento personalizzato](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Aggiungere ad esempio `Submission Successful!` messaggio nella colonna `value` per il tipo di campo `submit`.

1. Visualizza in anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Messaggio di ringraziamento personalizzato](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Reindirizza gli utenti a un’altra pagina dopo l’invio

Il reindirizzamento di un utente a un’altra pagina dopo l’invio del modulo può migliorare l’esperienza utente fornendo informazioni rilevanti, confermando le azioni e guidando gli utenti verso i risultati desiderati. Ad esempio:

* dopo aver completato un modulo di acquisto, l’utente viene reindirizzato a una pagina di pagamento per completare la transazione in modo sicuro.
* quando si invia un modulo di registrazione per un evento o un webinar, gli utenti vengono reindirizzati a una pagina di conferma in cui vengono visualizzati i dettagli dell’evento, ad esempio data, ora e posizione.

Per reindirizzare gli utenti a un’altra pagina, effettua le seguenti operazioni:

1. Vai alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.
1. Incolla l&#39;URL nella colonna `value` per il tipo di campo `submit` nel foglio di calcolo per reindirizzare l&#39;utente in caso di invio corretto del modulo.
Per reindirizzare la pagina a una pagina diversa, utilizza l&#39;URL della pagina [Documentazione di Edge Delivery](https://www.aem.live/docs/).

   ![URL di reindirizzamento ringraziamento](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Visualizza in anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Reindirizza messaggio di ringraziamento](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

È inoltre possibile creare un nuovo file di documento e aggiungere il relativo URL di anteprima nella colonna `value` per il tipo di campo `submit`.

Dopo che un utente ha inviato un modulo, è importante fornire un chiaro messaggio di ringraziamento. Conferma l’esito positivo dell’invio e migliora la soddisfazione degli utenti.

## Consulta anche

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 



## See also

{{see-more-forms-eds}}