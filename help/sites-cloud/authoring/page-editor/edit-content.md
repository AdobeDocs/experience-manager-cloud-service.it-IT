---
title: Modifica del contenuto di una pagina con l’Editor pagina di AEM
description: L’editor pagina di AEM è uno strumento utile per la creazione dei contenuti.
exl-id: eacfda02-ff53-42ed-b5b2-88be3879a5e9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 9a798be41cb3bcf08b6841d236379bf861ff5510
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 32%

---

# Modifica del contenuto di una pagina con l’Editor pagina di AEM {#edit-content}

L’editor pagina di AEM è uno strumento utile per creare il contenuto di una pagina. Scopri come utilizzarlo per trascinare e rilasciare i contenuti e modificarli direttamente.

## Panoramica {#overview}

Nell’editor pagina puoi eseguire tre azioni di base per modificare il contenuto:

1. [Aggiunta di nuovi componenti](#adding-components) mediante trascinamento nella pagina.
1. [Aggiunta di nuove risorse](#adding-asset) mediante trascinamento nella pagina.
1. [Modifica di componenti sul posto](#edit-in-place) già esistenti nella pagina.

L’editor pagina di AEM fornisce un’interfaccia utente intuitiva per eseguire queste attività, oltre a fornire accesso a funzioni più avanzate.

Inoltre, l’editor ti consente di organizzare il contenuto esistente nella pagina consentendo di:

* [Spostare i componenti](#moving-components)
* [Modifica layout componente](#editing-component-layout)
* [Modifica ereditarietà componente](#inherited-components)

>[!NOTE]
>
>Se necessario, il team del progetto può personalizzare l’editor. Per ulteriori dettagli, vedi [Personalizzazione dell&#39;authoring delle pagine](/help/implementing/developing/extending/page-authoring.md).

## Aggiunta di componenti {#adding-components}

Puoi trascinare i nuovi componenti nella pagina selezionandoli dal browser dei componenti [nel pannello laterale](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) e rilasciandoli in un segnaposto di componente.

### Segnaposto Componente {#component-placeholder}

Il segnaposto del componente è un indicatore che mostra dove verrà posizionato un componente quando lo rilasci. Ha due apparizioni.

* Quando si aggiunge un nuovo componente alla pagina (trascinandolo dal browser dei componenti), questo viene visualizzato come una casella grigia con i dettagli del componente che si sta posizionando.

  ![Segnaposto per l’aggiunta di un nuovo componente a una pagina](assets/edit-content-component-placeholder.png)

* Quando [si sposta un componente esistente](#movging-components), questo verrà visualizzato come un quadrato blu.

  ![Segnaposto per lo spostamento di un componente esistente su una pagina](assets/edit-content-move-placeholder.png)

In entrambi i casi, la destinazione selezionata verrà visualizzata come un contorno blu sotto il componente che si sta trascinando. La destinazione se il componente viene posizionato al momento del rilascio.

### Aggiunta di un componente dal browser Componenti {#adding-a-component-from-the-components-browser}

Puoi aggiungere un nuovo componente utilizzando il [browser componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser). Il segnaposto [componente](#component-placeholder) mostra dove stai posizionando il componente.

1. Verificare che l&#39;editor di pagine sia in modalità [**Modifica**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector).
1. Apri il [browser Componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).
1. Trascina il componente richiesto nella [posizione richiesta](#component-placeholder) e rilascialo.
1. [Modifica](#edit-content) il componente appena inserito.

>[!NOTE]
>
>Su un dispositivo mobile, il browser componenti occuperà l’intero schermo. Dopo aver iniziato a trascinare un componente, il browser si chiude per mostrare nuovamente la pagina per permetterti di posizionarlo.

### Aggiunta di un componente dal sistema paragrafo {#adding-a-component-from-the-paragraph-system}

Puoi aggiungere un nuovo componente utilizzando il segnaposto **Trascina qui i componenti** del sistema paragrafo:

1. Verificare che l&#39;editor di pagine sia in modalità [**Modifica**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector).
1. Per selezionare e aggiungere un nuovo componente dal sistema paragrafo esistono due modi:

   * Seleziona l’opzione **Inserisci componente** (+) dalla barra degli strumenti di un componente esistente o dalla casella **Trascina qui i componenti**.

     ![Inserire un componente](assets/edit-content-drag-components-here.png)

   * Se utilizzi un dispositivo desktop, puoi fare doppio clic sulla casella **Trascina qui i componenti**.

1. Viene aperta la finestra di dialogo **Inserisci nuovo componente** che consente di selezionare il componente richiesto. Tocca o fai clic sul componente da aggiungere.

   * Utilizza i filtri di ricerca per trovare il componente.
   * Per ulteriori informazioni sul componente, utilizza l’icona delle informazioni accanto ai nomi dei componenti.

   ![Finestra di dialogo Inserisci nuovo componente](assets/edit-content-insert-component.png)

1. Il componente selezionato viene aggiunto alla destinazione selezionata. Se necessario, [Modifica](#edit-content) il componente.

## Aggiunta di una risorsa {#adding-asset}

Puoi anche aggiungere un nuovo componente alla pagina trascinando una risorsa dal browser [risorse](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser). Questo crea automaticamente un componente del tipo appropriato (e che contiene la risorsa).

Puoi configurare questo comportamento per l’installazione in uso. Per ulteriori informazioni, consultare il documento [Guida di riferimento ai componenti](/help/implementing/developing/components/reference.md#component-placeholders).

Per creare un componente trascinando uno dei tipi di risorsa indicati sopra:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)
1. Apri il [browser Risorse](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser).
1. Trascina la risorsa richiesta nella posizione desiderata. Il segnaposto [componente](#component-placeholder) mostra dove è posizionato il componente e viene visualizzata una destinazione in cui verrà inserito.
1. Rilascia la risorsa sul target. Nella posizione richiesta viene creato un componente appropriato per il tipo di risorsa, contenente la risorsa selezionata.
1. [Modificare](#edit-content) il componente, se necessario.

>[!NOTE]
>
>Su un dispositivo mobile, il browser Risorse occupa l’intero schermo. Quando inizi a trascinare una risorsa, il browser si chiuderà per mostrare nuovamente la pagina e permetterti di posizionarla.

Se sfogliando le risorse disponibili scopri che è necessario eseguire una rapida modifica a una risorsa, puoi avviare l’[editor risorse](/help/assets/manage-digital-assets.md) direttamente dal browser, facendo clic sull’icona di modifica accanto al nome della risorsa.

## Modifica diretta dei componenti {#edit-in-place}

Selezionando un componente si apre la barra degli strumenti del componente. Consente di accedere a varie azioni che possono essere eseguite sul componente.

![Barra degli strumenti del componente](assets/edit-content-component-toolbar.png)

Le azioni disponibili nella barra degli strumenti del componente sono appropriate per il componente selezionato. La visualizzazione dipende dal componente selezionato e potrebbe non essere descritta in questa sezione.

* **Modifica** ti consente di modificare il contenuto del componente, spesso direttamente. Il suo comportamento dipende dal componente.

  Pulsante ![Modifica](assets/edit-content-edit.png)

* **Configura** consente di modificare alcuni parametri del componente non direttamente correlati al suo contenuto, normalmente in una finestra di dialogo. Il suo comportamento dipende dal componente.

  ![Pulsante Configura](assets/edit-content-configure.png)

* **Copia** copia il componente negli Appunti per incollarlo altrove. Il componente originale rimane invariato.

  ![Pulsante Copia](assets/edit-content-copy.png)

* **Taglia** copia il componente negli Appunti. Il componente originale viene rimosso.

  ![Pulsante Taglia](assets/edit-content-cut.png)

* **Elimina** elimina il componente dalla pagina con la tua conferma.

  ![Pulsante Elimina](assets/edit-content-delete.png)

* **Inserisci componente** apre la finestra di dialogo per [aggiungere un nuovo componente](#adding-a-component-from-the-paragraph-system).

  ![Pulsante Inserisci](assets/edit-content-insert-component.png)

* **Incolla** incolla il componente dagli Appunti alla pagina. Se l&#39;originale rimane, dipende dal fatto che hai usato **Copia** o **Taglia**.

   * È possibile utilizzare Incolla per collocare i componenti sulla stessa pagina o su una pagina diversa.
   * Se si incolla in un’altra pagina che era già aperta prima dell’operazione Taglia/Copia, per visualizzare il contenuto incollato è necessario aggiornare la pagina.
   * L’elemento viene incollato sopra l’elemento in cui selezioni l’azione Incolla.
   * L’azione Incolla viene mostrata solo se è presente contenuto negli Appunti.

  ![Pulsante Incolla](assets/edit-content-paste.png)

* **Gruppo** consente di selezionare più componenti contemporaneamente. È possibile eseguire la stessa azione su un dispositivo desktop tramite **Ctrl+clic** o **Comando+clic**.

  ![Pulsante Gruppo](assets/edit-content-group.png)

* **Elemento padre** seleziona il componente padre del componente selezionato.

  ![Pulsante Elemento padre](assets/edit-content-parent.png)

* **Layout** consente di modificare il [layout](#editing-component-layout) del componente selezionato.

   * Ciò vale solo per il componente selezionato e non attiva la [Modalità di layout](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) per l’intera pagina.

  ![Pulsante Layout](assets/edit-content-layout.png)

* **Converti in variante di frammento di esperienza** consente di creare un [frammento di esperienza](/help/sites-cloud/authoring/fragments/content-fragments.md) dal componente selezionato o di aggiungerlo a un frammento di esperienza esistente.

  ![Pulsante Converti in frammento esperienza](assets/edit-content-convert.png)

### Finestra di dialogo di modifica del componente   {#component-edit-dialog}

Alcuni componenti offrono opzioni di modifica aggiuntive rispetto a quelle disponibili direttamente. È possibile aprire la finestra di dialogo per modifica di un componente utilizzando l&#39;icona [Modifica (matita) della barra degli strumenti del componente](#component-toolbar) per accedere ad altre opzioni di configurazione.

Le opzioni di modifica effettive dipendono dal componente. Per alcuni componenti [alcune azioni saranno disponibili solo in modalità a schermo intero](#edit-content-full-screen-mode). Esempio:

* Componente testo

  ![Barra degli strumenti del componente testo](assets/edit-content-text-component.png)

* Componente immagine

  ![Barra degli strumenti del componente immagine](assets/edit-content-image-component.png)

### Modifica componenti in modalità a tutto schermo {#edit-content-full-screen-mode}

Molti componenti offrono una modalità a schermo intero per la modifica accessibile con questo pulsante.

![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/editing-full-screen.png)

La modifica a schermo intero consente di visualizzare più opzioni di modifica rispetto all’editor locale, ad esempio per il componente Immagine.

![Componente immagine a schermo intero](assets/edit-content-image-component-full-screen.png)

Utilizza il pulsante **Riduci a icona** per attivare la modalità a schermo intero.

![Pulsante Riduci a icona](assets/edit-content-minimize.png)

## Spostamento dei componenti {#moving-components}

Per spostare un componente:

1. Seleziona il componente da spostare tenendo premuto o facendo clic.
1. Trascina il componente nella nuova posizione.

   * L&#39;editor pagina indica la posizione del componente con un [segnaposto](#component-placeholder) e dove è possibile eliminare il paragrafo con una destinazione.

   ![Spostamento di un componente](assets/edit-content-move-placeholder.png)

1. Rilascialo nella posizione desiderata.

>[!TIP]
>
>Per spostare un componente puoi anche utilizzare [Taglia e Incolla](#component-toolbar).

## Modifica del layout dei componenti {#editing-component-layout}

Invece di passare più volte dalla modalità di modifica alla [modalità di layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md) per regolare le impostazioni di un componente, è possibile selezionare l’azione **Layout**. Questo permette di modificare rapidamente il layout di quello specifico componente, senza uscire dalla modalità di modifica.

1. In modalità **Modifica** della console Sites, seleziona un componente per visualizzare la barra degli strumenti del componente.

1. Seleziona l&#39;azione **Layout** per modificare il layout del componente.

   ![Pulsante Layout della barra degli strumenti del componente](assets/edit-content-layout.png)

1. Una volta selezionata l&#39;azione Layout, è possibile modificare il layout del componente come si fa in [modalità layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md#defining-layouts-layout-mode).

   * Vengono visualizzate le maniglie di ridimensionamento del componente.
   * La barra degli strumenti dell’emulatore viene visualizzata nella parte superiore dello schermo.
   * La barra degli strumenti del componente presenta le azioni di layout al posto delle azioni di modifica standard.

   ![Un componente in modalità layout](assets/edit-content-layout-mode.png)

1. Dopo aver apportato le modifiche necessarie, tocca o fai clic sul pulsante **Chiudi** nel menu Azioni del componente per interrompere la modifica del layout del componente e la barra degli strumenti del componente torna al suo normale stato di modifica.

   ![Barra degli strumenti di un componente pagina](assets/edit-content-layout-close.png)

>[!TIP]
>
>L’azione Layout è limitata al componente selezionato. Ad esempio, se stai modificando il layout di un componente e fai clic su un altro componente, per il componente appena selezionato viene visualizzata la barra degli strumenti di modifica standard (non la barra degli strumenti di layout), mentre le maniglie di ridimensionamento e la barra degli strumenti dell’emulatore scompaiono.
>
>Se devi modificare il layout globale della pagina, che iinteresserà più componenti, passa alla [modalità di layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md).

## Modifica dell’ereditarietà dei componenti {#inherited-components}

L’ereditarietà è il meccanismo in cui il contenuto può essere collegato in modo che la modifica di un elemento cambia automaticamente l’altro. I componenti ereditati possono essere il risultato di vari scenari, tra cui:

* [Gestione multisito](/help/sites-cloud/administering/msm/overview.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)

Puoi annullare e riabilitare l’ereditarietà. A seconda del componente, queste opzioni sono disponibili dalla barra degli strumenti del componente, se il componente fa parte di una Live Copy o di un lancio.

* **Annulla ereditarietà**

  ![Pulsante Annulla ereditarietà](assets/edit-content-cancel-inheritance.png)

* **Riabilita ereditarietà** se l&#39;ereditarietà è già annullata

  ![Pulsante Riattiva ereditarietà](assets/edit-content-re-enable-inheritance.png)

* **Rollout** è disponibile anche nel blueprint o nell&#39;origine Live Copy

  ![Pulsante Rollout](assets/edit-content-rollout.png)
