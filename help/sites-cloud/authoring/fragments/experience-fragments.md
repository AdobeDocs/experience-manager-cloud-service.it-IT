---
title: Frammenti di esperienza
description: Utilizza Frammenti di esperienza in Adobe Experience Manager as a Cloud Service per rendere le tue esperienze riutilizzabili e flessibili.
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
solution: Experience Manager Sites
feature: Authoring, Experience Fragments
role: User
source-git-commit: 5578cfd1bbe91d904d3f36b67acf610f9196cb7d
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 90%

---

# Frammenti di esperienza {#experience-fragments}

In Adobe Experience Manager as a Cloud Service, un frammento esperienza:

* è un gruppo di uno o più componenti;
* include sia contenuto che layout;
* può essere aggiunto come riferimento nelle pagine;
* può contenere qualsiasi componente.

Un frammento di esperienza:

* è parte di un’esperienza (pagina).
* Può essere utilizzato su più pagine (basate su modelli modificabili).
* Si basa su un modello (solo modificabile) che ne definisce struttura e componenti.
* Questo modello viene utilizzato per creare la *pagina root* del frammento di esperienza.
* È costituito da uno o più componenti, con layout, in un sistema paragrafo.
* Può contenere altri frammenti di esperienza.
* Può essere combinato con altri componenti (inclusi altri frammenti esperienza) per formare una pagina completa (esperienza).
* Puoi creare una o più varianti in base alla pagina root.
* Queste varianti possono condividere contenuti e/o componenti.
* Può essere suddiviso in blocchi predefiniti che possono essere utilizzati in più varianti del frammento.

Puoi utilizzare Frammenti esperienza:

* Se un autore desidera riutilizzare parti (un frammento di un’esperienza) di una pagina.
Senza Frammenti esperienza, l’autore dovrebbe copiare e incollare tale frammento. Creare e gestire queste esperienze di copia/incolla richiede tempo e può essere fonte di errori da parte dell’utente.
Grazie a Frammenti esperienza non è più necessario eseguire operazioni di copia/incolla.
* Per supportare il caso d’uso del CMS headless.
Gli autori intendono utilizzare AEM solo per l’authoring, ma non per la distribuzione al cliente. Un sistema/punto di contatto di terze parti utilizzerebbe tale esperienza e quindi la consegnerebbe all’utente.
* Con [Gestione multisito (MSM)](/help/sites-cloud/administering/msm/overview.md); come frammento di esperienza fa parte di una pagina. Questo vale sia per i singoli frammenti che per le cartelle in cui risiedono.

