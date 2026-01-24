---
title: Creare e pubblicare moduli adattivi con Edge Delivery Services
description: Istruzioni dettagliate per la creazione, l’authoring e la pubblicazione di moduli adattivi utilizzando i modelli Edge Delivery Services in AEM, con particolare attenzione all’accuratezza e alla chiarezza tecnica.
keywords: moduli adattivi, edge delivery service, editor universale, creazione di moduli, AEM forms, pubblicazione di moduli
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: ht
source-wordcount: '1005'
ht-degree: 100%

---


# Creare e pubblicare moduli adattivi con Edge Delivery Services

Questo documento fornisce istruzioni dettagliate per la creazione, la configurazione e la pubblicazione di moduli adattivi utilizzando i modelli di Edge Delivery Services in AEM. Copre l’intero flusso di lavoro, dalla creazione dei moduli all’implementazione nella produzione.

Al termine di questa guida, imparerai come:

- Creare moduli utilizzando i modelli di Edge Delivery Services
- Authoring dei moduli utilizzando l’editor universale
- Configurare e pubblicare moduli in Edge Delivery Services
- Accedere ai moduli pubblicati e verificare la distribuzione



## Prerequisiti

Prima di procedere, assicurati che siano soddisfatti i seguenti prerequisiti:


- **AEM Forms as a Cloud Service**: istanza di authoring attiva con una licenza per Moduli.
- **Account GitHub**: account personale o organizzativo per la gestione dell’archivio.
- **Configurazione archivio**: scegli una delle opzioni seguenti:
   - **Nuovo progetto**: [crea un nuovo progetto AEM con il Blocco moduli adattivi](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). L’archivio è preconfigurato per Edge Delivery Services.
   - **Progetto esistente**: [aggiungi il Blocco moduli adattivi a un archivio esistente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) e aggiorna la configurazione.

- **Connessione AEM-GitHub**: [stabilisci una connessione](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) tra l’istanza AEM e l’archivio GitHub.
- **Edge Delivery Services**: verifica che l’archivio sia configurato per la distribuzione automatica.
- **Autorizzazioni**: verifica di disporre dei diritti di accesso necessari per la creazione e la pubblicazione dei moduli.

- Conferma che l’archivio GitHub contenga il blocco dei moduli adattivi.



## Flusso di lavoro di creazione e pubblicazione di moduli

Il processo è composto da tre fasi principali:

- **Fase 1:** [creazione del modulo](#step-1-form-creation)
- **Fase 2:** [authoring e progettazione dei moduli](#step-2-form-authoring-and-design)
- **Fase 3:** [configurazione e pubblicazione](#step-3-configuration-and-publishing)

Ogni fase include passaggi di convalida per confermare la corretta configurazione.


### Fase 1: creazione de modulo

1. **Creazione del modulo di accesso**
   - Accedi all’istanza di authoring di AEM Forms as a Cloud Service.
   - Passa ad **Adobe Experience Manager** > **Moduli** > **Moduli e documenti**.
   - Seleziona **Crea** > **Moduli adattivi**.

1. **Seleziona modello**
   - Nella scheda **Origine**, seleziona un **modello basato su Edge Delivery Services**.
   - Il pulsante **Crea** viene attivato.

     ![Creare moduli EDS](/help/edge/assets/create-eds-forms.png)

1. **Configurare opzioni (facoltativo)**
   - **Scheda Origine dati**: se necessario, seleziona l’integrazione dei dati.
   - **Scheda invio**: scegli un’azione di invio (configurabile in seguito).
   - **Scheda consegna**: imposta la pianificazione della pubblicazione/annullamento della pubblicazione.

1. **Completa la configurazione del modulo**
   - Fai clic su **Crea** per aprire la procedura guidata per la creazione di moduli.
   - Immetti le seguenti informazioni:
      - **Nome**: identificatore interno (senza spazi, usa i trattini).
      - **Titolo**: nome visualizzato per il modulo.
      - **URL di GitHub**: URL dell’archivio (ad esempio, `https://github.com/your-org/your-repo`).

   ![Procedura guidata per la creazione di un modulo](/help/edge/assets/create-form-wizard.png)

1. **Convalida**
   - Dopo aver fatto clic su **Crea**, verifica che:
      - Il modulo venga aperto nell’editor universale.
      - L’URL di GitHub sia collegato correttamente.
      - La palette dei componenti sia disponibile.
      - L’area di lavoro del modulo sia visibile.

   ![Interfaccia dell’editor universale](/help/edge/assets/author-form.png)

**Risultato:** il modulo è pronto per l’authoring nell’editor universale.

### Passaggio 2: authoring e progettazione dei moduli


1. **Accedere alla libreria dei componenti**
   - Apri il browser Contenuto nell’editor universale.
   - Passa al componente **Modulo adattivo** nella struttura contenuto.

   ![Navigazione della struttura contenuto](/help/edge/assets/content-tree.png)

1. **Aggiungere i campi modulo**
   - Fai clic sull’icona **Aggiungi** per aprire la libreria dei componenti.
   - Seleziona i componenti dall’elenco **Componenti del modulo adattivo**.
   - Trascina i componenti nell’area di lavoro del modulo.

   ![Aggiungere componenti](/help/edge/assets/add-component.png)

1. **Progettare il modulo**
   - Configurare le proprietà del campo nel pannello delle proprietà.
   - Imposta regole e comportamenti di convalida.
   - Regola lo stile e il layout in base alle esigenze.

   ![Modulo di registrazione completato](/help/edge/assets/contact-us.png)

#### Convalida

- Tutti i campi obbligatori sono presenti.
- Le proprietà del campo sono configurate correttamente.
- Il layout è dinamico e accessibile.
- Le regole di convalida funzionano come previsto.

#### Passaggi successivi

- [Configura le azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per la gestione dei dati.
- [Guida all’editor universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) per le funzioni avanzate.

### Passaggio 3: configurazione e pubblicazione

Configura Edge Delivery Services e pubblica il modulo.

**Configurazione:** automatica (non è richiesta alcuna configurazione manuale).

- La connessione all’archivio GitHub e la configurazione di Edge Delivery Services vengono create durante la creazione del modulo.
- Gli endpoint di pubblicazione vengono configurati automaticamente.

**Verifica:**

- Conferma che la configurazione venga visualizzata nelle impostazioni del modulo.
- Assicurati che l’URL GitHub sia collegato correttamente.

![Configurazione automatica EDS](/help/edge/assets/aem-instance-eds-configuration.png)

#### Pubblicazione del modulo

1. Nell’editor universale, fai clic sul pulsante **Pubblica** (nell’angolo in alto a destra).
2. Conferma la pubblicazione riuscita nella finestra di dialogo.
3. Prendi nota degli URL generati per le versioni in prova e live.

   ![Pubblicare con l’editor universale](/help/edge/assets/publish-form.png)

- [Guida alla pubblicazione](/help/edge/docs/forms/universal-editor/publish-forms.md)

## URL del modulo

I moduli pubblicati sono accessibili tramite gli URL di Edge Delivery Services.

### Struttura dell’URL

- **In staging (anteprima/test):**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **Live (produzione):**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### Parametri URL

- `<branch>`: nome ramo GitHub (ad esempio, `main`, `develop`)
- `<repo>`: nome archivio GitHub (ad esempio, `my-forms-project`)
- `<owner>`: organizzazione GitHub o nome utente (ad esempio, `company-name`)
- `<form_name>`: identificatore del modulo definito in AEM (ad esempio, `contact-us`)

#### Esempio

Esempio per il modulo `contact-us` nell’archivio `forms-project` nell’organizzazione `acme-corp`:

- **In staging:** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **Live:** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### Differenze di ambiente

- **Staging (.page):** ultime modifiche per il test.
- **Live (.live):** contenuto pubblicato per la produzione.

![Struttura URL](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*raggruppamento della struttura URL per modulo Edge Delivery Services*

#### Esempi visivi

**Modello di Edge Delivery Services:**

- Staging: ![versione di staging modulo di registrazione](/help/forms/assets/registration-form-staged-version.png)
- Live: ![versione live del modulo di registrazione](/help/forms/assets/registration-form-live-version.png)

## Risoluzione di problemi

Di seguito sono riportati i problemi comuni e le soluzioni di AEM Forms con Edge Delivery Services.

+++Modulo che non si carica

**Problema:** l’URL del modulo restituisce una pagina vuota o l’errore 404.

**Risoluzione:**

- Rimuovi l’estensione `.html` dagli URL.
- Verifica che il modulo sia pubblicato.
- Controlla l’archivio GitHub per il blocco dei moduli adattivi.
- Assicurati che il nome del modulo corrisponda all’URL (distinzione maiuscole/minuscole).

+++

+++Problemi di configurazione

**Problema:** la configurazione di Edge Delivery Services non funziona.

**Risoluzione:**

- Assicurati che l’URL GitHub sia nel formato `https://github.com/owner/repository`.
- Utilizza il nome del ramo corretto nella configurazione.
- Verifica l’accesso all’archivio (pubblico o autenticato).
- Controlla `fstab.yaml` per i dettagli GitHub corretti.

+++

+++Problemi di pubblicazione

**Problema:** le modifiche non vengono visualizzate nel sito attivo.

**Risoluzione:**

- Attendi 2-3 minuti per l’aggiornamento della cache CDN.
- Conferma il completamento del flusso di lavoro di pubblicazione.
- Esegui prima il test nell’ambiente di staging (.page).
- Assicurati che l’archivio GitHub sia aggiornato.

+++

+++Problemi relativi all’editor universale

**Problema:** impossibile modificare il modulo o i componenti senza caricarli.

**Risoluzione:**

- Utilizza un browser supportato (Chrome, Firefox, Safari).
- Cancella la cache del browser e i cookie.
- Verifica la connettività di rete.
- Conferma le autorizzazioni di creazione.

+++

+++Errori di invio modulo

**Problema:** invii modulo non funzionanti.

**Risoluzione:**

- Configura l’azione di invio nelle proprietà del modulo.
- Testa gli endpoint per l’invio in modo manuale.
- Se incorpori moduli, seleziona le impostazioni CORS.
- Verifica che i campi obbligatori siano configurati.

+++

+++Problemi relativi alle prestazioni

**Problema:** caricamento del modulo lento o prestazioni scarse.

**Risoluzione:**

- Ottimizza le immagini.
- Rimuovi i componenti non necessari.
- Sfrutta la CDN Edge Delivery Services.
- Riduci a icona JavaScript/CSS personalizzato.

+++

+++Come trovare assistenza

Se i problemi persistono:

1. Verifica lo stato del servizio Adobe Experience Cloud.
2. Rivedi la [documentazione di Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=it).
3. Visita la [community Adobe Experience League](https://experienceleaguecommunities.adobe.com/?profile.language=it).
4. Contatta l’Assistenza clienti Adobe.

+++

## Passaggi successivi

Dopo aver completato la creazione e la pubblicazione del modulo, considera quanto segue:

- [Configura le azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md): configura la gestione dei dati e le integrazioni.
- [Modelli dati modulo](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md): connetti i moduli a origini dati back-end.
- [Best practice per Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=it): massimizza le prestazioni.
- [Analisi modulo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html?lang=it): tieni traccia delle prestazioni del modulo e del comportamento degli utenti.

