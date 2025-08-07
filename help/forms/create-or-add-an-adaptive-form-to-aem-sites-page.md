---
title: Come si aggiunge un modulo adattivo alla pagina di AEM Sites?
description: Scopri come creare o aggiungere un modulo adattivo alla pagina AEM Sites. Scopri anche i vantaggi e i vari modi per integrare i moduli nel sito web.
feature: Adaptive Forms, Foundation Components
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
exl-id: a1846c5d-7b0f-4f48-9d15-96b2a8836a9d
role: User, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '3162'
ht-degree: 1%

---

# Aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

## Panoramica {#overview}

Con AEM Forms, puoi aggiungere facilmente un modulo alla pagina di AEM Sites. Questo consente ai visitatori di compilare e inviare i moduli in modo comodo, senza mai uscire dalla pagina in cui si trovano. In questo modo, possono rimanere coinvolti senza difficoltà con altri elementi del sito web interagendo attivamente con il modulo.

È possibile utilizzare l’Editor pagina di AEM per creare e aggiungere rapidamente più moduli alle pagine di AEM Sites. L’utilizzo dell’Editor pagina di AEM consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui comportamento dinamico, convalide, integrazione dei dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

AEM Forms Cloud Service fornisce i componenti Contenitore modulo adattivo e Forms adattivo - Incorpora. È possibile utilizzare il Contenitore di moduli adattivi per creare un modulo in una pagina o in un frammento di esperienza di AEM Sites, mentre il componente Forms adattivo - Incorpora consente di aggiungere un modulo adattivo esistente o di creare un modulo utilizzando l’editor di Forms adattivo.