>[!NOTE]
>
>I **[frammenti di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md)** e i **frammenti di esperienza** sono funzioni diverse in AEM:
>* I **frammenti di contenuto** sono contenuti editoriali, con definizione e struttura, ma senza elementi visivi aggiuntivi di design e/o layout. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, consulta [Frammenti di contenuto e frammenti di esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=it#content-fragments).

>[!NOTE]
>
>Per poter accedere in scrittura ai frammenti esperienza, l’account utente deve essere registrato nel gruppo:
>
>* `experience-fragments-editors`
>
>Se riscontri problemi, contatta l’amministratore di sistema.

## Quando utilizzare i frammenti esperienza?   {#when-should-you-use-experience-fragments}

I Frammenti di esperienza sono indicati nei seguenti casi:

* Quando desideri riutilizzare le esperienze.
   * Per esperienze che riutilizzerai con contenuti simili o uguali.
* Quando utilizzi AEM come piattaforma di distribuzione di contenuti per terze parti.
   * Qualsiasi soluzione che desideri utilizzare AEM come piattaforma di distribuzione dei contenuti.
   * Incorporazione di contenuti nei punti di contatto di terzi.
* Se usi un’esperienza con diverse varianti o rappresentazioni.
   * Varianti specifiche del canale o del contesto.
   * Esperienze che è utile raggruppare; ad esempio, una campagna con esperienze diverse per i diversi canali.
* Quando utilizzi Commerce omnicanale.
   * Per assegnare funzioni transazionali ai punti di contatto.

## Organizzazione dei frammenti esperienza {#organizing-your-experience-fragments}

È consigliabile:
* organizzare i frammenti esperienza in cartelle;

* [configurare i modelli consentiti in queste cartelle](#configure-allowed-templates-folder).

La creazione di cartelle consente di:

* creare una struttura significativa per i frammenti esperienza, ad esempio, in base alla classificazione

  >[!NOTE]
  >
  >Non è necessario allineare la struttura dei frammenti esperienza alla struttura delle pagine del sito.

* [allocare i modelli consentiti a livello di cartella](#configure-allowed-templates-folder)

  >[!NOTE]
  >
  >Per creare un modello personalizzato, puoi utilizzare [l’editor modelli](/help/sites-cloud/authoring/page-editor/templates.md).

Nel progetto WKND alcuni frammenti esperienza vengono strutturati in base a `Contributors`. La struttura utilizzata illustra anche come utilizzare altre funzioni, come la gestione multisito (incluse le copie per lingua).

Consulta:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Cartelle per i frammenti esperienza](/help/sites-cloud/authoring/assets/xf-folders.png)

## Creazione e configurazione di una cartella per i frammenti esperienza {#creating-and-configuring-a-folder-for-your-experience-fragments}

Per creare e configurare una cartella per i frammenti esperienza, è consigliabile:

1. [Creare una cartella](/help/sites-cloud/authoring/sites-console/managing-pages.md#creating-a-new-folder).

1. [Configurare i modelli di frammento esperienza consentiti per la cartella](#configure-allowed-templates-folder).

>[!NOTE]
>
>È anche possibile configurare i [modelli consentiti per l’istanza](#configure-allowed-templates-instance), ma questo metodo **non** è consigliato in quanto i valori possono essere sovrascritti in seguito a un aggiornamento.

### Configurare i modelli consentiti per la cartella {#configure-allowed-templates-folder}

>[!NOTE]
>
>Si tratta del metodo consigliato per specificare i **modelli consentiti**, poiché i valori non verranno sovrascritti in seguito a un aggiornamento.

1. Individua la cartella **Frammenti esperienza** necessaria.

1. Seleziona la cartella e quindi **Proprietà**.

1. Specifica l’espressione regolare per recuperare i modelli richiesti nel campo **Modelli consentiti**.

   Esempio:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Consulta:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Proprietà dei frammenti esperienza - Modelli consentiti](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Modelli per frammenti esperienza](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleziona **Salva e chiudi**.

### Configurare i modelli consentiti per l’istanza {#configure-allowed-templates-instance}

>[!CAUTION]
>
>È consigliabile non utilizzare questo metodo per modificare i **modelli consentiti**, in quanto i modelli specificati possono essere sovrascritti in seguito a un aggiornamento.
>
>Utilizza questa finestra di dialogo solo a scopo informativo.

1. Individua la console **Frammenti esperienza** necessaria.

1. Seleziona le **opzioni di configurazione**:

   ![Pulsante Configurazione](/help/sites-cloud/authoring/assets/xf-18.png)

1. Specifica i modelli richiesti nella finestra di dialogo **Configura frammenti esperienza**:

   ![Configura frammenti esperienza](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Modelli per frammenti esperienza](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleziona **Salva**.

## Creazione di un frammento esperienza {#creating-an-experience-fragment}

Per creare un frammento esperienza:

1. Seleziona **Frammenti esperienza** nel pannello di navigazione globale.

   ![Frammenti esperienza nel pannello di navigazione](/help/sites-cloud/authoring/assets/xf-01.png)

1. Individua la cartella desiderata e seleziona **Crea**:

   ![Creazione di una cartella per i frammenti esperienza](/help/sites-cloud/authoring/assets/xf-02.png)

1. Seleziona **Frammento esperienza** per aprire la procedura guidata **Crea frammento esperienza**.

   Seleziona il **modello** appropriato, quindi **Avanti**:

   ![Selezione di un modello di frammento esperienza](/help/sites-cloud/authoring/assets/xf-03.png)


1. Inserisci le **proprietà** per il **frammento esperienza**.

   È obbligatorio un **Titolo**. Se il **Nome** viene lasciato vuoto, viene generato dal **Titolo**.

   ![Proprietà dei frammenti esperienza](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >I tag del modello Frammento di esperienza non verranno uniti ai tag presenti nella pagina root Frammento di esperienza.
   >
   >Sono completamente separati.

1. Fai clic su **Crea**.

   Viene visualizzato un messaggio. Seleziona:

   * **Fine** per tornare alla console
   * **Apri** per aprire l’editor frammenti

## Modifica del frammento esperienza {#editing-your-experience-fragment}

L’editor dei frammenti esperienza offre funzionalità simili al normale editor di pagina.

>[!NOTE]
>
>Consulta [Modifica del contenuto di una pagina](/help/sites-cloud/authoring/page-editor/edit-content.md) per ulteriori informazioni su come utilizzare l’editor pagina.

La procedura di esempio seguente illustra come creare un teaser per un prodotto:

1. Trascina il componente richiesto dal [browser Componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

1. A seconda del componente:
   * Aggiungi eventuali contenuti e/o risorse, in base alle esigenze.
   * Configura le proprietà in base alle esigenze.

1. Aggiungi altri componenti in base alle esigenze.

Esempio: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Frammento esperienza nella pagina](/help/sites-cloud/authoring/assets/xf-05.png)

## Creazione di una variante del frammento esperienza {#creating-an-experience-fragment-variation}

Puoi creare varianti del frammento di esperienza, in base alle tue esigenze:

1. Apri la pagina per la [modifica](#editing-your-experience-fragment).
1. Apri la scheda **Varianti**.

   ![Creazione di una variante del frammento esperienza](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Crea** consente di creare:

   * **Variazione**
   * **Variante come Live Copy**.

     >[!NOTE]
     >
     >La creazione di una variante iniziale come Live Copy erediterà il titolo utilizzando la Live Copy Source come variante principale.

1. Definisci le proprietà richieste:

   * **Modello**
   * **Titolo**
   * **Nome**: se è lasciato vuoto, viene generato dal Titolo.
   * **Descrizione**
   * **Tag varianti**

   Esempio:

   ![Proprietà della variante](/help/sites-cloud/authoring/assets/xf-07.png)


1. Conferma con **Fine**; la nuova variante viene visualizzata nel pannello.

## Utilizzo del frammento esperienza {#using-your-experience-fragment}

Ora puoi utilizzare il frammento di esperienza durante l’authoring delle pagine:

1. Apri la pagina da modificare.

   >[!NOTE]
   >
   >La pagina deve essere basata su un modello modificabile.

1. Crea un’istanza del componente Frammento esperienza, all’interno del sistema di paragrafi della pagina:

1. Aggiungi il frammento esperienza effettivo all’istanza del componente, eseguendo una delle seguenti operazioni:

   * Trascina il frammento richiesto dal browser Risorse e rilascialo nel componente.
   * Seleziona **Configura** nella barra degli strumenti del componente e specifica il frammento da utilizzare, quindi conferma con **Fine**.

   >[!NOTE]
   >
   >L’opzione Modifica, nella barra degli strumenti del componente, funziona come una scelta rapida per aprire il frammento nell’editor frammenti.

Esempio: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Frammento esperienza nell’editor pagina](/help/sites-cloud/authoring/assets/xf-08.png)

## Blocchi predefiniti {#building-blocks}

Puoi selezionare uno o più componenti per creare un blocco predefinito da riutilizzare nel frammento:

### Creazione di un blocco predefinito {#creating-a-building-block}

Per creare un blocco predefinito:

1. Nell’editor Frammento di esperienza, seleziona i componenti da riutilizzare:

   ![Selezione del componente per il blocco predefinito](/help/sites-cloud/authoring/assets/xf-09.png)

1. Dalla barra degli strumenti Componenti, seleziona **Converti in blocco predefinito**:

   ![Pulsante Blocco predefinito](/help/sites-cloud/authoring/assets/xf-10.png)

1. Inserisci il nome del **blocco predefinito** e conferma con **Converti**:

   ![Assegnazione di un nome al blocco predefinito](/help/sites-cloud/authoring/assets/xf-11.png)

1. Il **blocco predefinito** verrà visualizzato nella scheda a sinistra (**Locale**) e potrà essere selezionato per ulteriori azioni:

   ![Blocco predefinito nella barra](/help/sites-cloud/authoring/assets/xf-12.png)

#### Gestione di un blocco predefinito {#managing-a-building-block}

Il blocco predefinito è visibile nella scheda **Blocchi predefiniti**. Per ciascun blocco sono disponibili le seguenti azioni:

* **Vai a master**: apri la variante della pagina root in una nuova scheda
* **Rinomina**
* **Elimina**

![Gestione dei blocchi predefiniti](/help/sites-cloud/authoring/assets/xf-13.png)

#### Utilizzo di un blocco predefinito {#using-a-building-block}

Puoi trascinare il blocco predefinito nel sistema di paragrafi di qualsiasi frammento, come un qualsiasi altro componente.

Durante la modifica di un frammento esperienza, nella scheda a sinistra vengono visualizzati i blocchi predefiniti disponibili. Puoi filtrare in base a:

* **Locale**: blocchi predefiniti del frammento esperienza corrente
* **Tutti**: blocchi predefiniti di tutti i frammenti

![Selezione dei blocchi predefiniti](/help/sites-cloud/authoring/assets/xf-14.png)

## Personalizzazione nel frammento di esperienza {#personalization-experience-fragment}

La personalizzazione nel frammento di esperienza ti consente, in qualità di addetto al marketing, di definire i tipi di pubblico target per il frammento di esperienza una sola volta e di riutilizzare il frammento in qualsiasi pagina. Tale comportamento:

* elimina la necessità di specificare le varianti richieste per ogni pubblico ogni volta che viene utilizzato il frammento
* mantiene lo stile tra le offerte

Puoi creare un frammento di esperienza con più componenti raggruppati all’interno di questo singolo frammento. Puoi anche creare varianti del frammento per ogni segmento di pubblico specifico, quindi riutilizzare questi frammenti di esperienza nei canali richiesti.

La personalizzazione si ottiene definendo le proprietà di **Personalizzazione** del frammento di esperienza o della variante, oppure della cartella contenente i frammenti; ciò significa che l’ereditarietà può ignorare le proprietà di personalizzazione.

La configurazione di queste proprietà abilita anche la modalità di **Targeting** nell’editor del frammento di esperienza.

### Definizione della personalizzazione per il frammento di esperienza {#defining-personalization-experience-fragment}

Per personalizzare il frammento:

1. Passa alla posizione desiderata nella console **Frammenti di esperienza**.

1. Seleziona una cartella o un frammento e poi, dalla barra degli strumenti, seleziona **Proprietà**.

   >[!NOTE]
   >
   >Le proprietà di personalizzazione definite in una cartella vengono ereditate da tutte le cartelle secondarie nella sotto-struttura, mentre i frammenti di esperienza (e le varianti) all’interno di questa sotto-struttura. È possibile sostituirli interrompendo l’ereditarietà.

1. Apri la scheda **Personalizzazione** per definire e salvare le impostazioni. Ad esempio, su una cartella:

   ![Frammento di esperienza - Proprietà di personalizzazione](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >Quando un frammento è incorporato in una pagina Sites ed è stata configurata la **Personalizzazione**, al momento del rendering della pagina verrà utilizzata solo la versione di personalizzazione della pagina.
   >
   >Affinché il targeting eseguito sui componenti di un frammento funzioni correttamente nel rendering della pagina, è necessario soddisfare le seguenti condizioni:
   >
   >Il **Percorso ContextHub** selezionato nella scheda **Personalizzazione** deve essere:
   >
   >* lo stesso percorso configurato per la pagina in cui verrà eseguito il rendering del frammento
   >
   >  Oppure:
   >
   >* un percorso che contiene un sottoinsieme degli archivi definiti in ContextHub configurati per la pagina
   >
   >Il **Percorso segmenti** selezionato nella scheda **Personalization** deve essere:
   >
   >* lo stesso percorso configurato per la pagina in cui verrà eseguito il rendering del frammento
   >
   >  Oppure
   >
   >* un percorso che contiene un sottoinsieme dei segmenti configurati per la pagina

### Definizione del targeting per il frammento di esperienza {#defining-targeting-experience-fragment}

Una volta configurate le proprietà di personalizzazione, la modalità Targeting è disponibile quando il frammento viene aperto per la modifica.

![Editor frammento di esperienza - Modalità di targeting](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

Questa modalità funziona come per la modifica delle pagine. Vedi [Modalità di targeting per l’Editor pagina](/help/sites-cloud/authoring/personalization/targeted-content.md) per ulteriori dettagli.

## Dettagli del frammento esperienza {#details-of-your-experience-fragment}

I dettagli del frammento vengono visualizzati in diverse posizioni:

1. Passa alla posizione dei frammenti esperienza, senza scendere fino alle varianti all’interno del frammento.
I dettagli vengono visualizzati in tutte le viste della console **Frammenti esperienza**. Nella **vista a elenco** sono visualizzati i dettagli di un’[esportazione in Target](/help/sites-cloud/integrating/integrating-adobe-target.md):

   ![Dettagli del frammento esperienza](/help/sites-cloud/authoring/assets/xf-15.png)

1. Quando apri le **proprietà** del frammento esperienza:

   ![Pulsante Proprietà](/help/sites-cloud/authoring/assets/xf-16.png)

   Le proprietà sono disponibili in diverse schede:

   >[!CAUTION]
   >
   >Queste schede vengono visualizzate quando apri **Proprietà** dalla console Frammenti esperienza.
   >
   >Se scegli **Apri proprietà** durante la modifica di un frammento esperienza, vengono visualizzate le [proprietà di pagina](/help/sites-cloud/authoring/sites-console/page-properties.md) appropriate.

   ![Proprietà dei frammenti esperienza](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Base**
      * **Titolo** - obbligatorio
      * **Descrizione**
      * **Tag**
      * **Numero totale di varianti** - solo informativo
      * **Numero di varianti web** - solo informativo
      * **Numero di varianti non web** - solo informativo
      * **Numero di pagine che utilizzano questo frammento** - solo informazioni
   * **Servizi cloud**
      * **Configurazione cloud**
      * **Configurazioni Cloud Service**
      * **ID pagina Facebook**
      * **Bacheca Pinterest**
   * **Riferimenti**
      * Un elenco di riferimenti
   * **Personalizzazione**
      * **Percorso ContextHub**
      * **Percorso dei segmenti**
      * **Marchio**

## Rendering HTML semplice {#the-plain-html-rendition}

Se utilizzi il selettore `.plain.` nell’URL, puoi accedere al rendering HTML semplice dal browser.

>[!NOTE]
>
>Sebbene sia disponibile direttamente dal browser, [lo scopo principale è quello di consentire ad altre applicazioni (ad esempio, applicazioni web di terze parti o implementazioni personalizzate per dispositivi mobili) di accedere ai contenuti del frammento esperienza direttamente dall’URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Pubblicazione di frammenti di esperienza {#publishing-experience-fragments}

La pubblicazione di un frammento di esperienza è fondamentalmente identica alla [pubblicazione di una pagina](/help/sites-cloud/authoring/sites-console/publishing-pages.md) (ma viene eseguita dalla console o dall’editor frammenti di esperienza).

In alternativa è possibile [pubblicare in anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) (di nuovo dalla console o dall’editor frammenti di esperienza).

>[!CAUTION]
>
>Per impostazione predefinita, la pubblicazione della cartella principale dei frammenti esperienza (che si trova direttamente in `/content/experience-fragments`):
>
>* pubblica solo la cartella contenitore stessa
>* non pubblica alcun elemento figlio
>* annulla la pubblicazione di eventuali elementi figlio già pubblicati
>
>Per la pubblicazione di tutti i frammenti esperienza nella cartella, ciascuno di essi deve essere pubblicato separatamente.

## Esportazione di frammenti esperienza   {#exporting-experience-fragments}

Per impostazione predefinita, i frammenti di esperienza vengono forniti nel formato HTML. che può essere utilizzato sia da AEM che da canali di terze parti.

Per l’esportazione in Adobe Target, è possibile utilizzare anche JSON. Consulta:

* [Integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Esportazione di frammenti di esperienza in Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
