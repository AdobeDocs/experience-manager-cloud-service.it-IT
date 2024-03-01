---
title: Configura pagina di ringraziamento per EDS Forms
description: Scopri come configurare le pagine di ringraziamento e il reindirizzamento per EDS Forms per ottimizzare l’esperienza utente e semplificare i percorsi di utenti.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Configurazione delle pagine di ringraziamento e del reindirizzamento nei blocchi di Forms adattivi

Le pagine di ringraziamento e il reindirizzamento sono aspetti vitali del miglioramento dell’esperienza utente, fornendo agli utenti conferma, una comunicazione chiara e una navigazione fluida dopo l’invio del modulo.

## Configurazione delle pagine di ringraziamento

Le pagine di ringraziamento fungono da riconoscimento rassicurante per gli utenti e consentono alle organizzazioni di comunicare informazioni essenziali rafforzando al contempo l’identità del marchio. Segui questi passaggi per configurare una pagina di ringraziamento per EDS Forms:

1. Accedi alla cartella del progetto AEM Edge Delivery in Microsoft SharePoint o Google Workspace.
1. Crea un file Microsoft Word o Google Docs denominato &quot;grazie&quot; all’interno della directory del progetto.
1. Aggiungi il messaggio di ringraziamento al file &quot;grazie&quot;.
   ![Esempio di pagina di ringraziamento](/help/edge/assets/sample-thankyou-page.png)
1. Utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il file &quot;grazie&quot;.

## Reindirizzamento degli utenti dopo l’invio

Il reindirizzamento agevola percorsi di utenti senza soluzione di continuità, guidando gli utenti verso destinazioni rilevanti, ottimizzando il coinvolgimento e aumentando i tassi di conversione.

Per impostazione predefinita, il blocco Forms adattivo reindirizza gli utenti alla pagina &quot;grazie&quot;. Per reindirizzare gli utenti a una pagina diversa da quella predefinita, sono disponibili due opzioni:

* sostituire la pagina di ringraziamento esistente con una pagina diversa oppure
* reindirizza la pagina &quot;grazie&quot; a un’altra pagina a tua scelta.

### Sostituisci la pagina &quot;grazie&quot; esistente

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


### Usa reindirizzamenti siti Web

Configura un reindirizzamento del sito web per indirizzare la pagina di ringraziamento a una pagina diversa. Consulta la sezione [Documentazione dei reindirizzamenti](https://www.aem.live/docs/redirects) per istruzioni dettagliate.


