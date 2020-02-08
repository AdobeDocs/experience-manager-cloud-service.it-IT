---
title: Frammenti esperienza
description: Utilizza Adobe Experience Manager come frammenti esperienza del servizio cloud per rendere le tue esperienze riutilizzabili e flessibili.
translation-type: tm+mt
source-git-commit: b7a2e86de27dbfcdecaf3a2bc1984678b7b69375

---


# Frammenti esperienza {#experience-fragments}

In Adobe Experience Manager come servizio Cloud, un frammento esperienza:
* è un gruppo di uno o più componenti
* include contenuto e layout
* è possibile fare riferimento alle pagine
* può contenere qualsiasi componente

Caratteristiche di un Frammento esperienza:

* È parte di un’esperienza (pagina).
* Può essere utilizzato su più pagine.
* Si basa su un modello (solo modificabile) per la definizione di struttura e componenti.
* È composto da uno o più componenti, con layout, in un sistema di paragrafo.
* Può contenere altri frammenti esperienza.
* Può essere combinato con altri componenti (inclusi gli altri Frammenti esperienza) per formare una pagina completa (esperienza).
* Può avere diverse varianti, che possono condividere contenuti e/o componenti.
* Può essere suddiviso in blocchi predefiniti che possono essere utilizzati in più varianti del frammento.

Quando utilizzare un Frammento esperienza:

* Se un autore desidera riutilizzare parti (un frammento di un’esperienza) di una pagina.
In assenza di frammenti esperienza, l’autore deve copiare e incollare il frammento. Creare e gestire queste esperienze tramite copia/incolla richiede tempo e può essere fonte di errori da parte dell’utente.
I frammenti esperienza eliminano la necessità di copiare/incollare.
* Per supportare il caso d’uso headless CMS.
Gli autori desiderano utilizzare AEM solo per l’authoring ma non per la distribuzione al cliente. Un sistema o punto di contatto di terze parti potrebbe prendere in carico questa particolare esperienza e in seguito trasmetterla all’utente finale.

>[!NOTE]
>
>Per poter accedere in scrittura ai frammenti esperienza, l’account utente deve essere registrato nel gruppo
>
>* `experience-fragments-editors`
>
>
Per qualsiasi problema riscontrato, contatta l’amministratore del sistema.

## Quando utilizzare i frammenti esperienza? {#when-should-you-use-experience-fragments}

I frammenti esperienza devono essere utilizzati:

* Quando desideri riutilizzare le esperienze.
   * Per esperienze che riutilizzerai con contenuti simili o uguali. &quot;merge_preserve&quot;.
* Quando utilizzi AEM come piattaforma di distribuzione di contenuti per terze parti.
   * Per qualsiasi soluzione che utilizza AEM come piattaforma di distribuzione di contenuti. &quot;merge_preserve&quot;.
   * Per incorporare contenuti nei punti di contatto di terze parti.
* Se usi un’esperienza con diverse varianti o rappresentazioni.
   * Varianti per un canale o per un contesto specifico. &quot;merge_preserve&quot;.
   * Esperienze che hanno senso raggruppare; ad esempio una campagna con esperienze diverse tra i canali.
