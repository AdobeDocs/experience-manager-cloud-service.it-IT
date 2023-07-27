---
title: Come si aggiunge un modulo adattivo alla pagina di AEM Sites?
description: Scopri come creare o aggiungere un modulo adattivo alla pagina AEM Sites. Scopri anche i vantaggi e i vari modi per integrare i moduli nel sito web.
feature: Adaptive Forms, Page Editor, Authoring
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
source-git-commit: 991de20303380af76d3e2e97aca8e0a4373e2232
workflow-type: tm+mt
source-wordcount: '3214'
ht-degree: 0%

---


# Aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |
| AEM as a Cloud Service | Questo articolo |

Con AEM Forms, puoi aggiungere facilmente un modulo alla pagina di AEM Sites. Questo consente ai visitatori di compilare e inviare i moduli in modo comodo, senza mai uscire dalla pagina in cui si trovano. In questo modo, possono rimanere coinvolti senza difficoltà con altri elementi del sito web interagendo attivamente con il modulo.

È possibile utilizzare l’Editor pagina AEM per creare e aggiungere rapidamente più moduli alle pagine AEM Sites. L’editor di pagine AEM consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites, sfruttando la potenza dei componenti per moduli adattivi, tra cui comportamento dinamico, convalide, integrazione dei dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

Il Cloud Service AEM Forms fornisce i componenti Contenitore modulo adattivo e Forms adattivo - Incorpora. È possibile utilizzare il Contenitore di moduli adattivi per creare un nuovo modulo in una pagina o in un frammento di esperienza di AEM Sites, mentre il componente Incorpora di Forms adattivo consente di aggiungere un modulo adattivo esistente o crearne uno nuovo tramite l’editor di Forms adattivo.

