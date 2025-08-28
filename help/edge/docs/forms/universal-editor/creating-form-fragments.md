---
title: Come creare frammenti di modulo per l’authoring basato su WYSIWYG
description: Scopri come creare frammenti di modulo nell’editor universale e aggiungerli ai moduli.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: ht
source-wordcount: '1670'
ht-degree: 100%

---

# Creazione di frammenti di modulo nell’editor universale

I frammenti di modulo sono componenti riutilizzabili che eliminano il lavoro di sviluppo ripetitivo e garantiscono la coerenza tra i moduli dell’organizzazione. Invece di ricreare sezioni comuni come informazioni di contatto, dettagli sull’indirizzo o accordi di consenso per ogni modulo, puoi creare questi elementi una volta come frammenti e riutilizzarli in più moduli.

**Che cosa scoprirai in questo articolo:**

- Informazioni sul valore aziendale e le funzionalità tecniche dei frammenti di modulo
- Creare frammenti di modulo riutilizzabili tramite l’editor universale
- Integrare frammenti nei moduli esistenti con la configurazione corretta
- Gestire il ciclo di vita dei frammenti e mantenere la coerenza tra i moduli

**Vantaggi aziendali:**

- **Tempo di sviluppo ridotto**: creazione di sezioni di modulo comuni una sola volta e riutilizzo ovunque
- **Coerenza migliorata**: layout e contenuto standardizzati in tutti i moduli
- **Manutenzione semplificata**: aggiornare un frammento una volta per riflettere le modifiche in tutti i moduli che lo utilizzano
- **Conformità avanzata**: garantire che le sezioni normative rimangano coerenti e aggiornate

I frammenti di modulo in Edge Delivery Services supportano funzionalità avanzate, che includono frammenti nidificati, più istanze all’interno di un singolo modulo e un’integrazione perfetta con le origini dati.

## Informazioni sui frammenti di modulo

I frammenti di modulo in Edge Delivery Services forniscono funzionalità avanzate per lo sviluppo del modulo modulare:

**Funzionalità di base:**

- **Gestione coerenza**: i frammenti mantengono layout e contenuto identici in più moduli. Con l’approccio “modifica una volta, rifletti ovunque”, gli aggiornamenti a un frammento si applicano automaticamente a tutti i moduli in modalità Anteprima.
- **Utilizzo multiplo**: aggiungere lo stesso frammento più volte all’interno di un singolo modulo, ciascuno con associazione dati indipendente a diverse origini dati o elementi dello schema.
- **Strutture nidificate**: creare gerarchie complesse incorporando frammenti in altri frammenti per architetture di modulo sofisticate.

**Requisiti tecnici:**

- **Coerenza URL di GitHub**: sia il frammento che qualsiasi modulo che lo utilizza devono specificare lo stesso URL di archivio GitHub
- **Modifica autonoma**: è possibile modificare i frammenti solo nel relativo modulo autonomo; non è possibile apportare modifiche nel modulo host

**Comportamento pubblicazione:**

>[!IMPORTANT]
>
>In modalità Anteprima, le modifiche apportate al frammento vengono applicate immediatamente a tutti i moduli. In modalità Pubblicazione, per visualizzare gli aggiornamenti è necessario ripubblicare sia il frammento che tutti i moduli che lo utilizzano.

>[!CAUTION]
>
>Evita riferimenti ricorsivi ai frammenti (nidificando un frammento all’interno di se stesso), in quanto questo causa errori di rendering e comportamenti imprevisti.

## Prerequisiti

**Requisiti tecnici di configurazione:**

- [Archivio GitHub configurato](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) con connessione stabilita tra l’ambiente AEM e l’archivio GitHub
- [Blocco di moduli adattivi più recente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) aggiunto all’archivio GitHub (per progetti Edge Delivery Services esistenti)
- È disponibile l’istanza di authoring di AEM Forms con modello di Edge Delivery Services
- Accesso all’URL dell’istanza di authoring di AEM Forms as a Cloud Service e all’URL dell’archivio GitHub

**Conoscenze e autorizzazioni richieste:**

- Informazioni di base sui concetti di progettazione del modulo e sulla gerarchia del componente
- Familiarità con l’interfaccia dell’editor universale e i flussi di lavoro per la creazione del modulo
- Autorizzazioni a livello di authoring in AEM Forms per creare e gestire le risorse del modulo
- Informazioni sugli standard del modulo aziendali e sui requisiti del componente riutilizzabile

## Utilizzo dei frammenti di modulo di Edge Delivery Services

Puoi creare frammenti di modulo di Edge Delivery Services nell’editor universale e aggiungere i frammenti creati a moduli di Edge Delivery Services. Con i frammenti di modulo di Edge Delivery Services puoi creare le azioni elencate di seguito:

