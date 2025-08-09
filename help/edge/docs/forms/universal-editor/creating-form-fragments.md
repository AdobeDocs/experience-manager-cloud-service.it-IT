---
title: Come creare frammenti di modulo per l’authoring basato su WYSIWYG
description: Scopri come creare frammenti di modulo nell’editor universale e aggiungerli ai moduli.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 40%

---

# Creazione di frammenti di modulo nell’editor universale

<!--
<span class="preview"> This feature is available through the early access program. To request access, send an email with your GitHub organization name and repository name from your official address to <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . For example, if the repository URL is https://github.com/adobe/abc, the organization name is adobe and the repository name is abc.</span> 

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>
-->

I frammenti di modulo sono componenti riutilizzabili che eliminano il lavoro di sviluppo ripetitivo e garantiscono la coerenza tra i moduli dell’organizzazione. Invece di ricreare sezioni comuni come informazioni di contatto, dettagli sull’indirizzo o accordi di consenso per ogni modulo, puoi creare questi elementi una volta come frammenti e riutilizzarli in più moduli.

**Operazioni da eseguire in questo articolo:**

- Comprendere il valore aziendale e le funzionalità tecniche dei frammenti di modulo
- Creare frammenti di modulo riutilizzabili tramite Editor universale
- Integrare frammenti nei moduli esistenti con la configurazione corretta
- Gestire il ciclo di vita dei frammenti e mantenere la coerenza tra i moduli

**Vantaggi aziendali:**

- **Tempo di sviluppo ridotto**: creazione di sezioni di moduli comuni una sola volta e riutilizzo ovunque
- **Maggiore coerenza**: layout e contenuti standardizzati in tutti i moduli
- **Manutenzione semplificata**: aggiorna un frammento una volta per riflettere le modifiche in tutti i moduli che lo utilizzano
- **Conformità migliorata**: garantire che le sezioni normative rimangano coerenti e aggiornate

I frammenti di modulo in Edge Delivery Services supportano funzionalità avanzate, tra cui frammenti nidificati, più istanze all’interno di un singolo modulo e un’integrazione perfetta con le origini dati.

## Informazioni sui frammenti di modulo

I frammenti di modulo in Edge Delivery Services forniscono funzionalità avanzate per lo sviluppo di moduli modulari:

**Funzionalità di base:**

- **Gestione coerenza**: i frammenti mantengono layout e contenuti identici in più moduli. Con l’approccio &quot;cambia una volta, riflette ovunque&quot;, gli aggiornamenti a un frammento si applicano automaticamente a tutti i moduli in modalità Anteprima.
- **Utilizzo multiplo**: aggiungere lo stesso frammento più volte all&#39;interno di un singolo modulo, ciascuno con associazione dati indipendente a diverse origini dati o elementi dello schema.
- **Strutture annidate**: crea gerarchie complesse incorporando frammenti in altri frammenti per architetture di moduli sofisticate.

**Requisiti tecnici:**

- **Coerenza URL GitHub**: sia il frammento che qualsiasi modulo che lo utilizza devono specificare lo stesso URL archivio GitHub
- **Modifica autonoma**: è possibile modificare i frammenti solo nel relativo modulo autonomo; non è possibile apportare modifiche nel modulo host

**Comportamento pubblicazione:**

>[!IMPORTANT]
>
>In modalità Anteprima, le modifiche apportate ai frammenti vengono applicate immediatamente a tutti i moduli. In modalità Pubblica, per visualizzare gli aggiornamenti è necessario ripubblicare sia il frammento che tutti i moduli che lo utilizzano.

>[!CAUTION]
>
>Evita riferimenti ricorsivi ai frammenti (nidificando un frammento all’interno di se stesso), in quanto questo causa errori di rendering e comportamenti imprevisti.

## Prerequisiti

**Requisiti tecnici di installazione:**

- [Archivio GitHub configurato](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) con connessione stabilita tra l&#39;ambiente AEM e l&#39;archivio GitHub
- [Ultimo blocco Forms adattivo](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) aggiunto all&#39;archivio GitHub (per progetti Edge Delivery Services esistenti)
- È disponibile l’istanza Autore AEM Forms con modello Edge Delivery Services
- Accesso all’URL dell’istanza di authoring di AEM Forms as a Cloud Service e all’URL dell’archivio GitHub

**Conoscenze e autorizzazioni richieste:**

