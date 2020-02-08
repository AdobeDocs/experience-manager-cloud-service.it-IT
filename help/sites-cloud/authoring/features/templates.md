---
title: Creazione di modelli di pagina
description: Un modello definisce la struttura della pagina risultante. Con l’Editor modelli, la creazione e manutenzione dei modelli non è più un’attività riservata agli sviluppatori.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Creazione di modelli di pagina {#creating-page-templates}

Quando si crea una pagina, è necessario selezionare un modello da utilizzare come base per la creazione della nuova pagina. Il modello definisce la struttura della pagina risultante, eventuali contenuti iniziali e i componenti che possono essere utilizzati.

Con l’**Editor modelli**, la creazione e la manutenzione dei modelli non è più un compito riservato agli sviluppatori. È possibile coinvolgere anche un tipo di utente avanzato, ossia l’**autore del modello**. Agli sviluppatori spetta il compito di configurare l’ambiente, creare librerie client e creare i componenti da usare, ma una volta che queste basi sono state definite, l’**autore del modello** potrà creare e configurare un modello senza un progetto di sviluppo.

Tramite la **Console dei modelli**, gli autori dei modelli possono:

* Creare un nuovo modello o copiarne uno esistente.
* Gestire il ciclo di vita del modello.

Tramite l’**Editor modelli**, gli autori dei modelli possono:

* Aggiungere componenti al modello e posizionarli su una griglia reattiva.
* Preconfigurare i componenti.
* Definire quali componenti possono essere modificati nelle pagine create con il modello.

Questo documento spiega come un **autore di modelli** può usare la console e l’editor per creare e gestire modelli modificabili.

Per informazioni dettagliate su come funzionano i modelli modificabili a livello tecnico, consulta il documento per sviluppatori Modelli di pagina - Modificabili. <!-- For detailed information about how editable templates work at a technical level, please see the developer document [Page Templates - Editable](/help/sites-developing/page-templates-editable.md) for more information.-->

>[!NOTE]
>
>L’**Editor modelli** non supporta il targeting direttamente a livello di modello. È possibile impostare il targeting per le pagine basate su un modello modificabile, ma non per i modelli stessi.

## Prima di iniziare {#before-you-start}

>[!NOTE]
>
>Un amministratore deve configurare una cartella di modelli nel **browser delle configurazioni** e applicare le autorizzazioni appropriate prima che un autore possa creare un modello in tale cartella.

Prima di iniziare, è importante considerare che la creazione di un nuovo modello richiede collaborazione. Per questo motivo per ogni attività è indicato il relativo [Ruolo. ](#roles) Ciò non influisce sul modo in cui un modello viene effettivamente utilizzato per creare una pagina, ma influisce sul modo in cui una pagina si collega al suo modello.

### Ruoli {#roles}

La creazione di un nuovo modello utilizzando la **Console modelli** e l’**Editor modelli** richiede la collaborazione tra i seguenti ruoli:

* **Amministratore**:
   * Creates a new folder for templates requires `admin` rights.
   * Tali compiti possono spesso essere svolti anche da uno sviluppatore
* **Sviluppatore**:
   * Si concentra sui dettagli tecnici o interni
   * Deve avere esperienza con l’ambiente di sviluppo.
   * Fornisce all’autore del modello le informazioni necessarie.
* **Autore del modello**:
   * This is a specific author who is member of the group `template-authors`
      * In questo modo vengono assegnati i privilegi e le autorizzazioni necessarie.
   * Può configurare l’uso di componenti e altri dettagli di alto livello che richiedono:
      * Alcune conoscenze tecniche
         * Ad esempio, l’uso di schemi ricorrenti quando si definiscono i percorsi.
      * Informazioni tecniche fornite dallo sviluppatore.

A causa della natura di alcune attività, come la creazione di una cartella, è necessario un ambiente di sviluppo, e questo richiede conoscenza ed esperienza.

I compiti descritti nel presente documento sono elencati con il ruolo di responsabilità per il loro svolgimento.

## Creazione e gestione di modelli {#creating-and-managing-templates}

Durante la creazione di un nuovo modello modificabile:

* Utilizza la console dei **Modelli**. Questa funzione è disponibile nella sezione **Generale** della console degli **Strumenti**.
   * O direttamente da: `https://<host>:<port>/libs/wcm/core/content/sites/templates.html/conf`
* Can [create a folder for the templates](#creating-a-template-folder-admin) if necessary
* [Crea un nuovo modello](#creating-a-new-template-template-author), che sarà inizialmente vuoto.
* Se necessario, [definisci proprietà aggiuntive](#defining-template-properties-template-author) per il modello.
* [Modifica il modello](#editing-templates-template-authors) per definire i seguenti elementi:
   * [Struttura](#editing-a-template-structure-template-author) : contenuto predefinito che non può essere modificato sulle pagine create con il modello.
   * [Contenuto](#editing-a-template-initial-content-author) iniziale - Contenuto predefinito che può essere modificato sulle pagine create con il modello.
   * [Layout](#editing-a-template-layout-template-author) - Per una serie di dispositivi.
   * [Stili](/help/sites-cloud/authoring/features/style-system.md): definisci gli stili da utilizzare con il modello e i suoi componenti.
* [Attiva il modello](#enabling-a-template-template-author) per l’uso durante la creazione di una pagina.
* [Consenti il modello](#allowing-a-template-author) per la pagina o la sezione richiesta del sito web.
* [Pubblica il modello](#publishing-a-template-template-author) per renderlo disponibile nell’ambiente di pubblicazione.

>[!NOTE]
>
>I **Modelli consentiti** sono spesso predefiniti al momento della configurazione iniziale del sito Web.

>[!CAUTION]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. <!-- Never enter any information that needs to be [internationalized](/help/sites-developing/i18n.md) into a template.-->
>
>Per gli elementi modello come intestazioni e piè di pagina che devono essere localizzati, utilizzate le funzioni di [localizzazione dei componenti core.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/localization.html)

### Creazione di una cartella di modelli - Amministratore {#creating-a-template-folder-admin}

È necessario creare una cartella di modelli per il progetto, che conterrà i modelli specifici per il progetto. Si tratta di un’operazione amministrativa descritta nel documento Modelli di pagina - Modificabili. <!-- A template folder should be created for your project to hold your project-specific templates. This is an admin task and is described in the document [Page Templates - Editable](/help/sites-developing/page-templates-editable.md#template-folders).-->

### Creazione di un nuovo modello - Autore del modello {#creating-a-new-template-template-author}

1. Open the **Templates Console** (via **Tools ->** **General**) then navigate to the required folder.

   >[!NOTE]
   >
   >In a standard AEM instance the **global** folder already exists in the template console. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello.
   >
   >Si consiglia di utilizzare una cartella di modelli creata per il progetto. <!-- It is recommended best practice to use a [template folder created for your project](/help/sites-developing/page-templates-editable.md#template-folders).-->

1. Seleziona **Crea**, seguito da **Crea modello** per aprire la procedura guidata.

1. Scegli un **Tipo di modello**, quindi seleziona **Avanti**.

   >[!NOTE]
   >
   >I tipi di modello sono layout predefiniti e possono essere pensati come modelli per un modello. Questi sono predefiniti dagli sviluppatori o dall’amministratore di sistema. Per ulteriori informazioni consulta il documento per sviluppatori Modelli di pagina - Modificabili. <!-- More information can be found in the developer document [Page Templates - Editable](/help/sites-developing/page-templates-editable.md#template-type).-->

1. Completa i **Dettagli modello**:

   * **Nome modello**
   * **Descrizione**

1. Seleziona **Crea**. Viene visualizzata una conferma; seleziona **Apri** per iniziare a modificare il modello o **Fine** per tornare alla console dei modelli.

   >[!NOTE]
   >
   >Quando viene creato un nuovo modello, questo viene contrassegnato come **Bozza** nella console, a indicare che non è ancora disponibile per l’uso da parte degli autori di pagine.

### Definizione delle proprietà del modello - Autore del modello {#defining-template-properties-template-author}

Un modello può avere le seguenti proprietà:

* Immagine
   * Immagine da utilizzare come [miniatura del modello](#template-thumbnail-image) per facilitarne la selezione, ad esempio nella procedura guidata Crea pagina.
      * Può essere caricata
      * Può essere generata in base al contenuto del modello
* Titolo
   * Titolo utilizzato per identificare il modello, ad esempio nella procedura guidata **Crea pagina**.
* Descrizione
   * An optional description to provide more information about the template and its use, which can be seen for example in the **Create Page** wizard.

Per visualizzare e/o modificare le proprietà:

1. In the **Templates Console**, select the template.
1. Seleziona **Visualizza proprietà** dalla barra degli strumenti o le opzioni rapide per aprire la finestra di dialogo.
1. Ora è possibile visualizzare o modificare le proprietà del modello.

>[!NOTE]
>
>Lo stato di un modello (bozza, attivato o disattivato) è indicato nella console.

#### Immagine della miniatura del modello {#template-thumbnail-image}

Per definire la miniatura del modello:

1. Modifica le proprietà del modello.
1. Scegli se caricare una miniatura o generarla dal contenuto del modello.
   * Per caricare una miniatura, tocca o fai clic su **Carica immagine**.
   * Per generare una miniatura, tocca o fai clic su **Genera anteprima**.
1. Per entrambi i metodi verrà visualizzata un’anteprima della miniatura.
   * Se non è soddisfacente, tocca o fai clic su **Cancella** per caricare un’altra immagine o rigenerare l’anteprima.
1. Una volta ottenuta la miniatura desiderata, tocca o fai clic su **Salva e chiudi**.

### Abilitazione e autorizzazione di un modello - Autore del modello {#enabling-and-allowing-a-template-template-author}

Per poter utilizzare un modello quando si crea una pagina, è necessario svolgere le seguenti operazioni:

* [Abilitate il modello](#enabling-a-template-template-author) per renderlo disponibile per la creazione di pagine.
* [Consentite al modello](#allowing-a-template-author) di specificare i rami di contenuto in cui può essere utilizzato il modello.

#### Abilitazione di un modello - Autore del modello {#enabling-a-template-template-author}

Un modello può essere attivato o disattivato per renderlo disponibile o non disponibile nella procedura guidata **Crea pagina**.

>[!CAUTION]
>
>Una volta abilitato un modello, verrà visualizzato un avviso quando un autore inizia ad aggiornarlo ulteriormente. In tal modo l’utente viene informato di un potenziale riferimento al modello, e che eventuali modifiche potrebbero quindi influenzare le pagine che vi fanno riferimento.

1. In the **Templates Console**, select the template.
1. Select **Enable** or **Disable** from the toolbar, and again in the confirmation dialog.
1. È ora possibile utilizzare il modello quando si [crea una nuova pagina](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page), anche se probabilmente si vorrà [modificare il modello](#editing-templates-template-authors) in base a specifiche esigenze.

>[!NOTE]
>
>Lo stato di un modello (bozza, attivato o disattivato) è indicato nella console.

#### Consentire un modello - Autore {#allowing-a-template-author}

Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

1. Apri le [Proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md) per la pagina principale del ramo in cui desideri rendere disponibile il modello.
1. Apri la scheda **Avanzate**.
1. Under **Template Settings** use **Add field** to specify the path(s) to your template(s).

   Il percorso può essere esplicito o utilizzare schemi ricorrenti. Esempio:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   L’ordine dei percorsi è irrilevante; tutti i percorsi vengono scansionati e gli eventuali modelli recuperati.

   >[!NOTE]
   >
   >Se l’elenco dei **Modelli consentiti** viene lasciato vuoto, l’albero viene asceso fino a quando non viene trovato un valore o un elenco.
   >
   >
   >See Template Availability - the principles for allowed templates remain the same. <!--See [Template Availability](/help/sites-developing/templates.md#template-availability) - the principles for allowed templates remain the same.-->

1. Fai clic su **Salva** per salvare le modifiche alle proprietà della pagina.

>[!NOTE]
>
>Spesso i modelli consentiti sono predefiniti per l’intero sito quando è configurato.

### Pubblicazione di un modello - Autore del modello {#publishing-a-template-template-author}

Poiché al modello viene fatto riferimento quando viene eseguito il rendering di una pagina, il modello completamente configurato deve essere pubblicato in modo che sia disponibile nell’ambiente di pubblicazione.

1. In the **Templates Console**, select the template.
1. Select **Publish** from the toolbar to open the wizard.
1. Seleziona **Criteri per contenuto** da pubblicare in tandem.
1. Seleziona **Pubblica** nella barra degli strumenti per completare l’azione.

## Modifica dei modelli - Autori dei modelli {#editing-templates-template-authors}

Quando si crea o si modifica un modello, è possibile definire vari aspetti. La modifica dei modelli è simile alla creazione delle pagine.

Il selettore **Modalità** nella barra degli strumenti consente di selezionare e modificare l’aspetto appropriato del modello:

* [Struttura](#editing-a-template-structure-template-author)
* [Contenuto iniziale](#editing-a-template-initial-content-author)
* [Layout](#editing-a-template-layout-template-author)

![Selettore modalità editor modelli](/help/sites-cloud/authoring/assets/templates-mode.png)

L’opzione **Criterio pagina** nel menu **Informazioni pagina** consente invece di [selezionare i criteri di pagina richiesti](#page-policies):

![Informazioni pagina Editor modelli](/help/sites-cloud/authoring/assets/templates-page-information.png)

>[!CAUTION]
>
>Se un autore inizia a modificare un modello che è già stato abilitato, verrà visualizzato un avviso. In tal modo l’utente viene informato di un potenziale riferimento al modello, e che eventuali modifiche potrebbero quindi influenzare le pagine che vi fanno riferimento.

### Attributi modello {#template-attributes}

Potete modificare i seguenti attributi di un modello:

#### Struttura {#template-structure}

Components added to the [structure](#editing-a-template-structure-template-author) cannot be moved/removed from resultant pages by the page authors. Se si desidera permettere agli autori delle pagine di aggiungere e rimuovere componenti alle pagine risultanti, è necessario aggiungere un sistema di paragrafi al modello.

Quando i componenti sono bloccati, è possibile aggiungere contenuti e questi ultimi possono essere modificati dagli autori delle pagine. È possibile sbloccare i componenti per consentire la definizione del [Contenuto iniziale](#editing-a-template-initial-content-author).

>[!NOTE]
>
>In modalità Struttura, tutti i componenti che sono l’elemento padre di un componente sbloccato non possono essere spostati, tagliati o cancellati.

#### Contenuto iniziale {#template-initial-content}

When a component has been unlocked you can define the [initial content](#editing-a-template-initial-content-author) that will be copied to the resultant page(s), created from the template. I componenti sbloccati possono essere modificati nella pagina o nelle pagine risultanti.

>[!NOTE]
>
>Nella modalità **Contenuto iniziale** e nelle pagine risultanti, tutti i componenti sbloccati che hanno un elemento padre accessibile (ad esempio i componenti all’interno di un contenitore di layout) possono essere eliminati.

#### Layout {#template-layout}

With the [layout](#editing-a-template-layout-template-author) you can predefine the template layout for the required device formats. La modalità **Layout** per la creazione dei modelli ha le stesse funzionalità della modalità [**Layout **per la creazione delle pagine.](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)

#### Criteri pagina {#template-page-policies}

[I criteri](#page-policies) di pagina possono collegare alla pagina criteri di pagina predefiniti. I criteri di pagina definiscono le varie configurazioni di progettazione.

#### Stili {#template-styles}

The [Style System](/help/sites-cloud/authoring/features/style-system.md) allows a template author to define style classes in the content policy of a component so that a content author is able to select them when editing the component on a page. Gli stili possono essere varianti visive alternative di un componente, per renderlo più flessibile.

Per ulteriori informazioni, consulta la [documentazione sul sistema di stili](/help/sites-cloud/authoring/features/style-system.md).

### Modifica di un modello - Struttura - Autore del modello {#editing-a-template-structure-template-author}

In **Structure** mode you define components and content for your template and define policy for the template and its components.

* I componenti definiti nella struttura del modello non possono essere spostati su una pagina risultante, né eliminati da alcuna pagina risultante.
* Se desideri che gli autori delle pagine siano in grado di aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
* I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il [contenuto iniziale](#editing-a-template-initial-content-author).
* Vengono definiti i criteri di design per i componenti e la pagina.

![Struttura delle pagine Editor modelli](/help/sites-cloud/authoring/assets/templates-page-structure.png)

Nella modalità **Struttura** dell’editor modelli è possibile eseguire diverse azioni e numerose funzioni per facilitare l’utente:

#### Add Components {#add-components}

Ci sono diversi meccanismi per aggiungere componenti ai modelli:

* Dal browser **Componenti** nel pannello laterale.
* By using the **Insert Component** option available on the toolbar of components already on the template or the **Drag components here** box.
* Trascinando una risorsa (dal browser **Risorse** nel pannello laterale) direttamente sul modello per generare il componente appropriato in situ.

Una volta aggiunto, ogni componente è contrassegnato con:

* Un bordo
* Un marcatore che indica il tipo di componente
* Un marcatore che indica se il componente è stato sbloccato

>[!NOTE]
>
>When you add an out-of-the-box **Title** component to the template it will contain the default text **structure**.
>
>Se si modifica questa impostazione e si aggiunge un proprio testo, questo testo aggiornato verrà utilizzato quando si crea una pagina dal modello.
>
>Se si lascia il testo (struttura) predefinito, il titolo predefinito corrisponde al nome della pagina risultante.

>[!NOTE]
>
>Although not identical, adding components and assets to a template has many similarities to similar actions when [page authoring](/help/sites-cloud/authoring/fundamentals/editing-content.md).

#### Azioni dei componenti {#component-actions}

Una volta aggiunte al modello, esegui le azioni sui componenti. Ogni singola istanza ha una barra degli strumenti che permette di accedere alle azioni disponibili e che dipende dal tipo di componente.

![Barra delle azioni di un componente modello](/help/sites-cloud/authoring/assets/templates-component-actions.png)

Può anche dipendere dalle azioni intraprese, ad esempio se un criterio è stato associato al componente, in tal caso l’icona di configurazione del progetto diventa disponibile.

#### Modifica e Configura {#edit-and-configure}

Con queste due azioni è possibile aggiungere contenuti ai componenti.

#### Border to Indicate Structure {#border-to-indicate-structure}

Quando si lavora in modalità **Struttura**, un bordo arancione indica il componente attualmente selezionato. Una linea tratteggiata indica il componente padre.

#### Criteri e proprietà (Generale) {#policy-and-properties-general}

I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello).

Crea un criterio per i contenuti o selezionane uno esistente per un componente.

![Pulsante Criterio contenuto](/help/sites-cloud/authoring/assets/templates-content-policy-button.png)

In questo modo è possibile definire i dettagli del progetto.

![Criteri contenuto](/help/sites-cloud/authoring/assets/template-content-policy.png)

La finestra di configurazione è divisa in due parti.

* In the left side of the dialogue under **Policy**, you have the ability to select an existing policy or select an existing one.
* In the right side of the dialogue under **Properties**, you can set the properties specific to the component type.

Le proprietà disponibili dipendono dal componente selezionato. Ad esempio, per un componente di testo, le proprietà definiscono, tra le altre opzioni, quelle di copia e incolla, formattazione e stile del paragrafo.

##### Criterio {#policy}

I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello).

Under **Policy** you can select an existing policy to apply to the component via the drop-down.

![Seleziona criterio](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

Puoi aggiungere un nuovo criterio selezionando il pulsante di aggiunta accanto al menu a discesa **Seleziona criterio**. A new title should then be given in the **Policy Title** field.

![Pulsante Aggiungi criterio](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

Il criterio esistente selezionato nel menu a discesa **Seleziona criterio** può essere copiato come nuovo criterio utilizzando il pulsante Copia, accanto al menu a discesa. A new title should then be given in the **Policy Title** field. By default the copied policy will be titled **Copy of X**, where X is the title of the copied policy.

![Pulsante Copia criterio](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

La descrizione del criterio nel campo **Descrizione criterio** è facoltativa.

In the **Other templates also using the selected policy** section, you can easily see which other templates use the policy selected in the **Select policy** dropdown.

![Utilizzo del criterio esistente](/help/sites-cloud/authoring/assets/templates-policy-use.png)

>[!NOTE]
>
>Se vengono aggiunti come contenuto iniziale più componenti dello stesso tipo, lo stesso criterio si applica a tutti i componenti.

##### Proprietà {#properties}

In **Proprietà** puoi definire le impostazioni del componente. Sono disponibili due schede:

* Principale
* Funzioni

###### Principale {#main}

Nella scheda **Principale** sono definite le impostazioni più importanti del componente.

Ad esempio, per un componente immagine è possibile definire le larghezze consentite e abilitare il caricamento lento.

Se per un’impostazione sono consentite più configurazioni, tocca o fai clic sul pulsante **Aggiungi** per aggiungerne un’altra.

![Pulsante Aggiungi](/help/sites-cloud/authoring/assets/templates-add-button.png)

Per rimuovere una configurazione, tocca o fai clic sul pulsante **Elimina** situato a destra della configurazione.

Per rimuovere una configurazione, tocca o fai clic sul pulsante **Elimina**.

![Pulsante Elimina](/help/sites-cloud/authoring/assets/templates-delete-button.png)

###### Funzioni {#features}

La scheda **Funzioni** consente di attivare o disattivare funzioni aggiuntive del componente.

Ad esempio, per un componente immagine è possibile definire le proporzioni di ritaglio, gli orientamenti consentiti e se il caricamento è ammesso.

![Scheda Funzioni](/help/sites-cloud/authoring/assets/templates-features-tab.png)

>[!CAUTION]
>
>Note that in AEM crop ratios are defined as **height/width**. Ciò è diverso dalla definizione convenzionale di larghezza/altezza ed è fatto per motivi di compatibilità legacy. Gli utenti che creano le pagine non noteranno alcuna differenza, purché sia stato definito chiaramente il **Nome**, che verrà visualizzato nell’interfaccia utente.

>[!NOTE]
>
>I criteri dei contenuti per i componenti si avvalgono dell’editor Rich Text possono essere definiti solo per le opzioni disponibili mediante tale editor tramite le impostazioni di interfaccia utente. <!--[Content policies for components implementing the rich text editor](/help/sites-administering/rich-text-editor.md#main-pars-header-206036638) can only be defined for options made available by the RTE through its UI settings.-->

#### Policy and Properties (Layout Container) {#policy-and-properties-layout-container}

Le impostazioni di criteri e proprietà di un contenitore di layout sono simili a quelle di uso generale, ma con alcune differenze.

>[!NOTE]
>
>La configurazione di un criterio è obbligatoria per i componenti contenitore, in quanto consente di definire i componenti che saranno disponibili nel contenitore.

La finestra di configurazione è divisa in due, come la finestra per uso generale.

##### Criterio {#policy-layout}

I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello).

Under **Policy** you can select an existing policy to apply to the component via the drop-down. Questo funziona come nell’uso generale della finestra.

##### Proprietà {#properties-layout}

In **Proprietà** è possibile scegliere quali componenti sono disponibili per il contenitore layout e definirne le impostazioni. Sono disponibili tre schede:

* Componenti consentiti
* Componenti standard
* Impostazioni reattive

###### Componenti consentiti {#allowed-components}

Nella scheda **Componenti consentiti**, definisci quali componenti sono disponibili per il contenitore layout.

* I componenti sono raggruppati in base ai gruppi di componenti, che possono essere espansi e ridotti.
* Per selezionare tutti i componenti di un gruppo, attiva la casella del nome del gruppo; per deselezionare tutti i componenti di un gruppo, disattiva questa casella.
* Se la casella contiene un meno (-) significa che è selezionato almeno un elemento del gruppo, ma non tutti.
* È disponibile un sistema di ricerca per filtrare i componenti in base al nome.
* Il numero a destra del nome di un gruppo di componenti indica quanti sono i componenti selezionati in tale gruppo, a prescindere dal filtro.

![Scheda Componenti consentiti](/help/sites-cloud/authoring/assets/templates-allowed-components-tab.png)

###### Componenti standard {#default-components}

Nella scheda **Componenti standard**, definisci quali componenti vengono associati automaticamente a determinati tipi di file multimediali in modo che, quando un autore trascina una risorsa dal browser delle risorse, AEM sappia a quale componente associarla. Per questa configurazione sono disponibili solo componenti con zone di rilascio.

Tocca o fai clic su **Aggiungi mappatura** per aggiungere un componente completamente nuovo e la mappatura del tipo MIME.

Seleziona un componente nell’elenco e o fai clic su **Aggiungi tipo** per aggiungere un ulteriore tipo MIME a un componente già mappato. Click the **Delete** icon to remove a MIME type.

![Scheda Componenti predefiniti](/help/sites-cloud/authoring/assets/templates-default-components-tab.png)

###### Impostazioni reattive {#responsive-settings}

Nella scheda **Impostazioni reattive** è possibile configurare il numero di colonne nella griglia risultante del contenitore layout.

#### Sblocca e blocca componenti {#unlock-and-lock-components}

Sblocca o blocca i componenti per definire se il contenuto è disponibile per la modifica in modalità **Contenuto iniziale**.

Quando un componente è stato sbloccato:

* Sul bordo è visualizzato un indicatore di lucchetto aperto.
* La barra degli strumenti dei componenti verrà regolata di conseguenza.
* I contenuti già inseriti non verranno più visualizzati in modalità **Struttura**.
   * Already entered content is considered initial content and is only visible in **Initial Content** mode.
* L’elemento padre di un componente sbloccato non può essere spostato, tagliato o cancellato.

![Pulsante Blocca componente](/help/sites-cloud/authoring/assets/templates-unlock-component.png)

Questo include lo sblocco dei componenti del contenitore in modo che possano essere aggiunti altri componenti, sia in modalità **Contenuto iniziale** che nelle pagine risultanti. Se sono già stati aggiunti componenti o contenuti al contenitore prima di sbloccarlo, questi non verranno più visualizzati in modalità **Struttura**, ma in modalità **Contenuto iniziale**. In **Modalità struttura**, verrà mostrato solo il componente del contenitore stesso con il suo elenco di **Componenti consentiti**.

![Componenti consentiti](/help/sites-cloud/authoring/assets/templates-allowed-components.png)

Per risparmiare spazio, il Contenitore di layout non cresce per contenere l&#39;elenco dei componenti consentiti. Piuttosto il contenitore diventa un elenco scorrevole.

I componenti configurabili vengono visualizzati con un’icona **Criteri**, che può essere toccata o cliccata per modificare i criteri e le proprietà di tale componente.

![Icona del componente configurabile](/help/sites-cloud/authoring/assets/templates-configurable-component.png)

#### Relazione con le pagine esistenti {#relationship-to-existing-pages}

Se la struttura viene aggiornata dopo la creazione di pagine basate sul modello, a tali pagine verranno applicate le modifiche apportate al modello. Questo fatto è segnalato da un avviso nella barra degli strumenti e da finestre di dialogo di conferma.

![Avviso del banner relativo al modello in uso](/help/sites-cloud/authoring/assets/templates-in-use-banner.png)

### Modifica di un modello - Contenuto iniziale - Autore {#editing-a-template-initial-content-author}

La modalità **Contenuto iniziale** viene utilizzata per definire il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello. Il contenuto iniziale può quindi essere modificato dagli autori delle pagine.

Sebbene tutto il contenuto creato in modalità **Struttura** sia visibile nel **Contenuto iniziale**, solo i componenti sbloccati possono essere selezionati e modificati.

>[!NOTE]
>
>La modalità **Contenuto iniziale** è in pratica una modalità di modifica per le pagine create con quel modello. Pertanto, i criteri non vengono definiti in modalità **Contenuto iniziale**, ma in [**modalità Struttura **](#editing-a-template-structure-template-author).

* I componenti sbloccati disponibili per la modifica sono contrassegnati. Quando sono selezionati, hanno un bordo blu:

   ![Modalità contenuto iniziale](/help/sites-cloud/authoring/assets/templates-initial-content-mode.png)

* I componenti sbloccati dispongono di una barra degli strumenti che consente di modificare e configurare il contenuto:

   ![Componente sbloccato](/help/sites-cloud/authoring/assets/templates-unlocked-components.png)

* Se un componente del contenitore è stato sbloccato (in modalità **Struttura**), è possibile aggiungervi nuovi componenti (in modalità **Contenuto iniziale).** I componenti aggiunti in modalità **Contenuto iniziale** possono essere spostati o eliminati dalle pagine risultanti.

   È possibile aggiungere un componente utilizzando l’area **Trascina qui i componenti** o l’opzione **Inserisci nuovo componente** dalla barra degli strumenti del contenitore appropriato.

   ![Aggiungi componente](/help/sites-cloud/authoring/assets/templates-add-component.png)
   ![Aggiungi componente](/help/sites-cloud/authoring/assets/templates-add-component-dialog.png)

* Se il contenuto iniziale del modello viene aggiornato dopo la creazione delle pagine basate sul modello, tali pagine non saranno influenzate dalle modifiche apportate al contenuto iniziale del modello.

>[!NOTE]
>
>Il contenuto iniziale è destinato alla preparazione dei componenti e del layout di pagina che fungono da punto di partenza per la creazione dei contenuti. Non è inteso come contenuto effettivo da mantenere così com’è. Per questo motivo, non può essere tradotto.
>
>Per includere nel modello testo convertibile, ad esempio nelle intestazioni o nei piè di pagina, potete utilizzare le funzioni di [localizzazione dei componenti](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/localization.html)core.

### Modifica di un modello - Layout - Autore del modello {#editing-a-template-layout-template-author}

È possibile definire il layout del modello per una serie di dispositivi. [Il layout](/help/sites-cloud/authoring/features/responsive-layout.md) reattivo per i modelli funziona come per l&#39;authoring delle pagine.

>[!NOTE]
>
>Le modifiche al layout verranno applicate in modalità **Contenuto iniziale**, ma non in modalità **Struttura**.

![Modificare il layout del modello](/help/sites-cloud/authoring/assets/templates-edit-layout.png)

### Editing a Template - Page Policy - Template Author/Developer {#editing-a-template-page-policy-template-author-developer}

I criteri di pagina, comprese le librerie lato client, vengono mantenuti sotto l’opzione Criteri **** pagina del menu Informazioni **** pagina.

To access the **Page Policy** dialog:

1. From the **Template Editor**, select **Page Information** from the toolbar, then **Page Policy** to open the dialog.
1. The **Page Policy** dialog opens and is divided into two sections:

   * Nella metà sinistra si definiscono i [criteri della pagina](#page-policies).
   * Nella metà destra si definiscono le [proprietà della pagina](#page-properties).
   ![Progettazione pagina](/help/sites-cloud/authoring/assets/templates-page-design.png)

#### Criteri pagina {#page-policies}

È possibile applicare un criterio per i contenuti al modello o alle pagine risultanti. In tal modo si definiscono i criteri dei contenuti per il sistema di paragrafi principale della pagina.

![Criterio pagina](/help/sites-cloud/authoring/assets/templates-page-policy.png)

* Puoi selezionare un criterio esistente per la pagina dal menu a discesa **Seleziona criterio**.

   ![Selettore criteri](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

   Puoi aggiungere un nuovo criterio selezionando il pulsante di aggiunta accanto al menu a discesa **Seleziona criterio**. A new title should then be given in the **Policy Title** field.

   ![Pulsante Aggiungi criterio](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

   Il criterio esistente selezionato nel menu a discesa **Seleziona criterio** può essere copiato come nuovo criterio utilizzando il pulsante Copia, accanto al menu a discesa. A new title should then be given in the **Policy Title** field. By default the copied policy will be titled **Copy of X**, where X is the title of the copied policy.

   ![Pulsante Copia criterio](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

* Aggiungi un titolo al criterio nel campo **Titolo criterio**. Un criterio deve avere un titolo che permetta di riconoscerlo facilmente nel menu a discesa **Seleziona criterio**.

   ![Titolo criterio](/help/sites-cloud/authoring/assets/templates-policy-title.png)

* La descrizione del criterio nel campo **Descrizione criterio** è facoltativa.
* In the **Other templates also using the selected policy** section, you can easily see which other templates use the policy selected in the **Select policy** dropdown.

   ![Utilizzo dei criteri](/help/sites-cloud/authoring/assets/templates-policy-use.png)

#### Proprietà pagina {#page-properties}

Using page properties, you can define the required client-side libraries by using the **Page Design** dialog. Le librerie lato client includono fogli di stile e Javascript da caricare con il modello e le pagine create con tale modello.

![Proprietà pagina](/help/sites-cloud/authoring/assets/templates-page-properties.png)

* Specifica le librerie lato client da applicare alle pagine create con questo modello. Immetti il nome di una libreria nel campo di testo nella sezione **Librerie lato client**.

   ![Librerie lato client](/help/sites-cloud/authoring/assets/templates-client-side-libraries.png)

* Se sono necessarie più librerie, fai clic sul pulsante Aggiungi per aggiungere un ulteriore campo di testo al nome della libreria.

   ![Pulsante Aggiungi](/help/sites-cloud/authoring/assets/templates-add-button.png)

   Aggiungi tutti i campi di testo necessari per le librerie lato client.

* Se necessario, definisci la posizione relativa delle librerie trascinando i campi con la maniglia di trascinamento.

   ![Trascinamento della maniglia](/help/sites-cloud/authoring/assets/templates-drag-handle.png)

>[!NOTE]
>
>L’autore del modello può specificare il criterio della pagina sul modello, ma dovrà ottenere i dettagli delle librerie appropriate lato client dallo sviluppatore.

### Modifica di un modello - Proprietà pagina iniziale - Autore {#editing-a-template-initial-page-properties-author}

L’opzione **Proprietà pagina iniziale** consente di definire le [proprietà della pagina iniziale](/help/sites-cloud/authoring/fundamentals/page-properties.md) da utilizzare per la creazione delle pagine risultanti.

1. Dall’editor dei modelli, seleziona **Informazioni pagina** dalla barra degli strumenti, quindi **Proprietà pagina iniziale** per aprire la finestra di dialogo.

1. Nella finestra di dialogo è possibile definire le proprietà che si desidera applicare alle pagine create con questo modello.

   ![Proprietà pagina iniziale dei modelli](/help/sites-cloud/authoring/assets/templates-initial-properties.png)

1. Conferma le definizioni con **Fine**.

## Best practice {#best-practices}

Quando si creano modelli, è necessario considerare i seguenti aspetti:

1. L’impatto delle modifiche apportate al modello, una volta che sono state create delle pagine da quel modello.

   Ecco un elenco delle diverse operazioni possibili sui modelli e di come influenzano le pagine create da essi:

   * Modifiche alla struttura:

      * Vengono immediatamente applicate alle pagine risultanti.
      * È comunque necessario pubblicare il modello modificato affinché i visitatori possano vedere le modifiche.
   * Modifiche ai criteri dei contenuti e alle configurazioni di progettazione:

      * Vengono applicate immediatamente alle pagine risultanti.
      * È necessario pubblicare le modifiche affinché i visitatori possano vederle.
   * Modifiche al contenuto iniziale:

      * Vengono applicate solo alle pagine create dopo la modifica del modello.
   * Le modifiche al layout dipendono dal ruolo del componente modificato:

      * Solo struttura: vengono applicate immediatamente.
      * Con contenuto iniziale: vengono applicate immediatamente solo alle pagine create dopo la modifica
   Si consiglia di prestare particolare attenzione nei seguenti casi:

   * Blocco o sblocco di componenti su modelli abilitati.
   * Questo può avere effetti collaterali, in quanto le pagine esistenti possono già essere in uso. In genere:

      * I componenti sbloccati (precedentemente bloccati) saranno assenti dalle pagine esistenti.
      * I componenti bloccati (che erano modificabili) nascondono il contenuto dalla visualizzazione sulle pagine.
   >[!NOTE]
   >
   >AEM fornisce avvisi espliciti quando si modifica lo stato di blocco di componenti su modelli che non sono più bozze.

1. [Creazione di cartelle personalizzate](#creating-a-template-folder-admin) per i modelli specifici del sito.
1. [Pubblica i modelli](#publishing-a-template-template-author) dalla console **Modelli**.
