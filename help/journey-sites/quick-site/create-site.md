---
title: Creare un sito da un modello
description: Scopri come creare rapidamente un sito AEM utilizzando un modello di sito.
exl-id: 31bb04c2-b3cc-44ca-b517-5b0d66d9b1fa
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 78%

---

# Creare un sito da un modello {#create-site-from-template}

Scopri come creare rapidamente un sito AEM utilizzando un modello di sito.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione rapida di siti AEM, [Comprendere Cloud Manager e il flusso di lavoro per la creazione rapida di siti,](cloud-manager.md) hai imparato Cloud Manager e come si collega al nuovo processo di creazione rapida dei siti e ora dovresti:

* Scopri in che modo AEM Sites e Cloud Manager collaborano per facilitare lo sviluppo front-end
* Scopri come il passaggio di personalizzazione front-end è completamente scollegato da AEM e non richiede alcuna conoscenza di AEM.

Questo articolo si basa su questi elementi fondamentali per consentirti di effettuare il primo passaggio di configurazione e creare un sito per un modello da personalizzare successivamente utilizzando gli strumenti front-end.

## Obiettivo {#objective}

Questo documento spiega come creare rapidamente un sito AEM utilizzando un modello di sito. Dopo la lettura dovresti:

* Comprendere come ottenere i modelli di sito di AEM.
* Scopri come creare un sito utilizzando un modello.
* Scopri come scaricare il modello dal tuo nuovo sito per fornirlo allo sviluppatore front-end.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso vale per l’amministratore AEM.

## Modelli per siti {#site-templates}

I modelli di sito consentono di combinare i contenuti di base del sito in un pacchetto semplice e riutilizzabile. Per consentire un rapido avvio del nuovo sito, i modelli di sito generalmente contengono il contenuto e la struttura di base del sito e informazioni sul suo stile. La struttura effettiva è la seguente:

* `files`: cartella con il kit dell’interfaccia utente, file XD ed eventualmente altri file
* `previews`: cartella con le schermate del modello di sito
* `site`: pacchetto di contenuti del contenuto copiato per ogni sito creato da questo modello, ad esempio modelli di pagina, pagine e così via.
* `theme`: origini del tema del modello per modificare l’aspetto del sito, inclusi CSS, JavaScript e così via.

I modelli sono potenti perché possono essere riutilizzati in modo che gli autori dei contenuti possano creare rapidamente un sito. Inoltre, poiché nell’installazione AEM si può disporre di più modelli, è possibile soddisfare le diverse esigenze aziendali in modo flessibile.

>[!NOTE]
>
>Il modello di sito non deve essere confuso con i modelli di pagina. I modelli di sito qui descritti definiscono la struttura complessiva di un sito. Un modello di pagina definisce la struttura e il contenuto iniziale di una singola pagina.

## Acquisizione di un modello di sito {#obtaining-template}