- Nozioni di base sui concetti di progettazione dei moduli e sulla gerarchia dei componenti
- Familiarità con l’interfaccia dell’Editor universale e i flussi di lavoro per la creazione di moduli
- Autorizzazioni a livello di autore in AEM Forms per la creazione e la gestione delle risorse dei moduli
- Informazioni sugli standard dei moduli aziendali e sui requisiti dei componenti riutilizzabili

## Utilizzo dei frammenti di modulo di Edge Delivery Services

Puoi creare frammenti di modulo di Edge Delivery Services nell’editor universale e aggiungere i frammenti creati a moduli di Edge Delivery Services. Con i frammenti di modulo di Edge Delivery Services puoi creare le azioni elencate di seguito:

- [Creazione di frammenti di modulo](#creating-form-fragments)
- [Aggiunta di frammenti di modulo a un modulo](#adding-form-fragments-to-a-form)
- [Gestione dei frammenti di modulo](#managing-form-fragments)

+++ Creazione di frammenti di modulo

Per creare un frammento di modulo nell’editor universale, effettua le seguenti operazioni:

1. Accedi all’istanza Autore AEM Forms as a Cloud Service.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Fai clic su **Crea > Frammento di modulo adattivo**.

   ![Crea frammento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Viene visualizzata la procedura guidata **Crea frammento di modulo adattivo**.
1. Seleziona il modello basato su Egde Delivery Services dalla scheda **Seleziona modello** e fai clic su **[!UICONTROL Avanti]**.
   ![Seleziona modello di Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Inserisci un titolo, un nome, una descrizione e i tag relativi al frammento. Assicurati di specificare un nome univoco per il frammento. Se esiste un altro frammento con lo stesso nome, il frammento non viene creato.
1. Specifica l’**URL di GitHub**. Ad esempio, se l&#39;archivio GitHub è denominato `edsforms`, si trova sotto l&#39;account `wkndforms`, l&#39;URL è `https://github.com/wkndforms/edsforms`.

   ![proprietà di base](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Facoltativo) Fai clic per aprire la scheda **Modello modulo** e dal menu a discesa **Seleziona da** seleziona uno dei seguenti modelli per il frammento:

   ![Mostra il tipo di modello nella scheda Modello modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **Modello dati modulo (FDM)**: integra nel frammento oggetti e servizi del modello dati provenienti dalle origini dati. Se il modulo richiede la lettura e la scrittura di dati da più origini, scegli Modello dati modulo (FDM).

   - **Schema JSON**: integra il modulo con un sistema back-end associando uno schema JSON che definisce la struttura dei dati. Consente di aggiungere contenuti dinamici utilizzando gli elementi dello schema.
   - **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

   >[!NOTE]
   >
   > Per informazioni su come integrare moduli o frammenti con un modello dati modulo (FDM) nell&#39;editor universale per utilizzare diverse origini dati back-end, vedere [Integrare moduli con il modello dati modulo nell&#39;editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Facoltativo) Specifica la **Data pubblicazione** o la **Data annullamento pubblicazione** per il frammento nella scheda **Avanzate**.

   ![Scheda Avanzate](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Fai clic su **Crea** per generare il frammento. Viene visualizzata una finestra di dialogo di successo con le opzioni di modifica.

   ![Modifica frammento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Fai clic su **Modifica** per aprire il frammento nell&#39;Editor universale con il modello predefinito applicato.

   ![Frammento nell&#39;editor universale per la creazione](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **Progetta il contenuto del frammento**: aggiungi i componenti del modulo (campi di testo, elenchi a discesa, caselle di controllo) per creare la sezione riutilizzabile. Per istruzioni dettagliate sui componenti, consulta [Guida introduttiva di Edge Delivery Services per AEM Forms con Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

1. **Configurare le proprietà del componente**: impostare i nomi dei campi, le regole di convalida e i valori predefiniti in base alle esigenze del caso d&#39;uso.

1. **Salva e visualizza l&#39;anteprima**: salva il frammento e utilizza la modalità Anteprima per verificare il layout e le funzionalità.

   ![Schermata di un frammento di modulo dei dettagli di contatto completato nell’editor universale, con campi per nome, telefono, e-mail e indirizzo che possono essere riutilizzati in più moduli](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**Checkpoint di convalida:**

- Nell’editor universale i frammenti vengono caricati senza errori
- Tutti i componenti del modulo vengono riprodotti correttamente
- Le proprietà dei campi e le regole di convalida funzionano come previsto
- Il frammento è salvato e disponibile nella console Forms e documenti

Una volta completato il frammento, puoi [integrarlo in qualsiasi Edge Delivery Services Form](#adding-form-fragments-to-a-form).

+++


+++ Aggiunta di frammenti di modulo a un modulo

In questo esempio viene illustrata la creazione di un modulo `Employee Details` che utilizza il frammento `Contact Details` per le sezioni delle informazioni relative ai dipendenti e ai supervisori. Questo approccio garantisce una raccolta coerente dei dati, riducendo al contempo lo sforzo di sviluppo.

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

   Il frammento di modulo viene aggiunto facendo riferimento al modulo e rimane sincronizzato con il frammento di modulo autonomo.

   ![Schermata che mostra il frammento dei dettagli di contatto integrato correttamente in un modulo dipendente all’interno dell’editor universale, in cui viene illustrato come i frammenti mantengono la propria struttura quando vengono riutilizzati](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   È possibile visualizzare in anteprima il modulo per visualizzarne l’aspetto nella modalità **Anteprima**.

   ![Anteprima](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Analogamente, è possibile ripetere i passaggi da 3 a 7 per inserire il frammento `Contact Details` nel pannello `Supervisor Details`.

   ![Modulo dettagli dipendenti](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ Gestione dei frammenti di modulo

Puoi eseguire diverse operazioni sui frammenti di modulo utilizzando l’interfaccia utente di AEM Forms.

1. Accedi all’istanza Autore AEM Forms as a Cloud Service.
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

**Progettazione e denominazione frammento:**

- **Usa nomi descrittivi e univoci**: scegli nomi che indichino chiaramente lo scopo del frammento (ad esempio, &quot;contact-details-with-validation&quot; anziché &quot;fragment1&quot;)
- **Pianificazione della riutilizzabilità**: i frammenti di progettazione devono essere indipendenti dal contesto, in modo che funzionino in diversi tipi di moduli
- **Mantieni concentrati i frammenti**: crea frammenti monouso anziché componenti multifunzionali complessi

**Flusso di lavoro di sviluppo:**

- **Test indipendente dei frammenti**: verifica la funzionalità del frammento prima dell&#39;integrazione nei moduli
- **Mantieni URL GitHub coerenti**: assicurati che venga utilizzato lo stesso URL dell&#39;archivio in tutti i frammenti e moduli correlati
- **Scopo del frammento di documento**: includere descrizioni e tag chiari per aiutare i membri del team a capire quando utilizzare ogni frammento

**Pubblicazione e manutenzione:**

- **Coordinare la pubblicazione**: durante l&#39;aggiornamento dei frammenti, pianifica la ripubblicazione simultanea di tutti i moduli dipendenti
- **Controllo versione**: utilizza messaggi di commit significativi quando aggiorni i frammenti per tenere traccia delle modifiche nel tempo
- **Monitorare le dipendenze**: tenere traccia dei moduli che utilizzano ogni frammento per valutare l&#39;impatto degli aggiornamenti

>[!TIP]
>
>Gli stili, gli script e le espressioni dei frammenti vengono mantenuti quando incorporati, quindi progetta tenendo presente questa ereditarietà.

## Riepilogo

Hai imparato a sfruttare i frammenti di modulo in Edge Delivery Services per migliorare l’efficienza dello sviluppo e mantenere la coerenza tra i moduli della tua organizzazione.

**Risultati chiave:**

- **Informazioni**: riconosciuto il valore aziendale e le funzionalità tecniche dei frammenti di modulo
- **Creazione**: frammenti di modulo riutilizzabili creati con Universal Editor con configurazione corretta
- **Integrazione**: frammenti aggiunti ai moduli con la configurazione corretta della proprietà e dell&#39;installazione dei riferimenti
- **Gestione**: operazioni del ciclo di vita e flussi di lavoro di manutenzione dei frammenti esplorati

**Passaggi successivi:**

- Crea una libreria di frammenti di uso comune per la tua organizzazione
- Stabilire convenzioni di denominazione e criteri di governance per l’utilizzo dei frammenti
- Esplora l&#39;integrazione avanzata con [Modelli dati modulo](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) per frammenti dinamici basati su dati
- Implementare modelli di modulo basati su frammenti per esperienze utente coerenti

I moduli ora usufruiscono di un’architettura modulare e gestibile in grado di scalare in modo efficiente tra i progetti, garantendo al contempo esperienze utente coerenti.


