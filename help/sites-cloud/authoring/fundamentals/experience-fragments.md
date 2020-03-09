---
title: Frammenti esperienza
description: Utilizza Frammenti esperienza di Adobe Experience Manager as a Cloud Service per rendere le tue esperienze riutilizzabili e flessibili.
translation-type: ht
source-git-commit: b7a2e86de27dbfcdecaf3a2bc1984678b7b69375

---


# Frammenti esperienza {#experience-fragments}

In Adobe Experience Manager as a Cloud Service, un frammento esperienza:
* è un gruppo di uno o più componenti;
* include sia contenuto che layout;
* può essere aggiunto come riferimento nelle pagine;
* può contenere qualsiasi componente.

Caratteristiche di un Frammento esperienza:

* È parte di un’esperienza (pagina).
* Può essere utilizzato su più pagine.
* Si basa su un modello (solo modificabile) per la definizione di struttura e componenti.
* È composto da uno o più componenti, con layout, in un sistema di paragrafo.
* Può contenere altri frammenti esperienza.
* Può essere combinato con altri componenti (inclusi altri frammenti esperienza) per formare una pagina completa (esperienza).
* Può avere diverse varianti, che possono condividere contenuti e/o componenti.
* Può essere suddiviso in blocchi predefiniti che possono essere utilizzati in più varianti del frammento.

Puoi utilizzare Frammenti esperienza:

* Se un autore desidera riutilizzare parti (un frammento di un’esperienza) di una pagina.
Senza Frammenti esperienza, l’autore dovrebbe copiare e incollare tale frammento. Creare e gestire queste esperienze di copia/incolla richiede tempo e può essere fonte di errori da parte dell’utente.
Grazie a Frammenti esperienza non è più necessario eseguire operazioni di copia/incolla.
* Per supportare il caso d’uso del CMS headless.
Gli autori intendono utilizzare AEM solo per l’authoring, ma non per la distribuzione al cliente. Un sistema o punto di contatto di terze parti potrebbe prendere in carico questa particolare esperienza e in seguito trasmetterla all’utente finale.

>[!NOTE]
>
>Per poter accedere in scrittura ai frammenti esperienza, l’account utente deve essere registrato nel gruppo
>
>* `experience-fragments-editors`
>
>
Per qualsiasi problema riscontrato, contatta l’amministratore del sistema.

## Quando utilizzare i frammenti esperienza?   {#when-should-you-use-experience-fragments}

I frammenti esperienza devono essere utilizzati:

* Quando desideri riutilizzare le esperienze.
   * Per esperienze che riutilizzerai con contenuti simili o uguali. .
* Quando utilizzi AEM come piattaforma di distribuzione di contenuti per terze parti.
   * Per qualsiasi soluzione che utilizza AEM come piattaforma di distribuzione di contenuti. .
   * Per incorporare contenuti nei punti di contatto di terze parti.
* Se usi un’esperienza con diverse varianti o rappresentazioni.
   * Varianti per un canale o per un contesto specifico. .
   * Per esperienze che è utile raggruppare; ad esempio una campagna con diverse esperienze per i vari canali.
* Quando utilizzi Commerce omnichannel.
   * Per condividere contenuti commerciali sui canali di [social media](/help/implementing/developing/extending/experience-fragments.md#social-variations) su larga scala.
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
   >Per creare un modello personalizzato, puoi utilizzare [l’editor modelli](/help/sites-cloud/authoring/features/templates.md).

Nel progetto WKND alcuni frammenti esperienza vengono strutturati in base a `Contributors`. La struttura utilizzata illustra anche come utilizzare altre funzioni, come la gestione multisito (incluse le copie per lingua).

Consulta:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Cartelle per i frammenti esperienza](/help/sites-cloud/authoring/assets/xf-folders.png)

## Creazione e configurazione di una cartella per i frammenti esperienza {#creating-and-configuring-a-folder-for-your-experience-fragments}

Per creare e configurare una cartella per i frammenti esperienza, è consigliabile:

1. [Creare una cartella](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

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

   Il campo **Titolo** è obbligatorio. Se il campo **Nome** è lasciato vuoto, verrà derivato dal **Titolo**.

   ![Proprietà dei frammenti esperienza](/help/sites-cloud/authoring/assets/xf-04.png)

1. Fai clic su **Crea**. 

   Viene visualizzato un messaggio. Seleziona:

   * **Fine** per tornare alla console
   * **Apri** per aprire l’editor frammenti

## Modifica del frammento esperienza {#editing-your-experience-fragment}

L’editor dei frammenti esperienza offre funzionalità simili al normale editor di pagina.

>[!NOTE]
>
>Consulta [Modifica del contenuto di pagina](/help/sites-cloud/authoring/fundamentals/editing-content.md) per ulteriori informazioni su come usare questo strumento.

L’esempio seguente illustra come creare un teaser per un prodotto:

1. Trascina il componente richiesto dal [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. A seconda del componente:
   * Aggiungi eventuali contenuti e/o risorse, in base alle esigenze.
   * Configura le proprietà in base alle esigenze.

1. Aggiungi altri componenti in base alle esigenze.

Esempio: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Frammento esperienza nella pagina](/help/sites-cloud/authoring/assets/xf-05.png)

## Creazione di una variante del frammento esperienza {#creating-an-experience-fragment-variation}

Puoi creare diverse varianti per un Frammento esperienza a seconda delle tue esigenze:

1. Apri la pagina per la [modifica](#editing-your-experience-fragment).
1. Apri la scheda **Varianti**.

   ![Creazione di una variante del frammento esperienza](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Crea** ti consente di creare:

   * **Variante**
   * **Variante come Live Copy**.

1. Definisci le proprietà richieste:

   * **Modello**
   * **Titolo**
   * **Nome**: se è lasciato vuoto, verrà derivato dal campo Titolo.
   * **Descrizione**
   * **Tag varianti**
   Esempio:

   ![Proprietà della variante](/help/sites-cloud/authoring/assets/xf-07.png)

1. Conferma con **Fine**; la nuova variante viene visualizzata nel pannello.

## Utilizzo del frammento esperienza {#using-your-experience-fragment}

A questo punto puoi utilizzare il frammento esperienza durante l’authoring delle pagine:

1. Apri la pagina da modificare.

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

Per creare un nuovo blocco predefinito:

1. Nell’editor Frammento esperienza, seleziona i componenti che desideri riutilizzare:

   ![Selezione del componente per il blocco predefinito](/help/sites-cloud/authoring/assets/xf-09.png)

1. Dalla barra degli strumenti Componenti, seleziona **Converti in blocco predefinito**:

   ![Pulsante Blocco predefinito](/help/sites-cloud/authoring/assets/xf-10.png)

1. Inserisci il nome del **blocco predefinito** e conferma con **Converti**:

   ![Assegnazione di un nome al blocco predefinito](/help/sites-cloud/authoring/assets/xf-11.png)

1. Il **blocco predefinito** verrà visualizzato nella scheda a sinistra (**Locale**) e può essere selezionato per ulteriori azioni:

   ![Blocco predefinito nella barra](/help/sites-cloud/authoring/assets/xf-12.png)

#### Gestione di un blocco predefinito {#managing-a-building-block}

Il blocco predefinito è visibile nella scheda **Blocchi predefiniti**. Per ogni blocco sono disponibili le azioni seguenti:

* **Vai a principale**: apre la variante principale in una nuova scheda
* **Rinomina**
* **Elimina**

![Gestione dei blocchi predefiniti](/help/sites-cloud/authoring/assets/xf-13.png)

#### Utilizzo di un blocco predefinito {#using-a-building-block}

Puoi trascinare il blocco predefinito nel sistema di paragrafi di qualsiasi frammento, come un qualsiasi altro componente.

Durante la modifica di un frammento esperienza, nella scheda a sinistra vengono visualizzati i blocchi predefiniti disponibili. Puoi filtrare in base a:

* **Locale**: blocchi predefiniti del frammento esperienza corrente
* **Tutti**: blocchi predefiniti di tutti i frammenti

![Selezione dei blocchi predefiniti](/help/sites-cloud/authoring/assets/xf-14.png)

## Dettagli del frammento esperienza {#details-of-your-experience-fragment}

I dettagli del frammento vengono visualizzati in diverse posizioni:

1. Passa alla posizione dei frammenti esperienza, senza scendere fino alle varianti all’interno del frammento.
I dettagli vengono visualizzati in tutte le viste della console **Frammenti esperienza**. Nella **vista a elenco** sono visualizzati i dettagli di un’esportazione in Target: <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![Dettagli del frammento esperienza](/help/sites-cloud/authoring/assets/xf-15.png)

1. Quando apri le **proprietà** del frammento esperienza:

   ![Pulsante Proprietà](/help/sites-cloud/authoring/assets/xf-16.png)

   Le proprietà sono disponibili in diverse schede:

   >[!CAUTION]
   >
   >Queste schede vengono visualizzate quando apri **Proprietà** dalla console Frammenti esperienza.
   >
   >Se scegli **Apri proprietà** durante la modifica di un frammento esperienza, vengono visualizzate le [proprietà di pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md) appropriate.

   ![Proprietà dei frammenti esperienza](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Base**
      * **Titolo** - obbligatorio
      * **Descrizione**
      * **Tag**
      * **Numero totale di varianti** - solo informativo
      * **Numero di varianti web** - solo informativo
      * **Numero di varianti non web** - solo informativo
      * **Numero di pagine con questo frammento** - solo informativo
   * **Cloud Services**
      * **Configurazione cloud**
      * **Configurazioni Cloud Service**
      * **ID pagina Facebook**
      * **Bacheca Pinterest**
   * **Riferimenti**
      * Un elenco di riferimenti
   * **Stato social media**
      * Dettagli delle varianti per social media

## Rendering HTML semplice {#the-plain-html-rendition}

Se utilizzi il selettore `.plain.` nell’URL, puoi accedere al rendering HTML semplice dal browser.

>[!NOTE]
>
>Sebbene sia disponibile direttamente dal browser, [lo scopo principale è quello di consentire ad altre applicazioni (ad esempio, applicazioni web di terze parti o implementazioni personalizzate per dispositivi mobili) di accedere ai contenuti del frammento esperienza direttamente dall’URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Esportazione di frammenti esperienza   {#exporting-experience-fragments}

Per impostazione predefinita, i frammenti esperienza vengono forniti nel formato HTML che può essere utilizzati sia da AEM che da canali di terze parti.

Per l’esportazione in Adobe Target, è possibile utilizzare anche il formato JSON. Per informazioni complete, consulta Integrazione di Target con Frammenti esperienza. <!--For export to Adobe Target, JSON can also be used. See [Target Integration with Experience Fragments](/help/sites-administering/experience-fragments-target.md) for full information.-->
