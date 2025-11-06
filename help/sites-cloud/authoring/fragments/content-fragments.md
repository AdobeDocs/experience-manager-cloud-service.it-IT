---
title: Frammenti di contenuto
description: I Frammenti di contenuto di Adobe Experience Manager as a Cloud Service ti consentono di progettare, creare, curare e utilizzare contenuti indipendenti dal canale che possono essere utilizzati anche durante l’authoring delle pagine.
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
solution: Experience Manager Sites
feature: Authoring, Content Fragments
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 82%

---

# Frammenti di contenuto {#content-fragments}

I frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service sono [creati e gestiti come risorse indipendenti dalla pagina](/help/sites-cloud/administering/content-fragments/overview.md), che consentono di creare contenuti indipendenti dal canale, insieme a varianti (possibilmente specifiche del canale). Puoi utilizzare questi frammenti, e le relative varianti, durante l’authoring delle pagine di contenuto.

>[!CAUTION]
>
>Questa pagina deve essere letta insieme a [Utilizzo dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md) (e pagine correlate), in quanto introduce la terminologia e i concetti di base, oltre alle informazioni sulla creazione e la gestione dei frammenti e sulla distribuzione di frammenti di contenuto strutturati a canali diversi dalle pagine AEM.

>[!NOTE]
>
>I frammenti di contenuto sono una funzionalità di **Sites**, ma sono memorizzati come **Assets**.
>
>Sono gestite principalmente con la console **[Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, anche se possono ancora essere gestite dalla console **[Assets](/help/assets/content-fragments/content-fragments-managing.md)**.
>
>L&#39;editor predefinito per [Frammenti di contenuto - Authoring](/help/sites-cloud/administering/content-fragments/authoring.md) è il nuovo editor; è possibile accedere sia dalla console **Frammenti di contenuto** che dalla console **Assets**.
>
>Per utilizzare l&#39;[editor originale](/help/assets/content-fragments/content-fragments-variations.md), aprire prima il nuovo editor e quindi disattivare l&#39;opzione **Nuovo editor**.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md)** sono funzioni diverse in AEM:
>
>* I **frammenti di contenuto** sono contenuti editoriali, con definizione e struttura, ma senza elementi visivi aggiuntivi di design e/o layout. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, consulta [Comprensione dei frammenti di contenuto e dei frammenti di esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=it#content-fragments).

I frammenti di contenuto consentono:

* La **Strategia di marketing e campagne**
   * La revisione dei contenuti tramite frammenti di contenuto gestiti a livello centrale.
* **Creative Pro**
   * Il tracciamento delle risorse creative tramite raccolte associate a frammenti di contenuto.
* **Copywriter**
   * Creazione di contenuti nell’editor frammento di contenuto di AEM.
   * Possono creare varianti del contenuto.
   * Possono associare contenuti rilevanti ai frammenti di contenuto.
   * Possono utilizzare il controllo delle versioni/flusso di lavoro.
   * Possono condividere dei frammenti di contenuto.
   * Possono gestire le traduzioni a livello centrale.
* **Produttori e responsabili dei percorsi**
   * Scelta di frammenti e varianti predefiniti con l’authoring in AEM.
   * Possono contare sul fatto che il frammento e il contenuto associato ad esso sono sempre aggiornati, poiché i copywriter e i creativi effettuano gli aggiornamenti su frammenti e risorse gestiti a livello centrale.
   * Possono contare sul fatto che i contenuti multimediali associati sono sempre curati in base alla rilevanza.
   * Possono creare all’istante varianti di contenuto ad hoc garantendo che queste restino comunque gestite a livello centrale nel frammento.

## Aggiunta di un frammento di contenuto alla pagina  {#adding-a-content-fragment-to-your-page}

1. Apri la pagina per la modifica.
2. Aggiungi il componente **Frammento di contenuto** dal browser **Componenti** o mediante il comando **Inserisci nuovo componente**.
3. Puoi effettuare le seguenti operazioni:
   * Apri il browser **Risorse** e applica il filtro **Frammenti di contenuto** (l’impostazione predefinita è Immagini). Poi trascina il frammento desiderato sull’istanza del componente.
   * Seleziona il componente del frammento di contenuto, quindi **Configura** dalla barra degli strumenti. Nella finestra di dialogo, apri la finestra di dialogo di selezione per individuare e selezionare il **frammento di contenuto** richiesto.

   >[!NOTE]
   >
   >In alternativa, puoi trascinare un frammento di contenuto specifico direttamente nella pagina. In questo modo verrà creato automaticamente il componente associato (Frammento di contenuto).

4. Inizialmente verrà visualizzato il contenuto dell’elemento **principale** e **primario** (variante). Puoi [selezionare altri elementi e/o varianti](#selecting-the-element-or-variation), secondo necessità.

   ![Frammenti di contenuto nel browser Risorse](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Per informazioni su ulteriori funzionalità di modifica, consulta anche:
   >
   >* [Layout dinamico](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
   >* [Modifica del contenuto di una pagina](/help/sites-cloud/authoring/page-editor/edit-content.md)

### Selezione dell’elemento o della variante {#selecting-the-element-or-variation}

Apri la finestra di dialogo **Configurazione** del frammento per configurare il frammento per la pagina corrente. La finestra di dialogo può dipendere dal componente utilizzato.

>[!NOTE]
>
>Consulta anche [Componenti core, componente Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it)

Nella finestra di dialogo di configurazione appropriata puoi selezionare i parametri disponibili, tra cui:

* **Frammento di contenuto**
   * Specifica il frammento da utilizzare.
* **Modalità di visualizzazione**:
   * **Elemento di testo singolo**
   * **Più elementi**
* **Elemento**
   * A seconda del modello utilizzato è disponibile una selezione.

  >[!NOTE]
  >
  >Gli elementi disponibili dipendono dal modello utilizzato.

* **Variazione**
   * La variante **Primaria** predefinita è sempre disponibile.
   * Se per il frammento sono state create delle varianti, è disponibile una selezione.

* **ID**

   * Attributo **ID HTML** da applicare al componente.

### Collegamento rapido all’editor frammento di contenuto  {#quick-connection-to-fragment-editor}

Puoi aprire l’origine del frammento in modalità di modifica (la risorsa) mediante l’icona **Modifica** nella barra degli strumenti del componente, così da poter [modificare e gestire il frammento di contenuto](/help/sites-cloud/administering/content-fragments/overview.md).

>[!CAUTION]
>
>Come sempre, la modifica dell’origine del frammento ha un impatto su tutte le pagine che fanno riferimento a tale frammento di contenuto.

### Aggiunta di contenuto intermedio  {#adding-in-between-content}

Quando un frammento di contenuto specifico viene aggiunto alla pagina, è disponibile un segnaposto **Trascina qui i componenti** tra ciascun paragrafo HTML (e nella parte superiore/inferiore) del frammento.

In questo modo è possibile aggiungere contenuto aggiuntivo [nel contenuto intermedio (ovvero nel contenuto intermedio)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) nel contenuto del frammento (in qualsiasi punto disponibile), senza dover modificare il frammento principale.

Per il contenuto intermedio è possibile:

* Aggiungi componenti dal browser [Componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
* Aggiungi risorse dal [browser Assets](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)
* usare [Contenuto associato](#using-associated-content) come origine per il contenuto intermedio.

>[!CAUTION]
>
>Il contenuto intermedio è il contenuto della pagina. Non viene memorizzato nel frammento di contenuto.

![Inserisci componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>È inoltre possibile [inserire risorse visive (immagini) nel frammento stesso](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Le risorse visive inserite nel frammento stesso sono associate al paragrafo precedente nel frammento. Non è pertanto possibile inserire contenuto intermedio tra una risorsa visiva e il paragrafo precedente. Qualora ti occorra questo livello di connessione, puoi aggiungere l’immagine al frammento (come [frammento con file multimediali diversi](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>Dopo aver aggiunto contenuto intermedio a un frammento di contenuto nella pagina, se si modifica la struttura del frammento di contenuto sottostante (ovvero nell’editor frammento di contenuto) si potrebbero verificare risultati erronei o imprevisti.
>
>In questi casi, il contenuto intermedio rimane inalterato:
>
>* I componenti intermedi hanno una posizione assoluta all’interno della sequenza di componenti nel flusso del frammento. Questa posizione non cambia, anche quando cambia il contenuto dei paragrafi nel frammento.
>
>  Questo potrebbe dare l’impressione di una modifica nella posizione relativa, poiché i paragrafi intermedi non hanno alcuna relazione contestuale con i paragrafi (del frammento) accanto ai quali sono posizionati,
>
>* a meno che le due strutture di paragrafo non siano in conflitto. In questo caso il contenuto intermedio non viene visualizzato, ma resta comunque presente nel codice interno.

### Uso di contenuti associati  {#using-associated-content}

Se hai [associato del contenuto](/help/assets/content-fragments/content-fragments-assoc-content.md) al [frammento di contenuto](/help/assets/content-fragments/content-fragments.md), queste risorse sono disponibili nel pannello laterale (dopo aver inserito il frammento nella pagina del contenuto). Il contenuto associato è di fatto una fonte speciale di contenuto per il [contenuto intermedio](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Esistono vari metodi per aggiungere [risorse visive (ad esempio immagini)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al frammento e/o alla pagina.

>[!NOTE]
>
>Se sulla stessa pagina sono presenti più frammenti di contenuto, la scheda **Contenuto associato** mostrerà le risorse appropriate per tutti i frammenti.

Una volta aggiunto alla pagina un frammento con contenuto associato, nel pannello laterale viene aperta una nuova scheda (**Contenuto associato**).

Da qui puoi trascinare le risorse nella posizione richiesta (su un componente esistente o nella posizione in cui viene creato il componente appropriato):

![Inserimento di un’immagine](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Risorse inserite nel frammento {#assets-inserted-into-the-fragment}

Se sono state inserite delle risorse (ad esempio immagini) nel frammento stesso (come [frammenti con file multimediali diversi](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)), le opzioni per la modifica di tali risorse nell’editor pagina sono limitate.

Ad esempio, per un’immagine è possibile:

* Ritaglia, ruota o capovolgi l’immagine.
* Aggiungi un titolo o un testo alternativo.
* Specifica una dimensione.
* Puoi anche configurare il layout.

Altre modifiche, ad esempio sposta, copia ed elimina devono essere effettuate nell’editor frammenti.

### Pubblicazione {#publishing}

I frammenti devono essere pubblicati in modo che possano essere utilizzati nelle pagine web pubblicate:

* Un frammento può essere pubblicato dopo che è stato [creato nella console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment).
* Se in una pagina in corso di pubblicazione viene utilizzato un *frammento non pubblicato*, è possibile pubblicare anche quest’ultimo allo stesso tempo.

## Esportazione di frammenti di contenuto {#exporting-content-fragments}

Per l’esportazione in Adobe Target, è possibile utilizzare JSON per distribuire il frammento. Consulta:

* [Integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Esportazione di frammenti di contenuto in Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)