![Esempio di modulo adattivo in una pagina AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

## Perché utilizzare i componenti core Forms adattivi per creare un modulo adattivo in una pagina o in un frammento di esperienza di AEM Sites?

Se in passato hai creato un componente Forms Foundation adattivo o moduli semplici basati su HTML per i siti, l’Adobe consiglia di utilizzare i componenti core Forms adattivi per creare un modulo adattivo nella pagina o nel frammento di esperienza di AEM Sites. Consente di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito, migliorando l’esperienza complessiva di creazione e gestione dei moduli per Adaptive Forms. Esaminiamo alcune di queste funzioni:

* **Controllo delle versioni:** Offerta pagine AEM Sites [solide funzionalità di controllo delle versioni](/help/sites-cloud/authoring/features/page-versions.md), che consente di tenere traccia e gestire diverse versioni dei moduli. In questo modo è possibile apportare modifiche e miglioramenti ai moduli mantenendo la possibilità di ripristinare le versioni precedenti, se necessario. Il controllo delle versioni garantisce un approccio controllato e organizzato allo sviluppo e all’evoluzione dei moduli.
* **Targeting (integrazione con Adobe Target):** Con le funzionalità di targeting delle pagine di AEM Sites, puoi anche [personalizzare l’esperienza del modulo per diversi tipi di pubblico](/help/sites-cloud/integrating/integration-adobe-target-ims.md). Sfruttando i segmenti utente e i criteri di targeting, è possibile adattare il contenuto, la progettazione o il comportamento del modulo a specifici gruppi di utenti. Questo ti consente di fornire un’esperienza di modulo personalizzata e rilevante, aumentando i tassi di coinvolgimento e conversione.
* **Traduzione:** AEM Sites [integrazione perfetta con i servizi di traduzione](/help/sites-cloud/administering/translation/overview.md), che consente di tradurre facilmente i moduli in più lingue. Questa funzione semplifica il processo di localizzazione, garantendo che i moduli siano accessibili a un pubblico globale. Puoi gestire le traduzioni in modo efficiente all’interno dei progetti di traduzione AEM, riducendo il tempo e l’impegno necessari per il supporto di moduli multilingue. Consulta la sezione considerazioni per ulteriori informazioni sulla traduzione.
* **Gestione multisito e Live Copy:** AEM Sites fornisce una solida [Funzionalità di gestione multisito e Live Copy](/help/sites-cloud/administering/msm/overview.md), che consente di creare e gestire più siti web all’interno di un unico ambiente. Questa funzione consente ora di riutilizzare i moduli in siti diversi, garantendo coerenza e riducendo le attività di duplicazione. Grazie al controllo e alla gestione centralizzati, è possibile gestire e aggiornare in modo efficiente i moduli su più siti Web.
* **Temi:** Le pagine AEM Sites forniscono un framework per progettare e mantenere stili visivi coerenti su più pagine web. Questi definiscono colori, font, fogli di stile e altri elementi visivi che contribuiscono all’aspetto generale del sito web. [Puoi utilizzare i temi progettati per una pagina AEM Sites per un modulo adattivo, risparmiando tempo e fatica](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes).
* **Assegnazione tag:** Le pagine di AEM Sites consentono di: [assegnare tag o etichette a una pagina, una risorsa o altro contenuto](/help/implementing/developing/introduction/tagging-framework.md). I tag sono parole chiave o etichette di metadati che consentono di categorizzare e organizzare il contenuto in base a criteri specifici. Puoi assegnare uno o più tag a pagine, risorse o qualsiasi altro elemento di contenuto all’interno di AEM per migliorare la ricerca e classificare le risorse.
* **Blocco e sblocco del contenuto:** AEM Sites consenti agli utenti di [controllare l’accesso e le modifiche alle pagine](/help/sites-cloud/authoring/fundamentals/editing-content.md) nell’ambiente AEM Sites. Quando una pagina viene bloccata, significa che è protetta da modifiche o modifiche non autorizzate da parte di altri utenti. Solo l’utente che ha bloccato il contenuto o un amministratore designato può sbloccarlo per consentire modifiche.

Inoltre, Forms adattivo nell’Editor pagina AEM utilizza [Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features). Questi Componenti core forniscono metodi standard e più semplici per assegnare stili e personalizzare i componenti, identici a [Componenti WCM di AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it).


## Come si crea o si aggiunge un modulo adattivo nella pagina di AEM Sites o in un frammento di esperienza AEM? {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Puoi sfruttare appieno questa funzione utilizzando le seguenti opzioni:

* **[Creare e aggiungere un modulo adattivo personalizzato a una pagina AEM Sites](#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Puoi utilizzare il componente Contenitore modulo adattivo per creare un modulo nuovo di zecca da zero, personalizzandolo in base a specifici requisiti e preferenze di progettazione.

* **[Creare e aggiungere un modulo adattivo personalizzato a un frammento di esperienza](#create-an-adaptive-form-in-sites-editor):** Puoi estendere la portata dei moduli aggiungendoli ai Frammenti esperienza AEM per consentirne il riutilizzo su più pagine o siti.

* **[Convertire un modulo adattivo in frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Converti un modulo adattivo aggiunto a una pagina AEM Sites in un frammento di esperienza per riutilizzare il modulo su più pagine AEM Sites.

* **Aggiungere più moduli a una pagina o a un frammento di esperienza di AEM Sites:**  Puoi creare o aggiungere più Forms adattivi a una pagina AEM Sites per fornire più scelte agli utenti in base alle loro preferenze e ai loro requisiti. Questi possono essere una combinazione di forme nuove di zecca da zero e moduli esistenti.

* **Creare e aggiungere moduli basati su modelli approvati a una pagina AEM Sites:** Puoi sfruttare i modelli pre-approvati per creare rapidamente Forms adattivi in linea con le linee guida di branding e gli standard di progettazione della tua organizzazione. L’opzione è disponibile solo per Forms adattivo creato con il componente Forms Editor adattivo o Forms adattivo - Incorpora.

* **Aggiungere moduli esistenti a una pagina AEM Sites:** Puoi integrare facilmente nei tuoi siti web i moduli già creati, consentendo ai visitatori di interagire direttamente con essi. L’opzione è disponibile solo per Forms adattivo creato con il componente Forms Editor adattivo o Forms adattivo - Incorpora.

## Considerazioni per la creazione di un modulo adattivo nella pagina di AEM Sites o nel frammento di esperienza AEM {#consideration}

* Quando utilizzi il Contenitore di moduli adattivi per creare o aggiungere un modulo, i moduli vengono tradotti e localizzati attraverso il flusso di traduzione AEM Sites. Per ogni lingua viene generata una copia separata (copia per lingua) della pagina del sito e dei moduli corrispondenti e, quando un autore di contenuto modifica una regola in un modulo nella pagina padre, le stesse modifiche devono essere apportate in tutte le copie per lingua del modulo. Il Contenitore di moduli adattivi consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

* Quando crei o aggiungi un modulo utilizzando il componente di incorporamento modulo adattivo, i moduli vengono tradotti e localizzati utilizzando il flusso di traduzione AEM Forms. In questo caso, viene mantenuto un singolo modulo a cui viene fatto riferimento in tutte le copie in lingua delle pagine di Sites. Il componente per l’incorporamento di moduli adattivi non fornisce l’accesso a varie funzioni delle pagine AEM Sites come, controllo delle versioni, targeting, traduzione e gestione multisito.


## Requisiti per la creazione o l’aggiunta di un modulo adattivo nella pagina di AEM Sites o nel frammento di esperienza AEM {#before-you-start-creating-an-adaptive-form}

Prima di iniziare a creare un modulo adattivo, abilita i componenti core Forms adattivi e aggiungi le librerie client Forms adattivi alla pagina AEM Sites:

+++  Abilitare i componenti core Forms adattivi per il tuo ambiente AEM Cloud Service

Assicurati che [I componenti core Forms adattivi sono abilitati per l’ambiente AEM Forms as a Cloud Service](enable-adaptive-forms-core-components.md).

+++

+++  Aggiungere librerie client Forms adattive alla pagina o al frammento di esperienza AEM Sites

Per abilitare la funzionalità completa del componente Contenitore Forms adattivo, aggiungi le librerie client Customheaderlibs e Customfooterlibs alla pagina AEM Sites utilizzando la pipeline di distribuzione. Per aggiungere le librerie:

1. Accedere e clonare [Archivio Git AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Apri la cartella AEM Cloud Service Git Repository in un editor di testo per piani. Ad esempio, Codice visivo Microsoft.
1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` e aggiungi al file il seguente codice:

       &quot;
       //Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;
   
1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` e aggiungi al file il seguente codice:

       &quot;
       
       //customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;
   
1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` e aggiungi al file il seguente codice:

       &quot;
       //Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;
   
1. Apri `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` e aggiungi al file il seguente codice:

       &quot;
       
       //customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;
   
1. [Eseguire la pipeline di distribuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) per distribuire le librerie client nell’ambiente AEM as a Cloud Service.

+++

+++ Abilita Adaptive Forms Container per la pagina o il frammento di esperienza AEM Sites

Per abilitare [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites o il frammento di esperienza per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su Modifica.
1. Apri il modello della pagina Sites o Frammento esperienza. Per aprire il modello, passare alla [!UICONTROL Informazioni pagina] ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Modifica modello]. Apre il modello corrispondente nell’editor modelli.
1. Nella vista Struttura, fare clic sul pulsante **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) nella barra dei menu. In **[!UICONTROL Componenti consentiti]** e seleziona la **[!UICONTROL Contenitore Forms adattivo]**  casella di controllo sotto **[Nome progetto archetipo AEM] - Modulo adattivo**.
1. Clic **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Creare un modulo adattivo {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Puoi creare un nuovo modulo da zero, adattandolo in modo specifico ai tuoi requisiti e alle preferenze di progettazione, direttamente in una pagina di AEM Sites o in Frammento di esperienza. Per i moduli monouso, si consiglia di creare direttamente una pagina di AEM Sites, mentre i frammenti di esperienza sono ideali per i moduli che devono essere riutilizzati in più pagine del sito web.

* [Creare un modulo in una pagina di AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creare un modulo in un frammento esperienza](#create-an-adaptive-form-in-experience-fragment)
* [Convertire un modulo adattivo in una pagina di AEM Sites in un frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Creare un modulo in una pagina di AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puoi utilizzare il componente Contenitore modulo adattivo nell’Editor pagina AEM per creare un modulo personalizzato. Il componente consente di creare un modulo trascinandone e rilasciandone i componenti. I componenti del modulo sono basati su Componenti core. Puoi personalizzarli facilmente in base alle esigenze della tua organizzazione.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Per creare un modulo adattivo in una pagina Sites:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Trascina la selezione **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti alla pagina Sites. Crea uno spazio nella pagina per il modulo. Puoi utilizzare la modalità layout per modificare la dimensione dello spazio del contenitore.
1. Trascina i componenti core modulo adattivo nello spazio contenitore per creare il modulo.
1. Aggiungi il pulsante Invia.

Poi, tu [impostare l&#39;azione di invio](#configure-submit-action-for-form) e proprietà avanzate.

### Creare un modulo in un frammento esperienza {#create-an-adaptive-form-in-experience-fragment}

Puoi estendere la portata dei moduli aggiungendoli ai Frammenti esperienza AEM per consentirne il riutilizzo su più pagine o siti. Ad esempio, puoi includere un modulo di iscrizione a una newsletter all’interno di un frammento di esperienza. Questo consente di riutilizzare in modo comodo il frammento su più pagine del sito web, eliminando la necessità di ricreare ripetutamente il modulo. Eventuali aggiornamenti o modifiche apportate al modulo di iscrizione alla newsletter all’interno del frammento di esperienza vengono propagate automaticamente a tutte le pagine in cui viene utilizzato. Questo semplifica il processo e garantisce un’esperienza utente fluida, semplificando al contempo la gestione dei moduli del sito web.

Per creare un modulo adattivo in un frammento di esperienza:

1. Apri un frammento di esperienza.
1. Trascina la selezione **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti al frammento di esperienza.
1. Per creare il modulo, trascina i componenti core modulo adattivo nello spazio contenitore nel frammento di esperienza.
1. Aggiungi il pulsante Invia.

Poi, tu [impostare l&#39;azione di invio](#configure-submit-action-for-form) e proprietà avanzate.

### Convertire un modulo in una pagina di AEM Sites in un frammento di esperienza {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

È possibile convertire un modulo adattivo esistente in un editor di pagine Sites in un frammento di esperienza per riutilizzare il modulo in più pagine o siti.

Per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza:

1. Apri la pagina AEM Sites contenente il modulo adattivo (nel componente Contenitore Forms adattivo) in modalità di modifica.
1. Apri la Struttura contenuto e seleziona la **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Nella barra dei menu, seleziona ![Icona Converti in frammento esperienza](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Icona Converti in variante di frammento esperienza.
   ![Fai clic sul logo dell’archivio file per convertire un modulo adattivo nella pagina AEM Sites in un frammento di esperienza](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Viene visualizzata una finestra di dialogo per convertire il contenitore Moduli adattivi in un nuovo frammento di esperienza o aggiungerlo a un frammento di esperienza esistente
1. Nella finestra di dialogo Converti in variante di frammento di esperienza, imposta i valori per le seguenti opzioni:

   * **Azione:** Seleziona per creare un nuovo frammento di esperienza o Aggiungi a un frammento di esperienza esistente.
   * **Percorso principale:** Specifica il percorso della cartella in cui ospitare il frammento di esperienza. L’opzione è disponibile solo per la creazione di un nuovo frammento di esperienza.
   * **Modello:** Specifica il percorso del modello Frammento esperienza. Se non disponi di un modello Frammento esperienza, [crearlo](/help/implementing/developing/extending/experience-fragments.md). L’opzione è disponibile solo per aggiungere un modulo adattivo a un frammento di esperienza esistente.
   * **Titolo frammento:** Specifica il titolo del frammento di esperienza. Il titolo identifica in modo univoco un frammento esperienza


## Configurare l’azione di invio per un modulo nella pagina o nel frammento di esperienza di AEM Sites {#configure-submit-action-for-form}

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante Invia in un modulo adattivo. I moduli adattivi includono alcune azioni di invio pronte all’uso. Puoi anche estendere un’azione di invio predefinita per creare un’azione di invio personalizzata. Per configurare un&#39;azione di invio per il modulo:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona la **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sulle proprietà Contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo con cui configurare le azioni di invio.
   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare l’azione di invio per un modulo adattivo](/help/forms/assets/adaptive-forms-container.png)
1. Seleziona e configura un’azione Invia in base alle tue esigenze. Per informazioni dettagliate sulle azioni di invio, vedere [Azione di invio modulo adattivo](/help/forms/configuring-submit-actions.md)


## Configurare uno schema o un modello di dati modulo per un modulo nella pagina o nel frammento di esperienza di AEM Sites {#configure-schema-or-data-model-for-form}

È possibile utilizzare il modello dati modulo per collegare un modulo a un&#39;origine dati per inviare e ricevere dati in base alle azioni degli utenti. Puoi anche collegare un modulo a uno schema JSON per ricevere i dati inviati in un formato predefinito. In base al requisito, connetti il modulo a uno schema JSON o a un modello di dati del modulo:

* [Creare uno schema JSON e caricarlo nell’ambiente](/help/forms/adaptive-form-json-schema-form-model.md)  oppure
* [Creare un modello di dati modulo](/help/forms/create-form-data-models.md)

Per configurare uno schema JSON o un modello dati modulo per il modulo:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona la **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sulle proprietà Contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull’icona chiave inglese per configurare un modello dati per il modulo adattivo](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. Seleziona e configura uno schema JSON o un modello dati modulo, in base ai requisiti. Per informazioni dettagliate sulle azioni di invio, vedere [Azione di invio modulo adattivo](/help/forms/configuring-submit-actions.md).

   * Quando selezioni il **[!UICONTROL Modello modulo]** , utilizza **[!UICONTROL Seleziona modello dati modulo]** per selezionare un modello di dati modulo preconfigurato.
   * Quando selezioni il **[!UICONTROL Schema]** , utilizza **[!UICONTROL Schema]** per selezionare uno schema JSON per il modulo.

1. Clic **[!UICONTROL Fine]**.

## Configurare un servizio di precompilazione per un modulo nella pagina o nel frammento di esperienza di AEM Sites {#configure-prefill-service-for-form}

Puoi utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Operazioni disponibili:

* [Creare un servizio di precompilazione personalizzato](/help/forms/prepopulate-adaptive-form-fields.md)
* [Utilizza il servizio di precompilazione del modello dati del modulo](#fdm-prefill-service)

### Utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo nella pagina o nel frammento di esperienza di AEM Sites {#fdm-prefill-service}

È possibile utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo in una pagina di AEM Sites o in un frammento di esperienza utilizzando un modello dati modulo o un servizio di precompilazione personalizzato. Il servizio di precompilazione del modello dati del modulo utilizza [Ottieni il servizio del modello di dati del modulo configurato](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) per recuperare i dati. Per utilizzare il servizio di precompilazione del modello dati modulo per un modulo adattivo:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona la **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sulle proprietà Contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare il servizio di precompilazione per il modulo adattivo](/help/forms/assets/adaptive-forms-container.png)
1. Seleziona un modello di dati modulo. Apri **[!UICONTROL Base]** scheda. Nel servizio di preriempimento, seleziona **[!UICONTROL Servizio preriempimento modello dati modulo]**.
1. Clic **[!UICONTROL Fine]**. Il modulo adattivo è ora configurato per l’utilizzo della precompilazione del modello dati del modulo. Ora è possibile utilizzare [editor di regole](rule-editor.md) per creare regole per precompilare i campi del modulo.


## Reindirizza l’utente a una pagina o mostra un messaggio di ringraziamento all’invio del modulo

All&#39;invio di un modulo è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o a un messaggio. Per reindirizzare l’utente o configurare il messaggio di ringraziamento:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona la **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.

1. Apri **[!UICONTROL Invio]** scheda.

   * Per configurare un URL di reindirizzamento, per l’opzione Invia seleziona la **[!UICONTROL Reindirizza a URL]** e sfoglia e seleziona una pagina AEM Sites oppure specifica l’URL di una pagina esterna.

   * Per configurare un messaggio personalizzato o di ringraziamento, per all’opzione Invia, seleziona la **[!UICONTROL Mostra messaggio]** e inserisci un messaggio nella sezione **[!UICONTROL Contenuto del messaggio]** casella. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.

## Vedi successivo

* [Creare stili o temi per i moduli](using-themes-in-core-components.md)
* [Aggiungere un comportamento dinamico ai moduli tramite l’editor di regole](rule-editor.md)
* [Impostare il layout dei moduli per dimensioni di schermo e tipi di dispositivi diversi](/help/sites-cloud/authoring/features/responsive-layout.md)


## Articolo correlato {#related-article}

* [Creare un modulo adattivo basato su Componenti core autonomi](/help/forms/creating-adaptive-form-core-components.md)
