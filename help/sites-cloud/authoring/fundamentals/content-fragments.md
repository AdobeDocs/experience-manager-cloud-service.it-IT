---
title: Frammenti di contenuto
description: I frammenti di contenuto di Adobe Experience Manager as a Cloud Service consentono di progettare, creare, redigere e utilizzare contenuti indipendenti dalla pagina.
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
source-git-commit: 624b202efd08243e91b36a35f3df7c8c0bd998a9
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 100%

---

# Frammenti di contenuto {#content-fragments}

I frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/sites-cloud/administering/content-fragments/content-fragments.md).

Consentono di creare contenuti versatili utilizzabili in qualsiasi canale, con possibili varianti per canali specifici. Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto.

Insieme alla funzione di esportazione JSON aggiornata, i frammenti di contenuto strutturati possono anche essere utilizzati per distribuire contenuti AEM, tramite Content Services a canali diversi dalle pagine AEM.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** sono funzioni diverse in AEM:
>
>* I **frammenti di contenuto** sono contenuti editoriali, in particolare testo e immagini correlate. Sono contenuti puri, privi di design e layout.
>* I **frammenti esperienza** sono contenuti con un layout completo e di conseguenza frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.

>[!CAUTION]
>
>Questa pagina deve essere letta insieme a [Utilizzo dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md) (e pagine correlate), in quanto introduce la terminologia e i concetti di base e spiega come creare e gestire i frammenti.

I frammenti di contenuto si prestano alle seguenti applicazioni:

* **Strategia di marketing e campagne**
   * Revisione dei contenuti tramite frammenti di contenuto gestiti a livello centrale.
* **Creativi professionisti**
   * Monitoraggio delle risorse creative tramite raccolte associate a frammenti di contenuto.
* **Copywriter**
   * Creazione di contenuti nell’editor frammento di contenuto di AEM.
   * Creazione di varianti del contenuto.
   * Associazione di contenuti rilevanti ai frammenti di contenuto.
   * Uso delle funzioni di gestione versioni/flusso di lavoro.
   * Condivisione dei frammenti di contenuto.
   * Gestione delle traduzioni a livello centrale.
* **Produttori e responsabili viaggi**
   * Scelta di frammenti predefiniti ed elaborazione di varianti con l’authoring in AEM.
   * Garanzia che il frammento e il contenuto associato ad esso sono sempre aggiornati, con tutte le modifiche apportate dai copywriter e i creativi a frammenti e risorse gestiti a livello centrale.
   * Garanzia che i contenuti multimediali associati sono sempre vagliati e selezionati in base alla loro rilevanza.
   * Possibilità di creare al volo varianti di contenuto ad hoc, con la garanzia che queste restano comunque gestite a livello centrale nel frammento.

## Aggiunta di un frammento di contenuto alla pagina  {#adding-a-content-fragment-to-your-page}

1. Apri la pagina per la modifica.
2. Aggiungi il componente **Frammento di contenuto** dal browser **Componenti** o mediante il comando **Inserisci nuovo componente**.
3. Puoi effettuare le seguenti operazioni:
   * Apri il browser **Risorse** e applica il filtro **Frammenti di contenuto** (l’impostazione predefinita è Immagini). Quindi, trascina il frammento desiderato sull’istanza di componente.
   * Seleziona il componente del frammento di contenuto, quindi **Configura** dalla barra degli strumenti. Nella finestra di dialogo, apri la finestra di dialogo di selezione per individuare e selezionare il **frammento di contenuto** richiesto.

   >[!NOTE]
   >
   >In alternativa, puoi trascinare un frammento di contenuto specifico direttamente nella pagina. In questo modo verrà creato automaticamente il componente associato (Frammento di contenuto).