![Esempio di modulo adattivo in una pagina AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

## Perché utilizzare i componenti core Forms adattivi per creare un modulo adattivo in una pagina o in un frammento di esperienza di AEM Sites?

Se in passato hai creato un componente Forms Foundation adattivo o moduli basati su HTML semplici per i siti, Adobe consiglia di utilizzare i componenti core Forms adattivi per creare un modulo adattivo nella pagina o nel frammento di esperienza di AEM Sites. Consente di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito, migliorando l’esperienza complessiva di creazione e gestione dei moduli per Adaptive Forms. Esaminiamo alcune di queste funzioni:

* **Controllo delle versioni:** le pagine AEM Sites offrono [solide funzionalità di controllo delle versioni](/help/sites-cloud/authoring/sites-console/page-versions.md), che consentono di tenere traccia e gestire versioni diverse dei moduli. In questo modo è possibile apportare modifiche e miglioramenti ai moduli mantenendo la possibilità di ripristinare le versioni precedenti, se necessario. Il controllo delle versioni garantisce un approccio controllato e organizzato allo sviluppo e all’evoluzione dei moduli.
* **Targeting (integrazione con Adobe Target):** Con le funzionalità di targeting delle pagine di AEM Sites, puoi anche [personalizzare l&#39;esperienza del modulo per tipi di pubblico diversi](/help/sites-cloud/integrating/integrating-adobe-target.md). Utilizzando i segmenti utente e i criteri di targeting, è possibile adattare il contenuto, la progettazione o il comportamento del modulo a specifici gruppi di utenti. Questo ti consente di fornire un’esperienza di modulo personalizzata e rilevante, aumentando i tassi di coinvolgimento e conversione.
* **Traduzione:** AEM Sites [integrazione perfetta con i servizi di traduzione](/help/sites-cloud/administering/translation/overview.md), che consente di tradurre facilmente i moduli in più lingue. Questa funzione semplifica il processo di localizzazione, garantendo che i moduli siano accessibili a un pubblico globale. Puoi gestire le traduzioni in modo efficiente all’interno dei progetti di traduzione AEM, riducendo il tempo e l’impegno necessari per il supporto di moduli multilingue. Consulta la sezione considerazioni per ulteriori informazioni sulla traduzione.
* **Gestione multisito e Live Copy:** AEM Sites fornisce [solide funzionalità di gestione multisito e Live Copy](/help/sites-cloud/administering/msm/overview.md), che consentono di creare e gestire più siti Web in un unico ambiente. Questa funzione consente ora di riutilizzare i moduli in siti diversi, garantendo coerenza e riducendo le attività di duplicazione. Grazie al controllo e alla gestione centralizzati, è possibile gestire e aggiornare in modo efficiente i moduli su più siti Web.
* **Temi:** le pagine AEM Sites forniscono un framework per la progettazione e la gestione di stili visivi coerenti su più pagine Web. Questi definiscono colori, font, fogli di stile e altri elementi visivi che contribuiscono all’aspetto generale del sito web. [Puoi utilizzare i temi progettati per una pagina AEM Sites per un modulo adattivo, risparmiando tempo e fatica](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes).
* **Assegnazione tag:** le pagine AEM Sites ti consentono di [assegnare tag o etichette a una pagina, una risorsa o altro contenuto](/help/implementing/developing/introduction/tagging-framework.md). I tag sono parole chiave o etichette di metadati che consentono di categorizzare e organizzare il contenuto in base a criteri specifici. Puoi assegnare uno o più tag a pagine, risorse o qualsiasi altro elemento di contenuto all’interno di AEM per migliorare la ricerca e classificare le risorse.
* **Blocco e sblocco del contenuto:** AEM Sites consente agli utenti di [controllare l&#39;accesso e le modifiche alle pagine](/help/sites-cloud/authoring/page-editor/edit-content.md) nell&#39;ambiente AEM Sites. Quando una pagina viene bloccata, significa che è protetta da modifiche o modifiche non autorizzate da parte di altri utenti. Solo l’utente che ha bloccato il contenuto o un amministratore designato può sbloccarlo per consentire modifiche.

Inoltre, Forms adattivo nell&#39;Editor pagina di AEM utilizza [Componenti core di Forms adattivo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it#features). Questi Componenti core forniscono metodi standard e più semplici per assegnare stili e personalizzare i componenti, identici a [Componenti AEM Sites WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it).


## Come si crea o si aggiunge un modulo adattivo nella pagina di AEM Sites o in un frammento di esperienza AEM? {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Puoi sfruttare appieno questa funzione utilizzando le seguenti opzioni:

* **[Crea e aggiungi un modulo adattivo personalizzato a una pagina di AEM Sites](#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Puoi utilizzare il componente Contenitore modulo adattivo per creare un modulo nuovo di zecca da zero, adattandolo in modo specifico ai tuoi requisiti e preferenze di progettazione.

* **[Crea e aggiungi un modulo adattivo personalizzato a un frammento di esperienza](#create-an-adaptive-form-in-sites-editor):** Puoi estendere la portata dei moduli aggiungendoli ai frammenti di esperienza AEM, in modo da riutilizzarli in più pagine o siti.

* **[Convertire un modulo adattivo in frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Convertire un modulo adattivo aggiunto a una pagina AEM Sites in un frammento di esperienza per riutilizzare il modulo in più pagine AEM Sites.

* **[Creazione e aggiunta di moduli basati su modelli approvati a una pagina di AEM Sites:](/help/forms/embed-adaptive-form-aem-sites.md#embed-form-using-adaptive-form-wizzard-aem-sites)** Puoi utilizzare modelli preapprovati per creare rapidamente Forms adattivo in linea con le linee guida di branding e gli standard di progettazione della tua organizzazione. L’opzione è disponibile solo per Forms adattivo creato con il componente Forms Editor adattivo o Forms adattivo - Incorpora.

* **[Aggiungi moduli esistenti a una pagina di AEM Sites:](/help/forms/embed-adaptive-form-aem-sites.md#embed-an-adaptive-form-in-sites-editor)** Puoi integrare facilmente nei tuoi siti Web i moduli già creati, consentendo ai visitatori di interagire direttamente con essi. L’opzione è disponibile solo per Forms adattivo creato con il componente Forms Editor adattivo o Forms adattivo - Incorpora.


* **Aggiungere più moduli a una pagina AEM Sites o a un frammento di esperienza:** È possibile creare o aggiungere più Forms adattivi a una pagina AEM Sites per fornire più scelte agli utenti in base alle loro preferenze e ai loro requisiti. Questi possono essere una combinazione di forme nuove di zecca da zero e moduli esistenti. Puoi utilizzare più volte il componente **[!UICONTROL Contenitore modulo adattivo]** per aggiungere Forms adattivo a una pagina di AEM Sites. Puoi utilizzare il componente **[!UICONTROL Forms adattivo - Incorpora]** più volte in una pagina di AEM Sites, solo se è selezionata l&#39;opzione **[!UICONTROL Modulo occupa l&#39;intera larghezza del frame]**. Se l&#39;opzione **[!UICONTROL Modulo occupa l&#39;intera larghezza del frame]** non è selezionata, la pagina di AEM Sites supporta un solo modulo adattivo per esistere senza un iframe. Per aggiungere altro Forms adattivo utilizzando il componente **[!UICONTROL Forms adattivo - Incorpora]**, seleziona **[!UICONTROL Il modulo copre l&#39;intera larghezza del frame]**.

## Considerazioni per la creazione di un modulo adattivo in una pagina AEM Sites o in un frammento di esperienza AEM {#consideration}

* Quando utilizzi il Contenitore di moduli adattivi per creare o aggiungere un modulo, i moduli vengono tradotti e localizzati attraverso il flusso di traduzione AEM Sites. Per ogni lingua viene generata una copia separata (copia per lingua) della pagina del sito e dei moduli corrispondenti e, quando un autore di contenuto modifica una regola in un modulo nella pagina padre, le stesse modifiche devono essere apportate in tutte le copie per lingua del modulo. Il Contenitore di moduli adattivi consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

* Quando crei o aggiungi un modulo utilizzando il componente di incorporamento modulo adattivo, i moduli vengono tradotti e localizzati utilizzando il flusso di traduzione AEM Forms. In questo caso, viene mantenuto un singolo modulo a cui viene fatto riferimento in tutte le copie in lingua delle pagine di Sites. Il componente per l’incorporamento di moduli adattivi non fornisce l’accesso a varie funzioni delle pagine AEM Sites come, controllo delle versioni, targeting, traduzione e gestione multisito.


## Requisiti per la creazione o l’aggiunta di un modulo adattivo nella pagina di AEM Sites o nel frammento di esperienza di AEM {#before-you-start-creating-an-adaptive-form}

Prima di iniziare a creare un modulo adattivo, abilita i componenti core Forms adattivi e aggiungi le librerie client Forms adattivi alla pagina AEM Sites:

### Abilitare i componenti core adattivi di Forms per il tuo ambiente AEM Cloud Service

Assicurati che i [Componenti core adattivi di Forms siano abilitati per il tuo ambiente AEM Forms as a Cloud Service](enable-adaptive-forms-core-components.md).

### Aggiungere librerie client Forms adattive alla pagina o al frammento di esperienza AEM Sites

Per abilitare la funzionalità completa del componente Contenitore Forms adattivo, aggiungi le librerie client Customheaderlibs e Customfooterlibs alla pagina AEM Sites utilizzando la pipeline di distribuzione. Per aggiungere le librerie:

1. Accedi e clona l&#39;[archivio Git AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=it).
1. Apri la cartella dell’archivio Git di AEM Cloud Service in un editor di testo del piano. Ad esempio, Codice visivo Microsoft.
1. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` e aggiungere il codice seguente al file:

   ```
       //Customheaderlibs.html
   
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` e aggiungere il codice seguente al file:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` e aggiungere il codice seguente al file:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Aprire il file `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` e aggiungere il codice seguente al file:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [Esegui la pipeline di distribuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=it) per distribuire le librerie client nell&#39;ambiente AEM as a Cloud Service.

### Abilita Adaptive Forms Container per la pagina o il frammento di esperienza AEM Sites

Per abilitare il componente [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, eseguire la procedura seguente:

1. Apri la pagina AEM Sites o il frammento di esperienza per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su Modifica.
1. Apri il modello della pagina Sites o Frammento esperienza. Per aprire il modello, vai a [!UICONTROL Informazioni pagina] ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Modifica modello]. Apre il modello corrispondente nell’editor modelli.
1. Nella visualizzazione Struttura fare clic sull&#39;icona **[!UICONTROL Criteri]** ![Criteri](/help/forms/assets/Smock_FeedManagement_18_N.svg) nella barra dei menu. Nell&#39;elenco **[!UICONTROL Componenti consentiti]** e selezionare la casella di controllo **[!UICONTROL Contenitore Forms adattivo]** in **[Nome progetto Archetipo AEM] - Modulo adattivo**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Creare un modulo adattivo {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Puoi creare un nuovo modulo da zero, adattandolo in modo specifico ai tuoi requisiti e alle preferenze di progettazione, direttamente in una pagina di AEM Sites o in Frammento di esperienza. Per i moduli monouso, si consiglia di creare direttamente una pagina di AEM Sites, mentre i frammenti di esperienza sono ideali per i moduli che devono essere riutilizzati in più pagine del sito web.

* [Creare un modulo in una pagina di AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creare un modulo in un frammento di esperienza](#create-an-adaptive-form-in-experience-fragment)
* [Convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Creare un modulo in una pagina di AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puoi utilizzare il componente Contenitore modulo adattivo nell’Editor pagina di AEM per creare un modulo personalizzato. Il componente consente di creare un modulo trascinandone e rilasciandone i componenti. I componenti del modulo sono basati su Componenti core. Puoi personalizzarli facilmente in base alle esigenze della tua organizzazione.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Per creare un modulo adattivo in una pagina Sites:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Trascina il componente **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti alla pagina Sites. Crea uno spazio nella pagina per il modulo. Puoi utilizzare la modalità layout per modificare la dimensione dello spazio del contenitore.
1. Trascina i componenti core modulo adattivo nello spazio contenitore per creare il modulo.
1. Aggiungi il pulsante Invia.

Successivamente, [impostare l&#39;azione di invio](#configure-submit-action-for-form) e le proprietà avanzate.

### Creare un modulo in un frammento esperienza {#create-an-adaptive-form-in-experience-fragment}

Puoi estendere la portata dei moduli aggiungendoli a Frammenti esperienza AEM, per consentirne il riutilizzo su più pagine o siti. Ad esempio, puoi includere un modulo di iscrizione a una newsletter all’interno di un frammento di esperienza. In questo modo è possibile riutilizzare il frammento in più pagine del sito Web, eliminando la necessità di ricreare ripetutamente il modulo. Eventuali aggiornamenti o modifiche apportate al modulo di iscrizione alla newsletter all’interno del frammento di esperienza vengono propagate automaticamente a tutte le pagine in cui viene utilizzato. Questo semplifica il processo e garantisce un’esperienza utente fluida, semplificando al contempo la gestione dei moduli del sito web.

Per creare un modulo adattivo in un frammento di esperienza:

1. Apri un frammento di esperienza.
1. Trascina il componente **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti al frammento di esperienza.
1. Per creare il modulo, trascina i componenti core modulo adattivo nello spazio contenitore nel frammento di esperienza.
1. Aggiungi il pulsante Invia.

Successivamente, [impostare l&#39;azione di invio](#configure-submit-action-for-form) e le proprietà avanzate.

### Convertire un modulo in una pagina di AEM Sites in un frammento di esperienza {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

È possibile convertire un modulo adattivo esistente in un editor di pagine Sites in un frammento di esperienza per riutilizzare il modulo in più pagine o siti.

Per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza:

1. Apri la pagina AEM Sites contenente il modulo adattivo (nel componente Contenitore Forms adattivo) in modalità di modifica.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Sulla barra dei menu, seleziona l&#39;icona ![Converti in frammento di esperienza](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Converti in variante di frammento di esperienza.
   ![Fai clic sul logo dell&#39;archivio file per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Viene visualizzata una finestra di dialogo per convertire il contenitore Moduli adattivi in un nuovo frammento di esperienza o aggiungerlo a un frammento di esperienza esistente
1. Nella finestra di dialogo Converti in variante di frammento di esperienza, imposta i valori per le seguenti opzioni:

   * **Azione:** Seleziona questa opzione per creare un frammento di esperienza o Aggiungi a un frammento di esperienza esistente.
   * **Percorso principale:** Specificare il percorso della cartella in cui ospitare il frammento di esperienza. L’opzione è disponibile solo per la creazione di un frammento di esperienza.
   * **Modello:** Specifica il percorso del modello Frammento esperienza. Se non disponi di un modello di Frammento esperienza, [crealo](/help/implementing/developing/extending/experience-fragments.md). L’opzione è disponibile solo per aggiungere un modulo adattivo a un frammento di esperienza esistente.
   * **Titolo frammento:** Specifica il titolo del frammento esperienza. Il titolo identifica in modo univoco un frammento esperienza


## Configurare l’azione di invio per un modulo nella pagina o nel frammento di esperienza di AEM Sites {#configure-submit-action-for-form}

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante Invia in un modulo adattivo. I moduli adattivi includono alcune azioni di invio pronte all’uso. Puoi anche estendere un’azione di invio predefinita per creare un’azione di invio personalizzata. Per configurare un&#39;azione di invio per il modulo:

1. Apri l’Editor pagina di AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo con cui configurare le azioni di invio.
   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare l&#39;azione di invio per un modulo adattivo](/help/forms/assets/adaptive-forms-container.png)
1. Seleziona e configura un’azione Invia in base alle tue esigenze. Per informazioni dettagliate sulle azioni di invio, consulta [Azione di invio modulo adattivo](/help/forms/configuring-submit-actions.md)


## Configurare uno schema o un modello dati modulo (FDM) per un modulo nella pagina o nel frammento di esperienza di AEM Sites {#configure-schema-or-data-model-for-form}

È possibile utilizzare il modello dati modulo (FDM) per collegare un modulo a un Source dati per inviare e ricevere dati in base alle azioni degli utenti. È possibile anche collegare un modulo a uno schema JSON per ricevere i dati inviati in un formato predefinito. In base al requisito, connetti il modulo a uno schema JSON o a un modello di dati del modulo (FDM):

* [Creare uno schema JSON e caricarlo nell&#39;ambiente](/help/forms/adaptive-form-json-schema-form-model.md) oppure
* [Creare un modello dati modulo (FDM)](/help/forms/create-form-data-models.md)

Per configurare uno schema JSON o un modello dati modulo (FDM) per il modulo:

1. Apri l’Editor pagina di AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull&#39;icona chiave inglese per configurare un modello dati per il modulo adattivo](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. Seleziona e configura uno schema JSON o un modello dati modulo (FDM), in base ai requisiti. Per informazioni dettagliate sulle azioni di invio, vedere [Azione di invio modulo adattivo](/help/forms/configuring-submit-actions.md).

   * Quando si seleziona l&#39;opzione **[!UICONTROL Modello modulo]**, utilizzare l&#39;opzione **[!UICONTROL Seleziona modello dati modulo]** per selezionare un modello dati modulo (FDM) preconfigurato.
   * Quando selezioni l&#39;opzione **[!UICONTROL Schema]**, utilizza l&#39;opzione **[!UICONTROL Schema]** per selezionare uno schema JSON per il modulo.

1. Fai clic su **[!UICONTROL Fine]**.

## Configurare un servizio di precompilazione per un modulo nella pagina o nel frammento di esperienza di AEM Sites {#configure-prefill-service-for-form}

Puoi utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Operazioni disponibili:

* [Creare un servizio di precompilazione personalizzato](/help/forms/prepopulate-adaptive-form-fields.md)
* [Utilizza il servizio di precompilazione del modello dati del modulo](#fdm-prefill-service)

### Utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo nella pagina o nel frammento di esperienza di AEM Sites {#fdm-prefill-service}

È possibile utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo in una pagina di AEM Sites o in un frammento di esperienza utilizzando un modello dati modulo o un servizio di precompilazione personalizzato. Il servizio di precompilazione del modello dati modulo utilizza il servizio [Get Service del modello dati modulo configurato](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) per recuperare i dati. Per utilizzare il servizio di precompilazione del modello dati modulo per un modulo adattivo:

1. Apri l’Editor pagina di AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare il servizio di precompilazione per il modulo adattivo](/help/forms/assets/adaptive-forms-container.png)
1. Seleziona un modello di dati modulo. Apri la scheda **[!UICONTROL Base]**. Nel servizio di precompilazione, selezionare **[!UICONTROL Servizio di precompilazione modello dati modulo]**.
1. Fai clic su **[!UICONTROL Fine]**. Il modulo adattivo è ora configurato per l’utilizzo della precompilazione del modello dati del modulo. Ora puoi utilizzare l&#39;[editor regole](rule-editor.md) per creare regole per precompilare i campi del modulo.


## Reindirizza l’utente a una pagina o mostra un messaggio di ringraziamento all’invio del modulo

All&#39;invio di un modulo è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o a un messaggio. Per reindirizzare l’utente o configurare il messaggio di ringraziamento:

1. Apri l’Editor pagina di AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.

1. Apri la scheda **[!UICONTROL Invio]**.

   * Per configurare un URL di reindirizzamento, per l&#39;opzione Invia selezionare l&#39;opzione **[!UICONTROL Reindirizza all&#39;URL]**, quindi sfogliare e selezionare una pagina AEM Sites o specificare l&#39;URL di una pagina esterna.
   * Per configurare un messaggio personalizzato o di ringraziamento, per l&#39;opzione Invia selezionare l&#39;opzione **[!UICONTROL Mostra messaggio]** e specificare un messaggio nella casella **[!UICONTROL Contenuto messaggio]**. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.


