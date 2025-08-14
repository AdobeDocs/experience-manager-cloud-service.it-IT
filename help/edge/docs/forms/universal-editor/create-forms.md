---
title: Creare e pubblicare Forms adattivo con Edge Delivery Services
description: Istruzioni dettagliate per la creazione, l’authoring e la pubblicazione di Adaptive Forms utilizzando i modelli di Edge Delivery Services in AEM, con particolare attenzione all’accuratezza e alla chiarezza tecnica.
keywords: moduli adattivi, servizi di consegna edge, editor universale, creazione di moduli, AEM forms, pubblicazione di moduli
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---


# Creare e pubblicare Forms adattivo con Edge Delivery Services

Questo documento fornisce istruzioni dettagliate per la creazione, la configurazione e la pubblicazione di Adaptive Forms utilizzando i modelli di Edge Delivery Services in AEM. Copre l’intero flusso di lavoro, dalla creazione dei moduli all’implementazione in produzione.

Al termine di questa guida, imparerai a:

- Creare moduli utilizzando i modelli di Edge Delivery Services
- Creare moduli con l’Editor universale
- Configurare e pubblicare moduli in Edge Delivery Services
- Accedere ai moduli pubblicati e verificare la distribuzione



## Prerequisiti

Prima di procedere, assicurati che siano soddisfatti i seguenti prerequisiti:


- **AEM Forms as a Cloud Service**: istanza di authoring attiva con una licenza Forms.
- **Account GitHub**: account personale o organizzativo per la gestione dell&#39;archivio.
- **Configurazione archivio**: scegliere una delle opzioni seguenti:
   - **Nuovo progetto**: [Crea un nuovo progetto AEM con blocco Forms adattivo](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). L’archivio è preconfigurato per Edge Delivery Services.
   - **Progetto esistente**: [Aggiungi blocco Forms adattivo a un repository esistente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) e aggiorna la configurazione.

- **Connessione AEM-GitHub**: [Stabilire una connessione](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) tra l&#39;istanza AEM e l&#39;archivio GitHub.
- **Edge Delivery Services**: verificare che l&#39;archivio sia configurato per la distribuzione automatica.
- **Autorizzazioni**: verificare di disporre dei diritti di accesso necessari per la creazione e la pubblicazione dei moduli.

- Conferma che l’archivio GitHub contenga il blocco Forms adattivo.



## Flusso di lavoro di creazione e pubblicazione di moduli

Il processo si articola in tre fasi principali:

- **Fase 1:** [Creazione modulo](#step-1-form-creation)
- **Fase 2:** [Authoring e progettazione dei moduli](#step-2-form-authoring-and-design)
- **Fase 3:** [Configurazione e pubblicazione](#step-3-configuration-and-publishing)

Ogni fase include passaggi di convalida per confermare la corretta configurazione.


### Passaggio 1: creazione di moduli

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

### Passaggio 2: authoring e progettazione dei moduli


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
   - Regola lo stile e il layout in base alle esigenze.

   ![Modulo di registrazione completato](/help/edge/assets/contact-us.png)

#### Convalida

- Tutti i campi obbligatori sono presenti.
- Le proprietà del campo sono configurate correttamente.
- Il layout è dinamico e accessibile.
- Le regole di convalida funzionano come previsto.

#### Passaggi successivi

- [Configurare le azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per la gestione dei dati.
- [Guida dell&#39;editor universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) per le funzionalità avanzate.

### Passaggio 3: configurazione e pubblicazione

Configura Edge Delivery Services e pubblica il modulo.

**Configurazione:** automatica (non è richiesta alcuna configurazione manuale).

- La connessione all’archivio GitHub e la configurazione di Edge Delivery Services vengono create durante la creazione del modulo.
- Gli endpoint di pubblicazione vengono configurati automaticamente.

**Verifica:**

- Conferma che la configurazione venga visualizzata nelle impostazioni del modulo.
- Verifica che l’URL GitHub sia collegato correttamente.

![Configurazione automatica EDS](/help/edge/assets/aem-instance-eds-configuration.png)

#### Pubblicazione del modulo

1. In Universal Editor, fare clic sul pulsante **Pubblica** (angolo superiore destro).
2. Conferma la pubblicazione nella finestra di dialogo.
3. Prendi nota degli URL generati per le versioni in staging e live.

   ![Pubblicazione editor universale](/help/edge/assets/publish-form.png)

- [Guida alla pubblicazione](/help/edge/docs/forms/universal-editor/publish-forms.md)

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

+++Problemi relativi alle prestazioni

**Problema:** caricamento del modulo lento o prestazioni insoddisfacenti.

**Risoluzione:**

- Ottimizzare le immagini.
- Rimuovere i componenti non necessari.
- Utilizzo di Edge Delivery Services CDN.
- Riduci a icona JavaScript/CSS personalizzato.

+++

+++Ottenimento della Guida

Se i problemi persistono:

1. Verifica lo stato del servizio Adobe Experience Cloud.
2. Rivedi la [documentazione di Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=it).
3. Visita la [community Adobe Experience League](https://experienceleaguecommunities.adobe.com/).
4. Contatta l’Assistenza clienti di Adobe.

+++

## Passaggi successivi

Dopo aver completato la creazione e la pubblicazione del modulo, considera quanto segue:

- [Configurare le azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md): configurare la gestione dei dati e le integrazioni.
- [Modelli dati modulo](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md): connettere i moduli a origini dati back-end.
- [Best practice per Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=it): massimizzare le prestazioni.
- [Analisi modulo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html): tieni traccia delle prestazioni del modulo e del comportamento dell&#39;utente.

