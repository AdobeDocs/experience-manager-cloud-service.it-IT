---
title: Crea sito da modello
description: Scopri come creare rapidamente un nuovo sito AEM utilizzando un modello di sito.
exl-id: 31bb04c2-b3cc-44ca-b517-5b0d66d9b1fa
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 0%

---

# Crea sito da modello {#create-site-from-template}

Scopri come creare rapidamente un nuovo sito AEM utilizzando un modello di sito.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di creazione di siti rapidi AEM, [Comprendere Cloud Manager e il flusso di lavoro per la creazione rapida di siti,](cloud-manager.md) hai appreso di Cloud Manager e di come si collega il nuovo processo di creazione rapida dei siti e ora dovresti:

* Scopri in che modo AEM Sites e Cloud Manager collaborano per facilitare lo sviluppo front-end
* Scopri come il passaggio di personalizzazione front-end è completamente scollegato dalla AEM e non richiede alcuna conoscenza AEM.

Questo articolo si basa su questi elementi di base, in modo da poter effettuare il primo passaggio di configurazione e creare un nuovo sito da un modello che puoi personalizzare successivamente utilizzando gli strumenti front-end.

## Obiettivo {#objective}

Questo documento spiega come creare rapidamente un nuovo sito AEM utilizzando un modello di sito. Dopo la lettura è necessario:

* Scopri come ottenere AEM modelli di sito.
* Scopri come creare un nuovo sito utilizzando un modello.
* Scopri come scaricare il modello dal tuo nuovo sito per fornire allo sviluppatore front-end.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso si applica all&#39;amministratore AEM.

## Modelli per siti {#site-templates}

I modelli di sito consentono di combinare i contenuti di base del sito in un pacchetto comodo e riutilizzabile. I modelli di sito generalmente contengono il contenuto e la struttura di base del sito, nonché informazioni sullo stile del sito per consentire un rapido avvio del nuovo sito. La struttura effettiva è la seguente:

* `files`: Cartella con il kit dell&#39;interfaccia utente, XD file ed eventualmente altri file
* `previews`: Cartella con schermate del modello di sito
* `site`: Pacchetto di contenuti del contenuto copiato per ogni sito creato da questo modello, ad esempio modelli di pagina, pagine e così via.
* `theme`: Sorgenti del tema del modello per modificare l&#39;aspetto del sito, inclusi CSS, JavaScript e così via.

I modelli sono potenti perché possono essere riutilizzati in modo che gli autori dei contenuti possano creare rapidamente un sito. Inoltre, poiché è possibile disporre di più modelli nell&#39;installazione AEM, è possibile soddisfare le diverse esigenze aziendali in modo flessibile.

>[!NOTE]
>
>Il modello di sito non deve essere confuso con i modelli di pagina. I modelli di sito qui descritti definiscono la struttura complessiva di un sito. Un modello di pagina definisce la struttura e il contenuto iniziale di una singola pagina.

## Ottenimento di un modello di sito {#obtaining-template}