- [Creazione di frammenti di modulo](#creating-form-fragments)
- [Aggiunta di frammenti di modulo a un modulo](#adding-form-fragments-to-a-form)
- [Gestione dei frammenti di modulo](#managing-form-fragments)

+++ Creazione di frammenti di modulo

Per creare un frammento di modulo nell’editor universale, effettua le seguenti operazioni:

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Fai clic su **Crea > Frammento di modulo adattivo**.

   ![Crea frammento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Viene visualizzata la procedura guidata **Crea frammento di modulo adattivo**.
1. Seleziona il modello basato su Egde Delivery Services dalla scheda **Seleziona modello** e fai clic su **[!UICONTROL Avanti]**.
   ![Seleziona modello di Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Inserisci un titolo, un nome, una descrizione e i tag relativi al frammento. Assicurati di specificare un nome univoco per il frammento. Se esiste un altro frammento con lo stesso nome, il frammento non viene creato.
1. Specifica l’**URL di GitHub**. Se, ad esempio, l’archivio GitHub è denominato `edsforms` ed è posizionato nell’account `wkndforms`, l’URL è `https://github.com/wkndforms/edsforms`.

   ![proprietà di base](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Facoltativo) Fai clic per aprire la scheda **Modello modulo** e dal menu a discesa **Seleziona da** seleziona uno dei seguenti modelli per il frammento:

   ![Mostra il tipo di modello nella scheda Modello modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **Modello dati modulo (FDM)**: integra nel frammento oggetti e servizi del modello dati provenienti dalle origini dati. Se il modulo richiede la lettura e la scrittura di dati da più origini, scegli Modello dati modulo (FDM).

   - **Schema JSON**: integra il modulo con un sistema back-end associando uno schema JSON che definisce la struttura dei dati. Consente di aggiungere contenuti dinamici utilizzando gli elementi dello schema.
   - **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

   >[!NOTE]
   >
   > Per informazioni su come integrare moduli o frammenti con un FDM (modello dati modulo) nell’editor universale per utilizzare diverse origini dati di back-end, consulta [Integrare moduli con FDM nell’editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Facoltativo) Specifica la **Data pubblicazione** o la **Data annullamento pubblicazione** per il frammento nella scheda **Avanzate**.

   ![Scheda Avanzate](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Fai clic su **Crea** per generare il frammento. Viene visualizzata una finestra di dialogo corretta con opzioni di modifica.

   ![Modifica frammento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Fai clic su **Modifica** per aprire il frammento nell’editor universale con il modello predefinito applicato.

   ![Frammento nell’editor universale per l’authoring](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **Progetta il contenuto del frammento**: aggiungi i componenti del modulo (campi di testo, elenchi a discesa, caselle di controllo) per creare la sezione riutilizzabile. Per indicazioni dettagliate sul componente, consulta [Guida introduttiva di Edge Delivery Services per AEM Forms con editor universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

1. **Configura le proprietà del componente**: imposta i nomi dei campi, le regole di convalida e i valori predefiniti in base alle esigenze del caso d’uso.

1. **Salva e visualizza l’anteprima**: salva il frammento e utilizza la modalità Anteprima per verificare il layout e la funzionalità.

   ![Schermata di un frammento di modulo dei dettagli di contatto completato nell’editor universale, con campi per nome, telefono, e-mail e indirizzo che possono essere riutilizzati in più moduli](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**Punti di controllo della convalida:**

- Nell’editor universale il frammento viene caricato senza errori
- Su tutti i componenti del modulo viene eseguito il rendering correttamente
- Le proprietà dei campi e le regole di convalida funzionano come previsto
- Il frammento è salvato e disponibile nella console Moduli e documenti

Una volta completato il frammento, puoi [integrarlo in qualsiasi modulo di Edge Delivery Services](#adding-form-fragments-to-a-form).

+++


+++ Aggiunta di frammenti di modulo a un modulo

In questo esempio viene illustrata la creazione di un modulo `Employee Details` che utilizza il frammento `Contact Details` per le sezioni delle informazioni relative ai dipendenti e ai supervisori. Questo approccio garantisce una raccolta dati coerente, riducendo al contempo lo sforzo di sviluppo.

Per integrare un frammento di modulo nel modulo:

1. Apri il passaggio in modalità di modifica.
1. Aggiungi il componente Frammento modulo al modulo.
1. Apri il Browser dei contenuti e accedi al componente **[!UICONTROL Modulo adattivo]** nella **Struttura contenuto**.
1. Passa alla sezione in cui desideri aggiungere un frammento. Ad esempio, passa al pannello **Dettagli dipendente**.

   ![Accedi alla sezione](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi il componente **[!UICONTROL Frammento modulo]** dall’elenco **Componenti modulo adattivo**.
   ![Aggiungi frammento modulo](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Quando selezioni il componente **[!UICONTROL Frammento modulo]**, il frammento viene aggiunto al modulo. Puoi configurare le proprietà del frammento aggiunto aprendo le relative **proprietà**. Ad esempio, nascondere il titolo del frammento dalle relative **Proprietà**.

   ![Configurazione delle proprietà del frammento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Seleziona il **Riferimento frammento** nella scheda **Base**. Vengono visualizzati tutti i frammenti disponibili per il modulo, a seconda del modello del modulo.

   Ad esempio, passa a `/content/forms/af` e seleziona il frammento `Contact Details`.

   ![Seleziona frammento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Fai clic su **[!UICONTROL Seleziona]**.

   Il frammento di modulo viene aggiunto in riferimento al modulo e rimane sincronizzato con il frammento di modulo indipendente.

   ![Schermata che mostra il frammento dei dettagli di contatto integrato correttamente in un modulo dipendente all’interno dell’editor universale, in cui viene illustrato come i frammenti mantengono la propria struttura quando vengono riutilizzati](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   È possibile visualizzare in anteprima il modulo per visualizzarne l’aspetto nella modalità **Anteprima**.

   ![Anteprima](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Analogamente, è possibile ripetere i passaggi da 3 a 7 per inserire il frammento `Contact Details` nel pannello `Supervisor Details`.

   ![Modulo dettagli dipendente](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ Gestione dei frammenti di modulo

Puoi eseguire diverse operazioni sui frammenti di modulo utilizzando l’interfaccia utente di AEM Forms.

1. Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

1. Selezionando un frammento di modulo, nella barra degli strumenti vengono visualizzate le seguenti operazioni che è possibile eseguire sul frammento selezionato.

   ![Gestione frammento](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
    </tr>
    <tr>
   <td><p>Modifica</p> </td>
   <td><p>Apre il frammento di modulo in modalità di modifica.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Proprietà</p> </td>
   <td><p>Fornisce opzioni per modificare le proprietà del frammento di modulo.<br /> <br /> </p> </td>
    </tr>
    <td><p>Copia</p> </td>
   <td><p> Fornisce opzioni per copiare il frammento di modulo e incollarlo nella posizione desiderata. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il frammento come HTML o per eseguire un’anteprima personalizzata unendo i dati di un file XML con il frammento. <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Avvia/Gestisci revisione</p> </td>
   <td><p>Consente di avviare e gestire una revisione del frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>Pubblica/Annulla pubblicazione</p> </td>
   <td><p>Pubblica o annulla la pubblicazione del frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Elimina</p> </td>
   <td><p>Elimina il frammento selezionato.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Confronta</p> </td>
   <td><p>Confronta due diversi frammenti di modulo a scopo di anteprima.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

+++

## Best practice

**Progettazione e denominazione del frammento:**

- **Utilizza nomi descrittivi e univoci**: scegli nomi che indichino chiaramente lo scopo del frammento (ad esempio, “contact-details-with-validation” anziché “fragment1”)
- **Pianificazione per la riutilizzabilità**: i frammenti di progettazione devono essere indipendenti dal contesto, in modo che funzionino in diversi tipi di moduli
- **Mantieni frammenti mirati**: crea frammenti a scopo singolo anziché componenti multifunzionali complessi

**Flusso di lavoro di sviluppo:**

- **Testa i frammenti in modo indipendente**: verifica la funzionalità del frammento prima dell’integrazione nei moduli
- **Mantieni URL GitHub coerenti**: assicurati che venga utilizzato lo stesso URL dell’archivio in tutti i frammenti e moduli correlati
- **Scopo del frammento di documento**: includi descrizioni e tag chiari per aiutare i membri del gruppo a capire quando utilizzare ogni frammento

**Pubblicazione e manutenzione:**

- **Coordina la pubblicazione**: durante l’aggiornamento dei frammenti, pianifica la ripubblicazione simultanea di tutti i moduli dipendenti
- **Controllo versione**: utilizza messaggi di commit significativi quando aggiorni i frammenti per tenere traccia delle modifiche nel tempo
- **Monitora le dipendenze**: tieni traccia dei moduli che utilizzano ogni frammento per valutare l’impatto dell’aggiornamento

>[!TIP]
>
>Gli stili, gli script e le espressioni dei frammenti vengono mantenuti quando incorporati, quindi progetta tenendo presente questa ereditarietà.

## Riepilogo

Hai imparato a sfruttare correttamente i frammenti di modulo in Edge Delivery Services per migliorare l’efficienza dello sviluppo e mantenere la coerenza tra i moduli della tua organizzazione.

**Raggiungimenti principali:**

- **Informazioni**: compreso il valore aziendale e le funzionalità tecniche dei frammenti di modulo
- **Creazione**: creati frammenti di modulo riutilizzabili con l’editor universale con configurazione corretta
- **Integrazione**: aggiunti frammenti ai moduli con configurazione della proprietà e di riferimento corretti
- **Gestione**: esplorate le operazioni del ciclo di vita e dei flussi di lavoro di manutenzione del frammento

**Passaggi successivi:**

- Crea una libreria di frammenti di utilizzo comune per la tua organizzazione
- Stabilisci convenzioni di denominazione e criteri di governance per l’utilizzo del frammento
- Esplora l’integrazione avanzata con [modelli di dati del modulo](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) per frammenti dinamici basati su dati
- Implementa modelli di modulo basati su frammenti per esperienze utente coerenti

I moduli ora beneficiano di un’architettura modulare e gestibile in grado di scalare in modo efficiente tra i progetti, garantendo al contempo esperienze utente coerenti.


