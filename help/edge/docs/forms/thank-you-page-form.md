---
title: Mostrare un messaggio di ringraziamento personalizzato dopo l’invio di un modulo
description: Scopri come configurare le pagine di ringraziamento e il reindirizzamento per il Blocco moduli per ottimizzare l’esperienza utente e semplificare i percorsi di utenti.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '557'
ht-degree: 100%

---

# Mostrare un messaggio di ringraziamento personalizzato dopo l’invio di un modulo

Dopo che un utente ha inviato un modulo, è fondamentale fornire un’esperienza semplice con un messaggio di ringraziamento. Questo non solo conferma l’avvenuto invio, ma migliora anche la soddisfazione degli utenti e li guida ulteriormente nel loro percorso.

- **Messaggio di ringraziamento**: un messaggio di ringraziamento è una pietra miliare dell’esperienza utente, che offre rassicurazione e trasmette informazioni importanti rafforzando al contempo l’identità del marchio. Il messaggio di ringraziamento serve come riconoscimento diretto dell’azione dell’utente, generando un senso di completamento e soddisfazione.

- **Reindirizzamento**: un reindirizzamento ha un ruolo fondamentale nel guidare gli utenti verso destinazioni rilevanti, nell’ottimizzare il coinvolgimento e, infine, nell’aumentare i tassi di conversione. Guidando gli utenti alla fase successiva del percorso in modo semplice, un reindirizzamento garantisce un’esperienza di navigazione fluida. Ad esempio, reindirizzando l’utente alla pagina dei pagamenti dopo la raccolta dei dettagli iniziali.

Il comportamento predefinito del blocco moduli adattivi consiste nella visualizzazione del seguente messaggio di ringraziamento all’invio. Il messaggio viene visualizzato nella parte superiore del modulo a seguito dell’avvenuto invio di un modulo.

![messaggio di ringraziamento predefinito](/help/edge/assets/thank-you-message.png)

Tuttavia, è possibile personalizzare questa esperienza in base alle proprie esigenze specifiche. Le opzioni includono:

- Mostrare un messaggio di ringraziamento personalizzato dopo l’invio di un modulo
- Reindirizzare gli utenti a un’altra pagina dopo l’invio per ulteriori azioni

>[!NOTE]
>
> Per personalizzare il messaggio di ringraziamento in base alle proprie esigenze, è possibile fare riferimento al seguente [foglio di calcolo “enquiry”](/help/edge/docs/forms/assets/enquiry.xlsx).

## Configurazione di un messaggio di ringraziamento personalizzato

Se desideri visualizzare un messaggio di ringraziamento personalizzato dopo l’invio riuscito del modulo, puoi configurare il foglio di calcolo per visualizzarlo.

Per configurare un messaggio di ringraziamento personalizzato per il Blocco moduli adattivi, effettua le seguenti operazioni:

1. Passa alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.
1. Aggiungi un messaggio di ringraziamento personalizzato nella colonna `value` per il tipo di campo `submit` nel foglio di calcolo.

   ![Messaggio di ringraziamento personalizzato](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Aggiungi, ad esempio, il messaggio `Submission Successful!` nella colonna `value` per il tipo di campo `submit`.

1. Visualizza in anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Messaggio di ringraziamento personalizzato](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Reindirizzare gli utenti a un’altra pagina dopo l’invio

Il reindirizzamento di un utente a un’altra pagina dopo l’invio del modulo può migliorare l’esperienza utente fornendo informazioni rilevanti, confermando le azioni e guidando gli utenti verso i risultati desiderati. Ad esempio:

- dopo aver completato un modulo di acquisto, l’utente viene reindirizzato a una pagina di pagamento per completare la transazione in modo sicuro.
- Quando inviano un modulo di registrazione per un evento o un webinar, gli utenti vengono reindirizzati a una pagina di conferma in cui vengono visualizzati i dettagli dell’evento, ad esempio data, ora e posizione.

Per reindirizzare gli utenti a un’altra pagina, effettua le seguenti operazioni:

1. Passa alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.
1. Incolla l’URL nella colonna `value` per il tipo di campo `submit` nel foglio di calcolo per reindirizzare l’utente in caso di invio riuscito del modulo.
Per reindirizzare la pagina a una pagina diversa, utilizza l’URL della pagina [Documentazione di Edge Delivery](https://www.aem.live/docs/).

   ![URL di reindirizzamento ringraziamento](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Visualizza in anteprima e pubblica il foglio utilizzando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Reindirizzamento del messaggio di ringraziamento](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

È inoltre possibile creare un nuovo file di documento e aggiungere il relativo URL di anteprima nella colonna `value` per il tipo di campo `submit`.

Dopo che un utente ha inviato un modulo, è importante fornire un chiaro messaggio di ringraziamento. Il messaggio conferma l’esito positivo dell’invio e migliora la soddisfazione degli utenti.