Il modo più semplice per iniziare è quello di [scaricare l’ultima versione del modello di sito standard AEM dal relativo archivio GitHub.](https://github.com/adobe/aem-site-template-standard/releases)

Una volta scaricato, puoi caricarlo nel tuo ambiente AEM come faresti con qualsiasi altro pacchetto. Consulta la [sezione Risorse aggiuntive](#additional-resources) per informazioni su come lavorare con i pacchetti, se hai bisogno di ulteriori informazioni su questo argomento.

>[!TIP]
>
>Il modello di sito standard AEM può essere personalizzato per soddisfare le esigenze del progetto ed evitare la necessità di ulteriori personalizzazioni. Tuttavia questo argomento esula dall’ambito del presente percorso. Per ulteriori informazioni, vedi la documentazione GitHub del modello di sito standard.

>[!TIP]
>
>Puoi anche scegliere di generare il modello dall’origine come parte del flusso di lavoro del progetto. Tuttavia questo argomento esula dall’ambito del presente percorso. Per ulteriori informazioni, vedi la documentazione GitHub del modello di sito standard.

## Installazione di un modello di sito {#installing-template}

L’utilizzo di un modello per creare un sito è semplice.

1. Accedi all’ambiente di authoring di AEM e passa alla console Sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Seleziona **Crea** in alto a destra e dal menu a discesa, seleziona **Sito da modello**.

   ![Creazione di un nuovo sito da un modello](assets/create-site-from-template.png)

1. Nella procedura guidata Crea sito, seleziona **Importa** nella parte superiore della colonna sinistra.

   ![Creazione guidata sito](assets/site-creation-wizard.png)

1. Nell’elenco dei file, individua il modello [hai scaricato in precedenza](#obtaining-template) e seleziona **Carica**.

1. Una volta caricato, il modello viene visualizzato nell’elenco dei modelli disponibili. Selezionala per selezionarla (rivelando anche informazioni sul modello nella colonna di destra), quindi seleziona **Successivo**.

   ![Seleziona un modello](assets/select-site-template.png)

1. Immetti un titolo per il sito. Se omesso, puoi specificare un nome per il sito o generarlo dal titolo.

   * Il titolo del sito viene visualizzato nella barra del titolo del browser.
   * Il nome del sito diventa parte dell’URL.

1. Seleziona **Crea** e il nuovo sito viene creato dal modello di sito.

   ![Dettagli del nuovo sito](assets/create-site-details.png)

1. Nella finestra di dialogo di conferma visualizzata, seleziona **Fine**.

   ![Finestra di dialogo di successo](assets/success.png)

1. Nella console Sites, i nuovi siti sono visibili e possono essere spostati per esplorarne la struttura di base definita dal modello.

   ![Struttura del nuovo sito](assets/new-site.png)

Gli autori dei contenuti adesso possono iniziare l’authoring.

## È richiesta un’ulteriore personalizzazione? {#customization-required}

I modelli di sito sono molto potenti e flessibili ed è possibile crearne qualsiasi numero per un progetto, consentendo di creare agevolmente varianti di sito. A seconda del livello di personalizzazione già eseguito sul modello di sito utilizzato, potrebbe non essere necessaria alcuna personalizzazione front-end aggiuntiva.

* Se il tuo sito non richiede una personalizzazione aggiuntiva, congratulazioni! Il tuo percorso termina qui!
* Se hai ancora bisogno di una personalizzazione front-end aggiuntiva, o se desideri semplicemente comprendere l’intero processo nel caso sia necessaria una personalizzazione futura, continua a leggere.

## Pagina di esempio {#example-page}

Se hai bisogno di ulteriori personalizzazioni front-end, ricorda che lo sviluppatore potrebbe non avere familiarità con i dettagli del contenuto. Pertanto, è consigliabile fornire allo sviluppatore un percorso dei contenuti tipici che possa essere utilizzato come base di riferimento in quanto il tema è personalizzato. Un esempio tipico è la home page della lingua master del sito.

1. Nel browser del sito passare alla home page della lingua master, quindi selezionare la pagina per selezionarla e selezionare **Modifica** nella barra dei menu.

   ![Home page tipica](assets/home-page-in-console.png)

1. Nell’editor, seleziona il pulsante **Informazioni pagina** nella barra degli strumenti e quindi **Visualizza come pubblicato**.

   ![Modificare l&#39;home page](assets/home-page-edit.png)

1. Nella scheda visualizzata, copia il percorso del contenuto dalla barra degli indirizzi. Avrà un aspetto simile a `/content/<your-site>/en/home.html?wcmmode=disabled`.

   ![Home page](assets/home-page.png)

1. Salva il percorso da fornire successivamente allo sviluppatore front-end.

## Scarica il tema {#download-theme}

Ora che il sito è stato creato, il tema sito generato dal modello può essere scaricato e fornito allo sviluppatore front-end per la personalizzazione.

1. Nella console Sites, mostra la barra **Sito**.

   ![Mostra barra del sito](assets/show-site-rail.png)

1. Seleziona la directory principale del nuovo sito, quindi fai clic su **Scarica origini tema** nella barra del sito.

   ![Scarica sorgenti del tema](assets/download-theme-sources.png)

Ora disponi di una copia dei file sorgenti del tema nei file di download.

## Configurazione utente proxy {#proxy-user}

Affinché lo sviluppatore front-end possa visualizzare in anteprima le personalizzazioni utilizzando il contenuto effettivo AEM dal sito, devi impostare un utente proxy.

1. In AEM dalla navigazione principale vai a **Strumenti** > **Sicurezza** > **Utenti**.
1. Nella console di gestione utenti, seleziona **Crea**.

   ![Console di gestione utenti](assets/user-management-console.png)
1. Nella finestra **Crea nuovo utente** devi fornire almeno:
   * **ID**: prendi nota di questo valore in quanto devi fornirlo allo sviluppatore front-end.
   * **Password**: salva questo valore in modo sicuro in un archivio password, in quanto devi fornirlo allo sviluppatore front-end.

   ![Dettagli nuovo utente](assets/new-user-details.png)

1. Nella scheda **Gruppi**, aggiungi l&#39;utente proxy al gruppo `contributors`.
   * Digitare il termine `contributors` attiva la funzione di completamento automatico di AEM per selezionare facilmente il gruppo.

   ![Aggiungi al gruppo](assets/add-to-group.png)

1. Seleziona **Salva e chiudi**.

La configurazione è stata completata. Gli autori dei contenuti ora possono iniziare a creare contenuti durante la preparazione del sito e iniziare la personalizzazione front-end nel passaggio successivo del percorso.

## Novità {#what-is-next}

Dopo aver completato questa parte del percorso di creazione rapida sito di AEM, è necessario:

* Comprendere come ottenere i modelli di sito di AEM.
* Scopri come creare un sito utilizzando un modello.
* Scopri come scaricare il modello dal tuo nuovo sito per fornirlo allo sviluppatore front-end.

Approfondisci questo argomento e continua il percorso di Creazione Rapida dei Siti AEM consultando il documento [Imposta la pipeline](pipeline-setup.md), in cui imparerai a creare una pipeline front-end per gestire la personalizzazione del tema sito.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso di Creazione Rapida dei Siti consultando il documento [Configura la pipeline,](pipeline-setup.md) le seguenti sono alcune risorse aggiuntive e opzionali che approfondiscono alcuni concetti menzionati in questo documento, ma non sono necessarie per continuare il percorso.

* [Modello del sito standard AEM](https://github.com/adobe/aem-site-template-standard): questo è l’archivio GitHub del modello del sito standard AEM.
* [Creazione e organizzazione delle pagine](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) - Questa guida descrive come gestire le pagine del sito AEM se desideri personalizzarlo ulteriormente dopo averlo creato dal modello.
* [Come lavorare con il pacchetto](/help/implementing/developing/tools/package-manager.md): i pacchetti consentono l&#39;importazione e l&#39;esportazione del contenuto dell&#39;archivio. Questo documento spiega come lavorare con i pacchetti in AEM 6.5, ed è applicabile anche ad AEMaaCS.
* [Documentazione sull’amministrazione del sito](/help/sites-cloud/administering/site-creation/create-site.md): per ulteriori informazioni sulle funzioni dello strumento Creazione Rapida dei Siti, consulta i documenti tecnici sulla creazione dei siti.
* [Crea o aggiungi moduli a una pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): scopri tecniche e best practice passo passo per integrare i moduli nel tuo sito web, ottimizzando le tue esperienze digitali per il massimo impatto.
