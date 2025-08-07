---
title: Creare e pubblicare Forms adattivo con Edge Delivery Services
description: Istruzioni dettagliate per la creazione, l’authoring e la pubblicazione di Forms adattivi utilizzando i modelli per Componenti core o Edge Delivery Services in AEM, con particolare attenzione all’accuratezza e alla chiarezza tecnica.
keywords: moduli adattivi, servizi di consegna edge, componenti core, editor universale, creazione di moduli, AEM forms, selezione di modelli, pubblicazione di moduli
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 3%

---


# Creare e pubblicare Forms adattivo con Edge Delivery Services

Questo documento fornisce istruzioni per la creazione, la configurazione e la pubblicazione di Adaptive Forms in AEM tramite Edge Delivery Services. Include i modelli dei Componenti core e Edge Delivery Services.

Al termine di questa guida, imparerai a:

- Seleziona il tipo di modello appropriato per il caso d’uso
- Creare moduli utilizzando i Componenti core o i modelli Edge Delivery Services
- Creare moduli con l’editor corretto
- Configurare e pubblicare moduli in Edge Delivery Services
- Accedere ai moduli pubblicati e verificare la distribuzione

## Selezione modello

Prima di iniziare, determinare quale tipo di modello è allineato ai requisiti:

| Criteri | Modello componenti core | Modello Edge Delivery Services |
|-------------------------|-----------------------------------------|-------------------------------------|
| Ideale per | Flussi di lavoro aziendali, integrazioni complesse | Moduli pubblici ad alte prestazioni |
| Editor | Editor di moduli adattivi | Editor universale |
| Pubblicazione | Pubblicazione AEM + Edge Delivery Services | Solo Edge Delivery Services |
| Complessità | Funzionalità avanzate dei moduli | Moduli veloci e semplificati |
| Integrazione | Ecosistema AEM completo | Sviluppo basato su Git |
| Curva di apprendimento | Familiare con gli utenti di AEM | Moderno approccio semplificato |

**Guida alla decisione:**

- Utilizza **Componenti core** per flussi di lavoro complessi, integrazione deep AEM o se utilizzi risorse AEM esistenti.
- Utilizza **Edge Delivery Services** per prestazioni, semplicità e pratiche di sviluppo moderne.

![Decisione selezione modello](/help/edge/docs/forms/universal-editor/assets/template-selection-decision.svg)
*Diagramma di flusso delle decisioni per la scelta del tipo di modello appropriato*

## Prerequisiti

Prima di procedere, assicurati che siano soddisfatti i seguenti prerequisiti:

### Requisiti tecnici

- **AEM Forms as a Cloud Service**: istanza di authoring attiva con una licenza Forms.
- **Account GitHub**: account personale o organizzativo per la gestione dell&#39;archivio.
- **Configurazione archivio**: scegliere una delle opzioni seguenti:
   - **Nuovo progetto**: [Crea un nuovo progetto AEM con blocco Forms adattivo](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). L’archivio è preconfigurato per Edge Delivery Services.
   - **Progetto esistente**: [Aggiungi blocco Forms adattivo a un repository esistente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) e aggiorna la configurazione.

### Configurazione dell’ambiente

- **Connessione AEM-GitHub**: [Stabilire una connessione](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) tra l&#39;istanza AEM e l&#39;archivio GitHub.
- **Edge Delivery Services**: verificare che l&#39;archivio sia configurato per la distribuzione automatica.
- **Autorizzazioni**: verificare di disporre dei diritti di accesso necessari per la creazione e la pubblicazione dei moduli.

### Convalida configurazione


1. Conferma che l’archivio GitHub contenga il blocco Forms adattivo.
2. Verifica la connessione tra AEM e l’archivio GitHub.
3. Assicurati di poter pubblicare i contenuti in Edge Delivery Services.



## Flusso di lavoro di creazione e pubblicazione di moduli

Il processo si articola in tre fasi principali:

