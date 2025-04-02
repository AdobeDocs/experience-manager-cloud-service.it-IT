---
title: Selettore frammento di contenuto micro-front-end per Adobe Experience Manager as a Cloud Service
description: Utilizza il Selettore frammenti di contenuto Microsoft-Frontend per cercare, trovare e recuperare frammenti di contenuto dall’applicazione.
role: Admin, User
source-git-commit: 32e1b3cef768b420f32b70202ddadc80db2b74e8
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 11%

---


# Selettore frammento di contenuto micro-front-end {#micro-frontend-content-fragment-selector}

Il selettore dei frammenti di contenuto micro-front-end fornisce un’interfaccia utente che si integra facilmente con l’archivio as a Cloud Service di Adobe Experience Manager (AEM). L’interfaccia consente di sfogliare o cercare frammenti di contenuto nell’archivio e di utilizzarli nell’applicazione.

L’interfaccia utente di Micro-Frontend è resa disponibile nell’applicazione utilizzando il pacchetto Selettore frammento di contenuto. Eventuali aggiornamenti al pacchetto vengono importati e caricati automaticamente nell’applicazione.

![Selettore frammento di contenuto micro-front-end - Panoramica](/help/headless/assets/content-fragment-selector-overview.png)

Il selettore dei frammenti di contenuto offre molti vantaggi, ad esempio:

* Facilità di integrazione con qualsiasi applicazione Adobe.
* Semplicità di manutenzione: gli aggiornamenti al pacchetto del selettore dei frammenti di contenuto vengono distribuiti automaticamente nel selettore dei frammenti di contenuto disponibile nell’applicazione. Ciò significa che l’applicazione non deve intervenire per caricare le modifiche più recenti.
* Facilità di personalizzazione grazie all’utilizzo di proprietà che controllano la visualizzazione del selettore dei frammenti di contenuto all’interno dell’applicazione.
* La ricerca full-text e i filtri personalizzabili consentono di navigare rapidamente nei frammenti di contenuto all’interno dell’esperienza di authoring.
* Possibilità di cambiare archivi all’interno di un’organizzazione IMS per la selezione di Frammenti di contenuto.
* Possibilità di ordinare i frammenti di contenuto e di visualizzarli nella vista selezionata.

## Prerequisiti {#prerequisites}

### Autenticazione IMS {#ims-authentication}

Se hai bisogno del flusso di lavoro di autenticazione IMS, assicurati che:

* L&#39;applicazione è in esecuzione su `HTTPS`.
* L’URL dell’applicazione si trova nell’elenco degli URL di reindirizzamento consentiti per il client IMS.
* Il flusso di accesso IMS viene configurato e renderizzato utilizzando un pop-up sul browser web. Pertanto, i popup devono essere abilitati o consentiti nel browser di destinazione.

In alternativa, se l’applicazione è già autenticata con il flusso di lavoro IMS, puoi aggiungere le informazioni IMS appropriate.

## Installazione {#installation}

Utilizza il componente `ContentFragmentSelector`. Sono disponibili diverse opzioni di installazione:

1. Registro NPM (Registro privato di Adobe)

   * Aggiungi quanto segue a `.npmrc`:

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * Quindi installare

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Archivio Git

   * Aggiungi quanto segue a `package.json` dipendenze:

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## Utilizzo del selettore dei frammenti di contenuto {#using-the-Content-Fragment-selector}

Una volta che il Selettore frammento di contenuto è configurato e autenticato per l’utilizzo del Selettore Frammento di contenuto con l’applicazione AEM as a Cloud Service, puoi selezionare Frammenti di contenuto o eseguire varie altre operazioni per cercare i frammenti nell’archivio:

![Selettore frammento di contenuto](/help/headless/assets/content-fragment-selector-using.png)

* Con il selettore **Archivio** in alto a destra, puoi selezionare l&#39;archivio che desideri utilizzare
* Nel pannello a sinistra puoi effettuare le seguenti operazioni:
   * Nascondere o mostrare le cartelle dall&#39;archivio selezionato
   * Seleziona una cartella specifica per mostrare i frammenti di contenuto in quella cartella
* Nel pannello principale puoi effettuare le seguenti operazioni:
   * Seleziona frammenti di contenuto
   * Cercare frammenti di contenuto
   * Ordina l&#39;elenco corrente in base a varie colonne, sia crescenti che decrescenti
   * Visualizzare l&#39;indicatore del formato di visualizzazione
   * Mostra, nascondi e specifica filtri

### Nascondi/Mostra pannello {#hide-show-panel}

Per nascondere le cartelle nel menu di navigazione a sinistra, fai clic sull’icona **Nascondi cartelle**. Per annullare le modifiche, fai di nuovo clic sull’icona **Nascondi cartelle**.

### Selettore archivio {#repository-switcher}

Il Selettore frammento di contenuto consente di selezionare un archivio per la selezione del frammento.

Puoi selezionare l&#39;archivio desiderato dal menu a discesa **Archivio**, disponibile nella parte superiore del pannello principale.

![Selettore frammento di contenuto](/help/headless/assets/content-fragment-repository-selector.png)

Le opzioni dell’archivio disponibili nell’elenco a discesa si basano sulla proprietà `repositoryId` definita nel file `index.html`. Questa proprietà si basa sull’ambiente dell’organizzazione IMS selezionata a cui accede l’utente attualmente connesso.

I consumatori possono passare un `repositoryID` preferito per eseguire il rendering dei frammenti da un archivio specifico e interrompere il rendering del commutatore dell’archivio.

### Cartelle dei frammenti di contenuto {#content-fragments-folders}

L’archivio Frammenti di contenuto è una raccolta di cartelle di Frammenti di contenuto che è possibile utilizzare per eseguire operazioni.

### Filtri {#filters}

Il Selettore frammento di contenuto fornisce anche opzioni di filtro predefinite per perfezionare i risultati della ricerca. Sono disponibili vari filtri, tra cui:

* **Modello frammento**
* **Localizzazione**
* **Stato**: lo stato corrente del frammento; `New`, `Draft`, `Published`, `Modified`, `Unpublished`
* Tag
* Utenti
* Ore e date

![Opzioni filtro](/help/headless/assets/content-selector-filters.png)

Puoi anche creare un filtro di ricerca predefinito da salvare per utilizzi futuri. Per creare filtri di ricerca personalizzati per i frammenti di contenuto, è possibile utilizzare la proprietà `filterSchema`.

### Barra di ricerca {#search-bar}

Il Selettore frammenti di contenuto consente di eseguire una ricerca full-text dei frammenti all’interno dell’archivio selezionato. Ad esempio, se digiti la parola chiave `wave` nella barra di ricerca, vengono visualizzati tutti i frammenti con la parola chiave `wave` citata in una delle proprietà dei metadati.

### Ordinamento {#sorting}

Puoi ordinare i frammenti nel Selettore frammento di contenuto in base a varie proprietà. Puoi anche ordinare i frammenti in ordine crescente o decrescente.

### Tipo di visualizzazione {#view-type}

Il selettore frammento di contenuto consente di visualizzare il frammento in:

* **Vista tabella**
