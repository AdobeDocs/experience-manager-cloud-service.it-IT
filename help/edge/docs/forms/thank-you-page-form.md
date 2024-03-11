---
title: Configurare la pagina di ringraziamento o il modulo di reindirizzamento dopo l’invio
description: Scopri come configurare le pagine di ringraziamento e il reindirizzamento per Forms Block per ottimizzare l’esperienza utente e semplificare i percorsi di utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
source-git-commit: 4144f9704aaf17ea684be147395adc3aa31641f2
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# Mostra la pagina di ringraziamento o il modulo di reindirizzamento dopo l’invio

Dopo che un utente ha inviato un modulo, è fondamentale fornire un’esperienza fluida tramite una pagina di ringraziamento o un reindirizzamento. Questi elementi non solo confermano la corretta presentazione, ma aumentano anche la soddisfazione degli utenti e li guidano ulteriormente nel loro percorso.

* **Pagina di ringraziamento**: una pagina di ringraziamento è una pietra miliare dell’esperienza utente e offre rassicurazione e trasmissione di informazioni importanti, rafforzando al contempo l’identità del brand. Serve come riconoscimento diretto dell&#39;azione dell&#39;utente, promuovendo un senso di completamento e soddisfazione.

* **Reindirizza**: un reindirizzamento svolge un ruolo fondamentale nel indirizzare gli utenti verso destinazioni rilevanti, ottimizzare il coinvolgimento e, in ultima analisi, aumentare i tassi di conversione. Guidando gli utenti alla fase successiva del percorso, un reindirizzamento garantisce un’esperienza di navigazione fluida. Ad esempio, reindirizzando l’utente alla pagina dei pagamenti dopo la raccolta dei dettagli iniziali.

Nel blocco Forms adattivo, il comportamento predefinito consiste nella visualizzazione di una pagina di ringraziamento. Tuttavia, puoi personalizzare questa esperienza in base alle tue esigenze specifiche. Le opzioni includono:

* [Configurazione della pagina e del messaggio di ringraziamento per l’allineamento con gli obiettivi di brand e comunicazione](#configuring-the-thank-you-page-and-message)
* [Reindirizzamento degli utenti a un’altra pagina dopo l’invio per ulteriori azioni](#redirect-users-to-another-page-post-submission)

## Configurazione della pagina di ringraziamento e del messaggio

Il comportamento predefinito di Blocco Forms adattivo consiste nella visualizzazione della pagina &quot;grazie&quot; all’invio. Per configurare la pagina di ringraziamento per il blocco Forms adattivo, segui la procedura riportata di seguito:

1. Accedi alla cartella del progetto AEM Edge Delivery in Microsoft SharePoint o Google Workspace.
1. Crea un file Microsoft Word o Google Docs denominato &quot;grazie&quot; all’interno della directory del progetto.
1. Aggiungi il messaggio di ringraziamento al file &quot;grazie&quot;. </br>

   ![Esempio di pagina di ringraziamento](/help/edge/assets/sample-thankyou-page.png)

1. Utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il file &quot;grazie&quot;.

Il blocco Forms adattivo visualizza la pagina &quot;grazie&quot; all’invio del modulo.

## Reindirizza gli utenti a un’altra pagina dopo l’invio

Per impostazione predefinita, il blocco Forms adattivo reindirizza gli utenti alla pagina &quot;grazie&quot;. Per reindirizzare gli utenti a una pagina diversa da quella predefinita, sono disponibili due opzioni:

* [Sostituisci la pagina &quot;grazie&quot; con un’altra pagina](#replace-the-existing-thankyou-page)
* [Utilizza i reindirizzamenti del sito web per il reindirizzamento della pagina &quot;grazie&quot;](#use-website-redirects-for-thankyou-page-redirection)

### Sostituisci la pagina &quot;grazie&quot;

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
   > Assicurati che nella cartella dei progetti dei Edge Delivery Services sia presente una pagina con lo stesso nome in Microsoft SharePoint o Google Workspace. Se la pagina non esiste, procedi alla sua creazione e pubblicazione.

1. Procedi con l’archiviazione della cartella &quot;form.js&quot; aggiornata e dei relativi file sottostanti nel progetto Edge Delivery Services su GitHub. Questo aggiornamento assicura che il modulo ora venga reindirizzato alla pagina aggiornata come specificato.

1. Assicurati che la pagina esista nella cartella dei progetti EDS e pubblicala.


### Utilizza i reindirizzamenti del sito web per il reindirizzamento della pagina &quot;grazie&quot;

Il reindirizzamento di un utente a un’altra pagina dopo l’invio del modulo può migliorare l’esperienza utente fornendo informazioni rilevanti, confermando le azioni e guidando gli utenti verso i risultati desiderati. Ad esempio:

* dopo aver completato un modulo di acquisto, l’utente viene reindirizzato a una pagina di pagamento per completare la transazione in modo sicuro.
* quando si invia un modulo di registrazione per un evento o un webinar, gli utenti vengono reindirizzati a una pagina di conferma in cui vengono visualizzati i dettagli dell’evento, ad esempio data, ora e posizione.

Per reindirizzare la pagina &quot;Grazie&quot; a un’altra pagina, utilizza [reindirizzamenti al sito web](https://www.aem.live/docs/redirects) foglio di calcolo.


## Consulta anche

{{see-more-forms-eds}}