- **Fase 1:** [Selezione modello e creazione modulo](#step-1-template-selection-and-form-creation)
- **Fase 2:** [Authoring e progettazione dei moduli](#step-2-form-authoring-and-design)
- **Fase 3:** [Configurazione e pubblicazione](#step-3-configuration-and-publishing)

Ogni fase include passaggi di convalida per confermare la corretta configurazione.

![Flusso di lavoro in tre fasi](/help/edge/docs/forms/universal-editor/assets/three-phase-workflow.svg)
*Panoramica delle tre fasi principali di creazione e pubblicazione dei moduli*

### Passaggio 1: selezione dei modelli e creazione dei moduli

Seleziona il flusso di lavoro in base alla scelta del modello:

>[!BEGINTABS]

>[!TAB Modello Edge Delivery Services]

**Caso d&#39;uso:** moduli ad alte prestazioni e flussi di lavoro di sviluppo moderni.

**Funzionalità:** authoring di Universal Editor e pubblicazione di Edge Delivery Services.

#### Procedura

1. **Creazione modulo di accesso**
   - Accedi all’istanza Autore AEM Forms as a Cloud Service.
   - Passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
   - Fai clic su **Crea** > **Forms adattivo**.

1. **Seleziona modello**
   - Nella scheda **Source**, seleziona un **modello basato su Edge Delivery Services**.
   - Il pulsante **Crea** viene attivato.

     ![Creare moduli EDS](/help/edge/assets/create-eds-forms.png)

1. **Configura opzioni (facoltativo)**
   - **Scheda Data Source**: se necessario, seleziona l&#39;integrazione dei dati.
   - **Scheda Invio**: scegli un&#39;azione di invio (configurabile in seguito).
   - **Scheda Consegna**: imposta la pianificazione della pubblicazione/annullamento della pubblicazione.

1. **Completare la configurazione del modulo**
   - Fai clic su **Crea** per aprire la procedura guidata per la creazione di moduli.
   - Immetti quanto segue:
      - **Nome**: identificatore interno (senza spazi, usare i trattini).
      - **Titolo**: nome visualizzato per il modulo.
      - **URL GitHub**: URL archivio (ad esempio, `https://github.com/your-org/your-repo`).

   ![Procedura guidata per la creazione di un modulo](/help/edge/assets/create-form-wizard.png)

1. **Convalida**
   - Dopo aver fatto clic su **Crea**, verifica:
      - Il modulo viene aperto in Universal Editor.
      - L’URL GitHub è collegato correttamente.
      - È disponibile la palette dei componenti.
      - L’area di lavoro del modulo è visibile.

   ![Interfaccia editor universale](/help/edge/assets/author-form.png)

**Risultato:** il modulo è pronto per l&#39;authoring nell&#39;editor universale.

>[!TAB Modello Componente Core]

**Caso d&#39;uso:** flussi di lavoro aziendali e integrazioni complesse.

**Funzionalità:** authoring Forms Editor adattivo, doppia pubblicazione (AEM + Edge Delivery Services), funzionalità avanzate per moduli.

#### Procedura

1. **Creazione modulo di accesso**
   - Accedi all’istanza Autore AEM Forms as a Cloud Service.
   - Passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
   - Fai clic su **Crea** > **Forms adattivo**.

1. **Seleziona modello e tema**
   - Nella scheda **Source**, seleziona un **modello basato su Componente core**.
   - Scegli un **tema** per lo stile.
   - Il pulsante **Crea** viene attivato.

   ![Selezione modello componente core](/help/forms/assets/core-component-based-template.png)

1. **Configura opzioni (facoltativo)**
   - **Scheda Data Source**: se necessario, seleziona l&#39;integrazione dei dati.
   - **Scheda Invio**: scegli un&#39;azione di invio (configurabile in seguito).
   - **Scheda Consegna**: imposta la pianificazione della pubblicazione/annullamento della pubblicazione.

1. **Completare la configurazione del modulo**
   - Fai clic su **Crea** per aprire la procedura guidata per la creazione di moduli.
   - Immetti quanto segue:
      - **Nome**: identificatore interno (senza spazi, usare i trattini).
      - **Titolo**: nome visualizzato per il modulo.
      - **Percorso**: percorso di archiviazione nell&#39;archivio AEM.

     ![Procedura guidata per la creazione di un modulo](/help/forms/assets/create-cc-form.png)

1. **Convalida**
   - Dopo aver fatto clic su **Crea**, verifica:
      - Il modulo viene aperto in Adaptive Forms Editor.
      - È disponibile la barra degli strumenti del componente.
      - Il pannello delle proprietà è accessibile.
      - Viene applicato lo stile del tema.

     ![Editor di moduli adattivi](/help/forms/assets/af-editor-form.png)

**Risultato:** il modulo è pronto per l&#39;authoring nell&#39;editor di Forms adattivo.

>[!ENDTABS]

### Passaggio 2: authoring e progettazione dei moduli

L’esperienza di authoring varia a seconda del modello:

- **Modello Edge Delivery Services**: Editor universale
- **Modello Componente Core**: Editor Forms Adattivo

![Confronto editor](/help/edge/docs/forms/universal-editor/assets/editor-comparison.svg)
*Confronto tra le funzionalità di Universal Editor e Adaptive Forms Editor*

>[!BEGINTABS]

>[!TAB Editor universale (Edge Delivery Services)]

**Interfaccia:** Modifica moderna e semplificata ottimizzata per le prestazioni.

#### Aggiungi componenti modulo

1. **Accedi alla libreria dei componenti**
   - Apri il browser Contenuto nell’editor universale.
   - Passa al componente **Modulo adattivo** nella struttura del contenuto.

   ![Navigazione struttura contenuto](/help/edge/assets/content-tree.png)

1. **Aggiungi campi modulo**
   - Fai clic sull&#39;icona **Aggiungi** per aprire la libreria dei componenti.
   - Selezionare i componenti dall&#39;elenco **Componenti modulo adattivo**.
   - Trascina i componenti nell’area di lavoro del modulo.

   ![Aggiungi componenti](/help/edge/assets/add-component.png)

1. **Progettare il modulo**
   - Configura le proprietà del campo nel pannello delle proprietà.
   - Impostare regole e comportamenti di convalida.
*s Regolare lo stile e il layout in base alle esigenze.

   ![Modulo di registrazione completato](/help/edge/assets/contact-us.png)

#### Convalida

- Tutti i campi obbligatori sono presenti.
- Le proprietà del campo sono configurate correttamente.
- Il layout è dinamico e accessibile.
- Le regole di convalida funzionano come previsto.

#### Passaggi successivi

- [Configurare le azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per la gestione dei dati.
- [Guida dell&#39;editor universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) per le funzionalità avanzate.

>[!TAB Editor Forms Adattivo (Componenti Core)]

**Interfaccia:** modifica completa con funzionalità avanzate per moduli.

#### Aggiungi componenti modulo

1. **Accedi alla libreria dei componenti**
   - Fai clic su **Inserisci componente** nella sezione **Trascina qui i componenti**.

   ![Area di inserimento componenti](/help/forms/assets/drag-components-af-editor.png)

2. **Aggiungi campi modulo**
   - Sfoglia l&#39;elenco **Componenti modulo adattivo**.
   - Trascina i componenti desiderati nel modulo.
   - Utilizza componenti avanzati come pannelli, procedure guidate e integrazioni di dati.

   ![Aggiungi libreria componenti](/help/forms/assets/add-component-af.png)

3. **Progettare il modulo**
   - Configura le proprietà del campo nel pannello delle proprietà.
   - Impostare regole di convalida e regole di business complesse.
   - Applicare temi e stili avanzati.

   ![Modulo di iscrizione completato](/help/forms/assets/af-editor-form.png)

#### Convalida

- Tutti i campi obbligatori sono presenti.
- Vengono configurate regole di convalida complesse.
- Viene applicato lo stile del tema.
- L’integrazione dei dati funziona come previsto (se applicabile).

#### Passaggi successivi

- [Configurare le azioni di invio](/help/forms/configure-submit-actions-core-components.md) per i flussi di lavoro avanzati.
- [Guida ai componenti core](/help/forms/creating-adaptive-form-core-components.md) per le funzionalità enterprise.

>[!ENDTABS]

### Passaggio 3: configurazione e pubblicazione

Configura Edge Delivery Services e pubblica il modulo. Il processo varia in base al tipo di modello.

#### Configurazione Edge Delivery Services

>[!BEGINTABS]
>[!TAB Modello Edge Delivery Services (automatico)]

**Configurazione:** automatica (non è richiesta alcuna configurazione manuale).

- La connessione all’archivio GitHub e la configurazione di Edge Delivery Services vengono create durante la creazione del modulo.
- Gli endpoint di pubblicazione vengono configurati automaticamente.

**Verifica:**

- Conferma che la configurazione venga visualizzata nelle impostazioni del modulo.
- Verifica che l’URL GitHub sia collegato correttamente.

![Configurazione automatica EDS](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Modello Componente Core (Manuale)]

**Configurazione:** è richiesta l&#39;installazione manuale.

#### Passaggi di configurazione manuali

1. **Accedi agli strumenti di configurazione**
   - Passa a **Strumenti** > **Servizi cloud** > **Configurazione Edge Delivery Services**.

   ![Accesso alla configurazione EDS](/help/edge/assets/select-eds-conf.png)

1. **Crea configurazione**
   - Selezionare la cartella corrispondente al nome del modulo (ad esempio, `forms/enrollment-form`).
   - Fai clic su **Crea** > **Configurazione**.

   ![Crea configurazione EDS](/help/forms/assets/create-eds-conf.png)

1. **Configura proprietà**
   - Fare clic su **Configurazione Edge Delivery Services**.
   - Seleziona **Proprietà** per aprire la finestra di dialogo di configurazione.

   ![Proprietà configurazione](/help/forms/assets/eds-conf.png)

1. **Imposta parametri**
   - **Richiesto:**
      - **Organizzazione**: nome organizzazione GitHub.
      - **Nome sito**: nome archivio GitHub.
      - **Ramo**: nome ramo (lasciare vuoto per principale).
   - **Facoltativo:**
      - **Host Edge**: predefinito (viene pubblicato sia in .page che in .live).
      - **Token di autenticazione sito**: per l&#39;autenticazione sicura (se richiesta).

1. **Salva configurazione**
   - Fare clic su **Salva e chiudi**.

#### Convalida

- Configurazione creata correttamente.
- L’organizzazione e l’archivio GitHub sono specificati correttamente.
- Le impostazioni del ramo corrispondono alla struttura dell’archivio.
- Il modulo viene visualizzato nella cartella di configurazione.

>[!ENDTABS]

#### Pubblicazione del modulo

>[!BEGINTABS]
>[!TAB Pubblicazione Editor Universale]

**Per Modelli Edge Delivery Services**

1. In Universal Editor, fare clic sul pulsante **Pubblica** (angolo superiore destro).
2. Conferma la pubblicazione nella finestra di dialogo.
3. Prendi nota degli URL generati per le versioni in staging e live.

   ![Pubblicazione editor universale](/help/edge/assets/publish-form.png)

- [Guida alla pubblicazione](/help/edge/docs/forms/universal-editor/publish-forms.md)

>[!TAB Pubblicazione editor adattivo di Forms]

1. Nella console Experience Manager Forms, seleziona il modulo da pubblicare.
2. Fai clic su **[!UICONTROL Pubblica]** nella barra degli strumenti. Esamina le risorse di riferimento da pubblicare.

![Pubblicare il modulo nell’editor di moduli adattivi](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Per informazioni dettagliate, vedere [Gestisci pubblicazione in Experience Manager Forms](/help/forms/manage-publication.md).

>[!ENDTABS]

## URL modulo

I moduli pubblicati sono accessibili tramite URL di Edge Delivery Services.

### Struttura URL

- **In prova (anteprima/prova):**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **Live (produzione):**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### Parametri URL

- `<branch>`: nome ramo GitHub (ad esempio `main`, `develop`)
- `<repo>`: nome archivio GitHub (esempio: `my-forms-project`)
- `<owner>`: organizzazione GitHub o nome utente (ad esempio, `company-name`)
- `<form_name>`: identificatore del modulo definito in AEM (ad esempio, `contact-us`)

#### Esempio

Esempio per il modulo `contact-us` nell&#39;archivio `forms-project` nell&#39;organizzazione `acme-corp`:

- **In prova:** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **Live:** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### Differenze di ambiente

- **In attesa (.page):** Ultime modifiche per il test.
- **Live (.live):** contenuto pubblicato per la produzione.

![Struttura URL](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*raggruppamento struttura URL modulo Edge Delivery Services*

#### Esempi visivi

**Modello Edge Delivery Services:**

- In prova: ![Versione in prova modulo di registrazione](/help/forms/assets/registration-form-staged-version.png)
- Live: ![Versione live del modulo di registrazione](/help/forms/assets/registration-form-live-version.png)

**Modello Componente Core:**

- In prova: ![Versione in prova modulo di iscrizione](/help/forms/assets/enrollment-form-staged-version.png)
- Live: ![Versione live del modulo di iscrizione](/help/forms/assets/enrollment-form-live-version.png)

## Risoluzione di problemi

Di seguito sono riportati i problemi comuni e le soluzioni di AEM Forms con Edge Delivery Services.

+++Modulo non caricato

**Problema:** l&#39;URL del modulo restituisce una pagina vuota o 404.

**Risoluzione:**

- Rimuovi l&#39;estensione `.html` dagli URL.
- Verifica che il modulo sia pubblicato.
- Controlla l’archivio GitHub per il blocco Forms adattivo.
- Assicurati che il nome del modulo corrisponda all’URL (distinzione maiuscole/minuscole).

+++

+++Problemi di configurazione

**Problema:** la configurazione di Edge Delivery Services non funziona.

**Risoluzione:**

- Verificare che l&#39;URL GitHub sia nel formato `https://github.com/owner/repository`.
- Utilizza il nome del ramo corretto nella configurazione.
- Verificare l&#39;accesso all&#39;archivio (pubblico o autenticato).
- Controllare `fstab.yaml` per i dettagli GitHub corretti.

+++

+++Problemi di pubblicazione

**Problema:** le modifiche non vengono visualizzate nel sito attivo.

**Risoluzione:**

- Attendere 2-3 minuti per l’aggiornamento della cache CDN.
- Conferma il completamento del flusso di lavoro di pubblicazione.
- Esegui prima il test nell’ambiente di staging (.page).
- Assicurati che l’archivio GitHub sia aggiornato.

+++

+++Problemi relativi all’editor universale

**Problema:** Impossibile modificare il modulo o i componenti senza caricarli.

**Risoluzione:**

- Utilizza un browser supportato (Chrome, Firefox, Safari).
- Cancella la cache del browser e i cookie.
- Verificare la connettività di rete.
- Conferma le autorizzazioni di creazione.

+++

+++Errori di invio modulo

**Problema:** invii modulo non funzionanti.

**Risoluzione:**

- Configura l’azione di invio nelle proprietà del modulo.
- Test manuale degli endpoint per l’invio.
- Se incorpori moduli, seleziona le impostazioni CORS.
- Verifica che i campi obbligatori siano configurati.

+++

+++Problemi di prestazioni

**Problema:** caricamento del modulo lento o prestazioni insoddisfacenti.

**Risoluzione:**

- Ottimizzare le immagini.
- Rimuovere i componenti non necessari.
- Utilizzo di Edge Delivery Services CDN.
- Riduci a icona JavaScript/CSS personalizzato.

+++

+++Come trovare assistenza

Se i problemi persistono:

1. Verifica lo stato del servizio Adobe Experience Cloud.
2. Rivedi la [documentazione di Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=it).
3. Visita la [community Adobe Experience League](https://experienceleaguecommunities.adobe.com/).
4. Contatta l’Assistenza clienti di Adobe.

+++

## Passaggi successivi

Dopo aver completato la creazione e la pubblicazione del modulo, considera quanto segue:

### Azioni immediate

- Eseguire il test del modulo utilizzando questa guida.
- Convalida l’archivio GitHub e la connessione AEM.
- Esaminare i moduli di esempio.

### Argomenti avanzati

- [Configurare le azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md): configurare la gestione dei dati e le integrazioni.
- [Modelli dati modulo](/help/forms/create-form-data-models.md): connettere i moduli a origini dati back-end.

### Ottimizzazione delle prestazioni

- [Best practice per Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=it): massimizzare le prestazioni.
- [Analisi modulo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html): tieni traccia delle prestazioni del modulo e del comportamento dell&#39;utente.

