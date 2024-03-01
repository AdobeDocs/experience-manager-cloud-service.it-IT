---
title: Configura pagina di ringraziamento per EDS Forms
description: Scopri come configurare le pagine di ringraziamento e il reindirizzamento per EDS Forms per ottimizzare l’esperienza utente e semplificare i percorsi di utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: cadeccd916884ca2437e2b2684771c181cc8281e
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---


# Mostra la pagina di ringraziamento o il modulo di reindirizzamento dopo l’invio

Dopo che un utente ha inviato un modulo, è fondamentale fornire un’esperienza fluida tramite una pagina di ringraziamento o un reindirizzamento. Questi elementi non solo confermano la corretta presentazione, ma aumentano anche la soddisfazione degli utenti e li guidano ulteriormente nel loro percorso.

* **Pagina di ringraziamento**: una pagina di ringraziamento è una pietra miliare dell’esperienza utente e offre rassicurazione e trasmissione di informazioni importanti, rafforzando al contempo l’identità del brand. Serve come riconoscimento diretto dell&#39;azione dell&#39;utente, promuovendo un senso di completamento e soddisfazione.

* **Reindirizza**: un reindirizzamento svolge un ruolo fondamentale nel indirizzare gli utenti verso destinazioni rilevanti, ottimizzare il coinvolgimento e, in ultima analisi, aumentare i tassi di conversione. Guidando gli utenti alla fase successiva del percorso, un reindirizzamento garantisce un’esperienza di navigazione fluida. Ad esempio, reindirizzando l’utente alla pagina dei pagamenti dopo la raccolta dei dettagli iniziali.

Nel blocco Forms adattivo, il comportamento predefinito consiste nella visualizzazione di una pagina di ringraziamento. Tuttavia, puoi personalizzare questa esperienza in base alle tue esigenze specifiche. Le opzioni includono:

* [Configurazione della pagina e del messaggio di ringraziamento per l’allineamento con gli obiettivi di brand e comunicazione](#configuring-the-thank-you-page-and-message)
* [Reindirizzamento degli utenti a un’altra pagina dopo l’invio](#redirect-users-to-another-page-post-submission), rafforzando ulteriormente il loro percorso

## Configurazione della pagina di ringraziamento e del messaggio

Il comportamento predefinito del blocco Forms adattivo consiste nella visualizzazione della pagina &quot;grazie&quot; all’invio. Per configurare la pagina di ringraziamento per il blocco Forms adattivo, segui la procedura riportata di seguito:

1. Accedi alla cartella del progetto AEM Edge Delivery in Microsoft SharePoint o Google Workspace.
1. Crea un file Microsoft Word o Google Docs denominato &quot;grazie&quot; all’interno della directory del progetto.
1. Aggiungi il messaggio di ringraziamento al file &quot;grazie&quot;. </br>

   ![Esempio di pagina di ringraziamento](/help/edge/assets/sample-thankyou-page.png)

1. Utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il file &quot;grazie&quot;.

Nel blocco Forms adattivo viene visualizzata la pagina &quot;Grazie&quot; all’invio del modulo.

## Reindirizza gli utenti a un’altra pagina dopo l’invio

Per impostazione predefinita, il blocco Forms adattivo reindirizza gli utenti alla pagina &quot;grazie&quot;. Per reindirizzare gli utenti a una pagina diversa da quella predefinita, sono disponibili due opzioni:

* sostituire la pagina esistente &quot;grazie&quot; con una pagina diversa oppure
* reindirizza la pagina &quot;grazie&quot; a un’altra pagina a tua scelta.

### Sostituisci la pagina di ringraziamento esistente

1. Apri il &quot;[Progetto EDS]/blocks/form/form.js&quot;.
1. Modificare il `thankyou` pagina nella riga seguente alla pagina scelta:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Ad esempio:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > Assicurati che nella cartella dei progetti del servizio di consegna Edge sia presente una pagina con lo stesso nome in Microsoft SharePoint o Google Workspace. Se la pagina non esiste, procedi alla sua creazione e pubblicazione.

1. Procedi con l’archiviazione della cartella &quot;form.js&quot; aggiornata e dei relativi file sottostanti nel progetto del servizio di consegna Edge su GitHub. Questo aggiornamento assicura che il modulo ora venga reindirizzato alla pagina aggiornata come specificato.

1. Assicurati che la pagina esista nella cartella dei progetti EDS e pubblicala.


### Utilizzare i reindirizzamenti del sito Web

Configura un reindirizzamento del sito web per indirizzare la pagina di ringraziamento a una pagina diversa. Consulta la sezione [Documentazione dei reindirizzamenti](https://www.aem.live/docs/redirects) per istruzioni dettagliate.

## Vedi altro

* [Componenti del modulo](/help/edge/docs/forms/form-components.md)
* [Proprietà del campo modulo](/help/edge/docs/forms/eds-form-field-properties)
* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)