* Quando utilizzi Commerce omnichannel.
   * Per condividere contenuti commerciali sui canali di [social media](/help/implementing/developing/extending/experience-fragments.md#social-variations) su larga scala. &quot;merge_preserve&quot;.
   * Per assegnare funzioni transazionali ai punti di contatto.

## Organizzazione dei frammenti esperienza {#organizing-your-experience-fragments}

Si consiglia di:
* utilizzare le cartelle per organizzare i frammenti esperienza,

* [configurate i modelli consentiti in queste cartelle](#configure-allowed-templates-folder).

La creazione di cartelle consente di:

* creare una struttura significativa per i frammenti esperienza; ad esempio, in base alla classificazione

   >[!NOTE]
   >
   >Non è necessario allineare la struttura dei frammenti esperienza con la struttura di pagina del sito.

* [allocare i modelli consentiti a livello di cartella](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >Puoi utilizzare l&#39;[Editor modelli](/help/sites-cloud/authoring/features/templates.md) per creare un modello personalizzato.

Il progetto WKND crea alcuni frammenti esperienza in base a `Contributors`. La struttura utilizzata illustra anche come possono essere utilizzate altre funzioni, come la gestione multisito (incluse le copie della lingua).

Vedi:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Cartelle per i frammenti esperienza](/help/sites-cloud/authoring/assets/xf-folders.png)

## Creazione e configurazione di una cartella per i frammenti esperienza {#creating-and-configuring-a-folder-for-your-experience-fragments}

Per creare e configurare una cartella per i frammenti esperienza, si consiglia di:

1. [Create una cartella](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [Configura i modelli di frammento esperienza consentiti per la cartella](#configure-allowed-templates-folder).

>[!NOTE]
>
>È anche possibile configurare i modelli [consentiti per l’istanza](#configure-allowed-templates-instance), ma questo metodo **non** è consigliato in quanto i valori possono essere sovrascritti al momento dell’aggiornamento.

### Configurare i modelli consentiti per la cartella {#configure-allowed-templates-folder}

>[!NOTE]
>
>Questo è il metodo consigliato per specificare i modelli **** consentiti, poiché i valori non verranno sovrascritti al momento dell&#39;aggiornamento.

1. Individua la cartella **Frammenti esperienza** necessaria.

1. Selezionate la cartella, quindi **Proprietà**.

1. Specificate l&#39;espressione regolare per recuperare i modelli richiesti nel campo Modelli **** consentiti.

   Esempio:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Vedi:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Proprietà frammento esperienza - Modelli consentiti](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta la sezione sui [modelli per frammenti esperienza](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Selezionate **Salva e chiudi**.

### Configurare i modelli consentiti per la tua istanza {#configure-allowed-templates-instance}

>[!CAUTION]
>
>Non è consigliabile modificare i modelli **** consentiti con questo metodo, in quanto i modelli specificati possono essere sovrascritti al momento dell&#39;aggiornamento.
>
>Utilizzare questa finestra di dialogo solo a scopo informativo.

1. Navigate to the required **Experience Fragments** console.

1. Seleziona le **opzioni di configurazione**:

   ![Pulsante Configurazione](/help/sites-cloud/authoring/assets/xf-18.png)

1. Specifica i modelli richiesti nella finestra di dialogo **Configura frammenti esperienza**:

   ![Configura frammenti esperienza](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta la sezione sui [modelli per frammenti esperienza](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleziona **Salva**.


## Creazione di un frammento esperienza {#creating-an-experience-fragment}

Per creare un frammento esperienza:

1. Select **Experience Fragments** from the Global Navigation.

   ![Frammenti esperienza nel pannello di navigazione](/help/sites-cloud/authoring/assets/xf-01.png)

1. Passate alla cartella desiderata e selezionate **Crea**:

   ![Creazione di una cartella per i frammenti esperienza](/help/sites-cloud/authoring/assets/xf-02.png)

1. Selezionate **Frammento** esperienza per aprire la procedura guidata **Crea frammento** esperienza.

   Seleziona il **Modello** appropriato, quindi **Avanti**:

   ![Selezione di un modello di frammento esperienza](/help/sites-cloud/authoring/assets/xf-03.png)


1. Inserisci le **Proprietà** per il **frammento esperienza**.

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

1. Trascinare il componente richiesto dal browser [Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. A seconda del componente:
   * Aggiungete eventuale contenuto e/o risorsa, a seconda delle necessità.
   * Configurare le proprietà come richiesto.

1. Aggiungi altri componenti in base alle esigenze.

Esempio: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Frammento esperienza sulla pagina](/help/sites-cloud/authoring/assets/xf-05.png)

## Creazione di una variante del frammento esperienza {#creating-an-experience-fragment-variation}

Puoi creare diverse varianti per un Frammento esperienza a seconda delle tue esigenze:

1. Apri la pagina per la [modifica](#editing-your-experience-fragment).
1. Apri la scheda **Varianti**.

   ![Creazione di una variante di frammento esperienza](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Crea** ti consente di creare:

   * **Variante**
   * **Variante come Live Copy**.

1. Definisci le proprietà richieste:

   * **Modello**
   * **Titolo**
   * **Nome** : se lasciato vuoto, verrà derivato dal Titolo
   * **Descrizione**
   * **Tag varianti**
   Esempio:

   ![Proprietà variante](/help/sites-cloud/authoring/assets/xf-07.png)

1. Confirm with **Done**, the new variation will be shown in the panel.

## Utilizzo del frammento esperienza {#using-your-experience-fragment}

A questo punto puoi utilizzare il frammento esperienza durante l’authoring delle pagine:

1. Apri la pagina da modificare.

1. Create un’istanza del componente Frammento esperienza, all’interno del sistema paragrafo della pagina:

1. Aggiungi il frammento esperienza effettivo all’istanza del componente, eseguendo una delle seguenti operazioni:

   * Trascina il frammento richiesto dal browser Risorse e rilascialo sul componente.
   * Select **Configure** from the component toolbar and specify the fragment to use, confirm with **Done**.
   >[!NOTE]
   >
   >L’opzione Modifica, nella barra degli strumenti del componente, funziona come una scelta rapida per aprire il frammento nell’editor frammenti.

Esempio: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Frammento esperienza nell’Editor pagina](/help/sites-cloud/authoring/assets/xf-08.png)

## Blocchi predefiniti {#building-blocks}

Puoi selezionare uno o più componenti per creare un blocco predefinito da riutilizzare nel frammento:

### Creazione di un blocco predefinito {#creating-a-building-block}

Per creare un nuovo blocco predefinito:

1. Nell’editor Frammento esperienza, seleziona i componenti che desideri riutilizzare:

   ![Seleziona componente per blocco predefinito](/help/sites-cloud/authoring/assets/xf-09.png)

1. Dalla barra degli strumenti Componenti, seleziona **Converti in blocco predefinito**:

   ![Pulsante Blocca generazione](/help/sites-cloud/authoring/assets/xf-10.png)

1. Inserisci il nome del **blocco predefinito** e conferma mediante **Converti**:

   ![Blocco predefinito nome](/help/sites-cloud/authoring/assets/xf-11.png)

1. Il blocco **** predefinito verrà visualizzato nella scheda a sinistra (**Locale**) e può essere selezionato per ulteriori azioni:

   ![Blocco predefinito nella barra](/help/sites-cloud/authoring/assets/xf-12.png)

#### Gestione di un blocco predefinito {#managing-a-building-block}

Il blocco predefinito è visibile nella scheda **Blocchi predefiniti**. Per ogni blocco sono disponibili le azioni seguenti:

* **** Vai a principale: apre la variante principale in una nuova scheda
* **Rinomina**
* **Elimina**

![Gestione dei blocchi predefiniti](/help/sites-cloud/authoring/assets/xf-13.png)

#### Utilizzo di un blocco predefinito {#using-a-building-block}

Puoi trascinare il blocco predefinito sul sistema di paragrafi di qualsiasi frammento, così come si fa con qualsiasi componente.

Quando si modifica un frammento esperienza, nella scheda a sinistra vengono visualizzati i blocchi predefiniti disponibili. Potete filtrare in base a:

* **Locale** - Blocchi costitutivi del frammento esperienza corrente
* **Tutti** - Blocchi predefiniti da tutti i frammenti

![Selezione dei blocchi predefiniti](/help/sites-cloud/authoring/assets/xf-14.png)

## Dettagli del frammento esperienza {#details-of-your-experience-fragment}

I dettagli del frammento vengono visualizzati in diversi luoghi:

1. Andate alla posizione dei frammenti esperienza (non andate oltre fino alle varianti all’interno del frammento).
I dettagli vengono visualizzati in tutte le viste della console **Frammenti esperienza**, dove la **vista a elenco** comprende i dettagli di una esportazione in Target: <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![Dettagli frammento esperienza](/help/sites-cloud/authoring/assets/xf-15.png)

1. Quando apri le **Proprietà** del frammento esperienza:

   ![Pulsante Proprietà](/help/sites-cloud/authoring/assets/xf-16.png)

   Le proprietà sono disponibili in varie schede:

   >[!CAUTION]
   >
   >Queste schede vengono visualizzate quando si aprono **Proprietà** dalla console Frammenti esperienza.
   >
   >Se **aprite le proprietà** durante la modifica di un frammento esperienza, vengono visualizzate le proprietà [di](/help/sites-cloud/authoring/fundamentals/page-properties.md) pagina appropriate.

   ![Proprietà dei frammenti esperienza](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Base**
      * **Titolo** - obbligatorio
      * **Descrizione**
      * **Tag**
      * **Numero totale di varianti** - solo informativo
      * **Numero di varianti web** - solo informativo
      * **Numero di varianti** non web - solo informazioni
      * **Numero di pagine con questo frammento** - solo informativo
   * **Servizi cloud**
      * **Configurazione cloud**
      * **Configurazioni servizi cloud**
      * **ID pagina Facebook**
      * **Bacheca Pinterest**
   * **Riferimenti**
      * Un elenco di riferimenti
   * **Stato social media**
      * Dettagli delle varianti per social media

## La rappresentazione HTML semplice {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition from the browser.

>[!NOTE]
>
>Sebbene sia disponibile direttamente dal browser, [lo scopo principale è quello di consentire ad altre applicazioni (ad esempio, applicazioni web di terze parti o implementazioni personalizzate per dispositivi mobili) di accedere ai contenuti del frammento esperienza direttamente dall’URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Esportazione di frammenti esperienza {#exporting-experience-fragments}

Per impostazione predefinita, i frammenti esperienza vengono forniti nel formato HTML che può essere utilizzati sia da AEM che da canali di terze parti.

Per l’esportazione in Adobe Target, è possibile utilizzare anche il formato JSON. Per informazioni complete, consulta Integrazione di Target con frammenti esperienza. <!--For export to Adobe Target, JSON can also be used. See [Target Integration with Experience Fragments](/help/sites-administering/experience-fragments-target.md) for full information.-->