Il modo più semplice per iniziare è [scarica l’ultima versione del modello di sito standard AEM dal relativo archivio GitHub.](https://github.com/adobe/aem-site-template-standard/releases)

Una volta scaricato puoi caricarlo nel tuo ambiente AEM come faresti con qualsiasi altro pacchetto. Consulta la sezione [Sezione Risorse aggiuntive](#additional-resources) per informazioni su come lavorare con i pacchetti, se hai bisogno di ulteriori informazioni su questo argomento.

>[!TIP]
>
>Il modello di sito standard AEM può essere personalizzato per soddisfare le esigenze del progetto ed evitare la necessità di ulteriori personalizzazioni. Tuttavia questo argomento va oltre il campo di applicazione del percorso. Per ulteriori informazioni, consulta la documentazione GitHub del modello di sito standard .

>[!TIP]
>
>Puoi anche scegliere di generare il modello dall’origine come parte del flusso di lavoro del progetto. Tuttavia questo argomento va oltre il campo di applicazione del percorso. Per ulteriori informazioni, consulta la documentazione GitHub del modello di sito standard .

## Installazione di un modello di sito {#installing-template}

L&#39;utilizzo di un modello per creare un nuovo sito è molto semplice.

1. Accedi all’ambiente di authoring AEM e passa alla console Sites

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Tocca o fai clic su **Crea** in alto a destra dello schermo e dal menu a discesa seleziona **Sito da modello**.

   ![Creazione di un nuovo sito da un modello](assets/create-site-from-template.png)

1. Nella procedura guidata Crea sito, tocca o fai clic su **Importa** nella parte superiore sinistra della colonna.

   ![Creazione guidata sito](assets/site-creation-wizard.png)

1. Nel browser dei file, individua il modello [scaricato in precedenza](#obtaining-template) e tocca o fai clic su **Carica**.

1. Una volta caricato, viene visualizzato nell’elenco dei modelli disponibili. Tocca o fai clic su di esso per selezionarlo (che rivela anche informazioni sul modello nella colonna di destra), quindi tocca o fai clic su **Successivo**.

   ![Seleziona un modello](assets/select-site-template.png)

1. Specifica un titolo per il sito. Se omesso, è possibile specificare un nome di sito o generarlo dal titolo.

   * Il titolo del sito viene visualizzato nella barra del titolo del browser.
   * Il nome del sito diventa parte dell’URL.

1. Tocca o fai clic su **Crea** e il nuovo sito viene creato dal modello di sito.

   ![Dettagli del nuovo sito](assets/create-site-details.png)

1. Nella finestra di dialogo di conferma visualizzata, tocca o fai clic su **Fine**.

   ![Finestra di dialogo di successo](assets/success.png)

1. Nella console Sites, i nuovi siti sono visibili e possono essere spostati per esplorare la struttura di base definita dal modello.

   ![Nuova struttura del sito](assets/new-site.png)

Gli autori dei contenuti possono ora iniziare a creare.

## È Richiesta Un&#39;Ulteriore Personalizzazione? {#customization-required}

I modelli di sito sono molto potenti e flessibili e è possibile creare qualsiasi numero per un progetto, consentendo di creare agevolmente varianti di sito. A seconda del livello di personalizzazione già eseguito sul modello di sito utilizzato, potrebbe non essere necessaria alcuna personalizzazione front-end aggiuntiva.

* Se il tuo sito non richiede una personalizzazione aggiuntiva, congratulazioni! Il tuo percorso finisce qui!
* Se hai ancora bisogno di una personalizzazione front-end aggiuntiva o se desideri semplicemente comprendere l’intero processo nel caso in cui ti occorra una personalizzazione futura, continua a leggere.

## Pagina di esempio {#example-page}

Se hai bisogno di ulteriori personalizzazioni front-end, ricorda che lo sviluppatore front-end potrebbe non avere familiarità con i dettagli del contenuto. Pertanto, è consigliabile fornire allo sviluppatore un percorso a contenuti tipici che possono essere utilizzati come base di riferimento in quanto il tema è personalizzato. Un esempio tipico è la home page della lingua master del sito.

1. Nel browser Sites individua la home page della lingua master del sito, quindi tocca o fai clic sulla pagina per selezionarla, quindi tocca o fai clic su **Modifica** nella barra dei menu.

   ![Pagina principale tipica](assets/home-page-in-console.png)

1. Nell’editor, seleziona la **Informazioni pagina** nella barra degli strumenti e quindi **Visualizza come pubblicato**.

   ![Modifica della home page](assets/home-page-edit.png)

1. Nella scheda visualizzata, copia il percorso del contenuto dalla barra degli indirizzi. Avrà un aspetto simile a `/content/<your-site>/en/home.html?wcmmode=disabled`.

   ![Home page](assets/home-page.png)

1. Salva il percorso da fornire successivamente allo sviluppatore front-end.

## Scarica il tema {#download-theme}

Ora che il sito è stato creato, il tema del sito generato dal modello può essere scaricato e fornito allo sviluppatore front-end per la personalizzazione.

1. Nella console Sites , mostra le **Sito** barra.

   ![Mostra barra dei siti](assets/show-site-rail.png)

1. Tocca o fai clic sulla directory principale del nuovo sito, quindi tocca o fai clic su **Scaricare le origini dei temi** nella barra del sito.

   ![Scaricare origini tema](assets/download-theme-sources.png)

Ora disponi di una copia dei file di origine del tema nei file di download.

## Configurazione utente proxy {#proxy-user}

Affinché lo sviluppatore front-end possa visualizzare in anteprima le personalizzazioni utilizzando il contenuto effettivo AEM dal sito, è necessario impostare un utente proxy.

1. In AEM dalla navigazione principale vai a **Strumenti** -> **Sicurezza** -> **Utenti**.
1. Nella console di gestione utenti, tocca o fai clic su **Crea**.

   ![Console di gestione utenti](assets/user-management-console.png)
1. In **Crea nuovo utente** finestra è necessario fornire almeno:
   * **ID** - Prendi nota di questo valore in quanto devi fornirlo allo sviluppatore front-end.
   * **Password** - Salvare questo valore in modo sicuro in un archivio password, in quanto è necessario fornirlo allo sviluppatore front-end.

   ![Nuovi dettagli utente](assets/new-user-details.png)

1. Sulla **Gruppi** aggiungi l&#39;utente proxy al `contributors` gruppo.
   * Digitazione del termine `contributors` attiva AEM funzione di completamento automatico per selezionare facilmente il gruppo.

   ![Aggiungi al gruppo](assets/add-to-group.png)

1. Tocca o fai clic su **Salva e chiudi**.

La configurazione è stata completata. Gli autori dei contenuti possono ora iniziare a creare contenuti nella preparazione del sito e iniziare a personalizzarli front-end nel passaggio successivo del percorso.

## Novità {#what-is-next}

Dopo aver completato questa parte del percorso di creazione siti rapidi AEM, è necessario:

* Scopri come ottenere AEM modelli di sito.
* Scopri come creare un nuovo sito utilizzando un modello.
* Scopri come scaricare il modello dal tuo nuovo sito per fornire allo sviluppatore front-end.

Sviluppare questa conoscenza e continuare il percorso di creazione siti rapida AEM revisione successiva del documento [Imposta La Pipeline,](pipeline-setup.md) dove creerai una pipeline front-end per gestire la personalizzazione del tema del sito.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso Creazione rapida siti esaminando il documento [Imposta La Pipeline,](pipeline-setup.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso.

* [Modello di sito standard AEM](https://github.com/adobe/aem-site-template-standard) - Questo è l’archivio GitHub del modello di sito standard AEM.
* [Creazione e organizzazione delle pagine](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) - Questa guida descrive come gestire le pagine del sito AEM se desideri personalizzarlo ulteriormente dopo averlo creato dal modello.
* [Come lavorare con il pacchetto](/help/implementing/developing/tools/package-manager.md) - I pacchetti consentono l&#39;importazione e l&#39;esportazione del contenuto del repository. Questo documento spiega come lavorare con i pacchetti nella AEM 6.5, che si applica anche ad AEMaaCS.
* [Documentazione sull’amministrazione del sito](/help/sites-cloud/administering/site-creation/create-site.md) - Per ulteriori informazioni sulle funzioni dello strumento Creazione rapida di siti, consultare i documenti tecnici sulla creazione del sito.