4. Inizialmente verrà visualizzato il contenuto dell’**elemento principale** e la **pagina mastro** (variante). Puoi [selezionare altri elementi e/o varianti](#selecting-the-element-or-variation), secondo necessità.

   ![Frammenti di contenuto nel browser Risorse](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Per informazioni su ulteriori funzionalità di modifica, vedi anche:
   >
   >* [Layout dinamico](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [Modifica del contenuto di una pagina](/help/sites-cloud/authoring/fundamentals/editing-content.md)


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
   * A seconda del modello utilizzato sarà disponibile una selezione.

   >[!NOTE]
   >
   >Gli elementi disponibili dipendono dal modello utilizzato.

* **Variazione**
   * Il **Master** predefinito sarà sempre disponibile.
   * Una selezione è disponibile se per il frammento sono state create delle varianti.

* **ID**

   * Attributo **ID HTML** da applicare al componente.

### Collegamento rapido all’editor frammento di contenuto  {#quick-connection-to-fragment-editor}

Puoi aprire l’origine del frammento in modalità di modifica (la risorsa) mediante l’icona **Modifica** nella barra degli strumenti del componente, così da poter [modificare e gestire il frammento di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Come sempre, la modifica dell’origine del frammento ha un impatto su tutte le pagine che fanno riferimento a tale frammento di contenuto.

### Aggiunta di contenuto intermedio  {#adding-in-between-content}

Quando si aggiunge alla pagina un frammento di contenuto specifico, è disponibile un segnaposto **Trascina qui i componenti** fra ciascun paragrafo HTML (nonché all’inizio e alla fine) del frammento.

Questo consente di aggiungere ulteriori contenuti [intermedi (ad esempio, contenuti intermedi)](/help/sites-cloud/administering/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) all’interno del contenuto del frammento (nei punti disponibili), senza dover modificare il frammento principale.

Per il contenuto intermedio puoi effettuare le seguenti operazioni:

* Aggiungere componenti dal [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
* Aggiungere risorse dal [browser Risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
* Usare [Contenuto associato](#using-associated-content) come origine per il contenuto intermedio.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

![Inserisci componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>Puoi anche [inserire risorse visive (immagini) nel frammento stesso](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Le risorse visive inserite nel frammento stesso sono associate al paragrafo precedente nel frammento. Non è pertanto possibile inserire contenuto intermedio tra una risorsa visiva e il paragrafo precedente. Qualora ti occorra questo livello di connessione, puoi aggiungere l’immagine al frammento (come [frammento con file multimediali diversi](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>Dopo aver aggiunto contenuto intermedio a un frammento di contenuto nella pagina, se si modifica la struttura del frammento di contenuto sottostante (ovvero nell’editor frammento di contenuto) si potrebbero verificare risultati erronei o imprevisti.
>
>In questi casi, il contenuto intermedio rimane inalterato:
>
>* I componenti intermedi hanno una posizione assoluta all’interno della sequenza di componenti nel flusso del frammento. Questa posizione resta invariata, anche quando cambia il contenuto dei paragrafi nel frammento.
>
>  Questo potrebbe dare l’impressione di una modifica nella posizione relativa, poiché i paragrafi intermedi non hanno alcuna relazione contestuale con i paragrafi (del frammento) accanto ai quali sono posizionati,
>* a meno che le due strutture di paragrafo non siano in conflitto. In questo caso il contenuto intermedio non viene visualizzato, ma resta comunque presente nel codice interno.


### Uso di contenuti associati  {#using-associated-content}

Se hai [associato del contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) al [frammento di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md), queste risorse saranno disponibili nel pannello laterale (dopo aver inserito il frammento nella pagina del contenuto). Il contenuto associato è di fatto una fonte speciale di contenuto per il [contenuto intermedio](/help/sites-cloud/administering/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Esistono diversi metodi per aggiungere [risorse visive (ad es. immagini)](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets) al frammento e/o alla pagina.

>[!NOTE]
>
>Se sulla stessa pagina sono presenti più frammenti di contenuto, la scheda **Contenuto associato** visualizza le risorse appropriate per tutti i frammenti.

Una volta aggiunto alla pagina un frammento con contenuto associato, nel pannello laterale viene aperta una nuova scheda (**Contenuto associato**).

Da qui puoi trascinare le risorse nella posizione richiesta (su un componente esistente o nella posizione in cui sarà creato il componente appropriato):

![Inserimento di un’immagine](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Risorse inserite nel frammento {#assets-inserted-into-the-fragment}

Se sono state inserite delle risorse (ad es. immagini) nel frammento stesso (come [frammenti con file multimediali diversi](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)) le opzioni per la modifica di tali risorse nell’editor pagina sono limitate.

Ad esempio, per un’immagine è possibile:

* Ritagliare, ruotare o capovolgere l’immagine.
* Aggiungere un titolo o testo alternativo.
* Specificare una dimensione.
* Puoi anche configurare il layout.

Altre modifiche, come spostamento, copia, eliminazione devono essere eseguite nell’editor frammento.

### Pubblicazione {#publishing}

I frammenti devono essere pubblicati in modo che possano essere utilizzati nelle pagine web pubblicate:

* Un frammento può essere pubblicato dopo che è stato [creato nella console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment).
* Se in una pagina in corso di pubblicazione viene utilizzato un *frammento non pubblicato*, è possibile pubblicare anche quest’ultimo allo stesso tempo.
