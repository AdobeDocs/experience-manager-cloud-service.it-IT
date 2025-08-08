---
title: Come si precompilano i campi del modulo adattivo?
description: Utilizza i dati esistenti per precompilare i campi di un modulo adattivo. Gli utenti possono precompilare le informazioni di base in un modulo accedendo con i loro profili social.
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: precompilare un modulo adattivo, servizi di consegna edge di moduli adattivi, riempimento automatico di moduli adattivi
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 2%

---


# Configurazione del servizio di preriempimento in Adaptive Forms tramite Edge Delivery Services

La precompilazione dei moduli è il processo di compilazione automatica dei campi modulo con i dati rilevanti provenienti da origini esterne, non appena un utente apre il modulo. Sfruttando le informazioni provenienti da profili utente, database, bozze salvate o altri sistemi back-end, la precompilazione semplifica l’esperienza di compilazione dei moduli, riducendo l’input manuale, riducendo al minimo gli errori e accelerando il completamento. Ciò non solo migliora la soddisfazione degli utenti, ma aumenta anche la probabilità di successo nell’invio dei moduli.

## Vantaggi della precompilazione dei moduli

| Beneficio | Descrizione |
|---------|-------------|
| **Completamento più rapido** | Riduce l&#39;immissione manuale dei dati, consentendo agli utenti di completare rapidamente i moduli |
| **Esperienza utente migliorata** | Forms si sente più personalizzato e comodo, soprattutto per gli utenti di ritorno |
| **Tassi di conversione più elevati** | Riduce l’abbandono dei moduli riducendo al minimo lo sforzo utente richiesto |
| **Errori di input ridotti** | I dati provenienti da fonti attendibili riducono gli errori di battitura e le voci errate |
| **Migliore qualità dei dati** | Garantisce dati strutturati, precisi e coerenti per i sistemi back-end |

## Come funziona la precompilazione

Il diagramma seguente illustra il processo di precompilazione automatica che si verifica quando un utente apre un modulo adattivo:

![Flusso del processo di precompilazione del modulo](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

Il processo di precompilazione prevede quattro passaggi chiave:

1. **Modulo aperto dall&#39;utente**: l&#39;utente accede a un modulo adattivo tramite un URL o un sistema di navigazione
2. **Identifica Source dati**: il servizio di precompilazione determina l&#39;origine dati configurata (modello dati modulo o servizio bozza)
3. **Recupera dati**: il sistema recupera i dati utente pertinenti in base al contesto, ai parametri o all&#39;identificazione utente
4. **Mappa e visualizza**: i dati sono mappati ai campi modulo utilizzando le proprietà `bindRef` e il modulo compilato viene visualizzato all&#39;utente

Questo processo automatizzato garantisce agli utenti di visualizzare un modulo precompilato con le informazioni pertinenti, migliorando in modo significativo l’esperienza utente e i tassi di completamento dei moduli.

## Struttura dei dati per la precompilazione

Forms adattivo supporta due tipi di campi:

- **Campi associati**: campi connessi a un&#39;origine dati con una proprietà `bindRef` non vuota
- **Campi non associati**: campi autonomi con valori `bindRef` vuoti

La struttura dei dati di precompilazione include:

- **afBoundData**: contiene dati per campi e pannelli associati
- **afUnBoundData**: contiene dati per campi non associati

Il formato dei dati deve corrispondere al modello del modulo:

- **Moduli XFA**: XML conforme allo schema modello XFA
- **Moduli schema XML**: XML corrispondente alla struttura dello schema
- **Moduli schema JSON**: conformi allo schema JSON
- **Moduli FDM (Form Data Model)**: JSON corrispondente alla struttura FDM
- **Moduli senza schema**: tutti i campi non sono associati e utilizzano XML non associato


## Prerequisiti

Prima di configurare i servizi di preriempimento, assicurati di disporre di:

### Configurazione necessaria

- [Archivio GitHub configurato per Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [Blocco Forms adattivo aggiunto al progetto](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [Origine dati configurata](/help/forms/configure-data-sources.md)
- [Modello dati modulo (FDM) creato](/help/forms/create-form-data-models.md)

### Requisiti di accesso

- Accesso ad AEM Forms as a Cloud Service
- Autorizzazioni per creare e modificare i moduli
- Accesso all’editor universale con le estensioni richieste abilitate

>[!TIP]
>
> È inoltre possibile modificare i moduli per integrare Form Data Model (FDM) nell’Editor universale per recuperare dati da varie origini back-end. Per ulteriori informazioni, vedere l&#39;articolo [Integrare i moduli con il modello dati del modulo nell&#39;editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

## Opzioni del servizio preriempimento

Universal Editor offre due opzioni di servizio di precompilazione:

| Tipo servizio | Scopo | Origine dati | Ideale per |
|--------------|---------|-------------|----------|
| **Precompilazione bozza portale moduli** | Riprende i moduli parzialmente completati | Bozze salvate in Forms Portal | Continuazione delle applicazioni incomplete |
| **Precompilazione modello dati modulo** | Compila i campi da sistemi esterni | Database back-end tramite FDM | Compilazione automatica dei dati del profilo utente |

### Confronto dettagliato

| Funzione | Servizio preriempimento bozza | Servizio preriempimento FDM |
|---------|----------------------|---------------------|
| **Autenticazione** | Richiede l&#39;accesso come bozza all&#39;utente | Configurabile in base all’origine dati |
| **Complessità installazione** | Configurazione minima | Richiede la configurazione e la mappatura di FDM |
| **Tipo di dati** | Dati statici salvati | Dati dinamici in tempo reale |
| **Caso d’uso** | Riprendi applicazioni salvate | Precompilare da profili utente o database |


## Configurare il servizio di precompilazione per un modulo


+++Fase 1: Impostazione del modello dati del modulo

### Passaggio 1: creare il modello dati del modulo

1. Accedi all’istanza di AEM Forms as a Cloud Service
2. Passa a **Adobe Experience Manager** > **Forms** > **Integrazioni dati**
3. Seleziona **Crea** > **Modello dati modulo**
4. Scegli la tua **configurazione Source dati** e seleziona il **Source dati** configurato

   ![Modello dati modulo creato](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   > Per istruzioni dettagliate sulla creazione di modelli dati modulo, vedi [Crea modello dati modulo](/help/forms/create-form-data-models.md).

### Passaggio 2: configurare i servizi FDM

1. Vai a **Adobe Experience Manager** > **Forms** > **Integrazioni dati**
2. Aprire il modello dati modulo in modalità di modifica
3. Seleziona un oggetto modello dati e fai clic su **Modifica proprietà**
4. Configura i servizi **Lettura** e **Scrittura** per gli oggetti modello dati selezionati

   ![Configura servizio di lettura/scrittura](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

5. Configurare gli argomenti del servizio:
   - Fai clic sull’icona Modifica per l’argomento Servizio di lettura
   - Associa l&#39;argomento a un **attributo profilo utente**, **attributo richiesta** o **valore letterale**
   - Specificare il valore di binding (ad esempio, `petid` per un modulo di registrazione per animali domestici)

   ![Configura argomento ID animale domestico](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

6. Fai clic su **Fine** per salvare l&#39;argomento e su **Salva** per salvare FDM

       >[!NOTA]
       >
   > Ulteriori informazioni sulla configurazione dei servizi FDM in [Utilizzare il modello dati modulo (FDM)](/help/forms/work-with-form-data-model.md).

+++

+++Fase 2: Creazione e configurazione del modulo adattivo

### Passaggio 3: creare un modulo adattivo

1. Passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**
2. Seleziona **Crea** > **Forms adattivo**
3. Nella scheda **Source** selezionare un modello di Edge Delivery Services:

       .[Modello Edge Delivery Services](/help/edge/assets/create-eds-forms.png)
   
4. Fai clic su **Crea** per aprire la procedura guidata **Crea modulo**
5. Specifica i dettagli del modulo:
   - **Nome**: immetti un nome descrittivo per il modulo
   - **Titolo**: fornisci un titolo intuitivo
   - **URL GitHub**: immetti l&#39;URL dell&#39;archivio (ad esempio, `https://github.com/wkndforms/edsforms`)

6. Fai clic su **Crea**.

       .[Crea modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)
   
Il modulo viene aperto nell’editor universale per l’authoring.

### Passaggio 4: configurare Source dati modulo

1. Seleziona il modulo e fai clic su **Proprietà**

       .[Seleziona proprietà modulo](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)
   
2. Apri la scheda **Modello modulo**
3. Dal menu a discesa **Seleziona da**, scegli **Modello dati modulo (FDM)**
4. Seleziona il Modello dati modulo creato (ad esempio, PetFDM) dal menu a discesa

       .[Selezionare la scheda Modello modulo](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)
   
5. Fai clic su **Salva e chiudi**
6. Apri il modulo per la modifica in Editor universale

Gli elementi del modulo dal tuo FDM vengono visualizzati nella scheda **Origine dati** del **Browser contenuti**.

### Passaggio 5: aggiungere l’associazione dati ai campi modulo

1. Seleziona elementi dati dalla scheda **Origine dati**
2. Fai clic su **Aggiungi** o trascina gli elementi per creare il modulo

   ![Schermata di Universal Editor che mostra il modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. Aggiungere l&#39;associazione dati ai campi modulo:
   - Seleziona un campo modulo
   - Nel pannello **Proprietà**, individua la proprietà **Riferimento binding**
   - Selezionare il riferimento di associazione dati appropriato

     ![Associazione dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++Fase 3: Configurazione del servizio di preriempimento

### Passaggio 6: abilitare le estensioni richieste

Assicurati che queste estensioni siano abilitate in Universal Editor:

1. **Estensione proprietà AEM Form**
   - Apri **Extension Manager** nell&#39;editor universale
   - Abilita l&#39;estensione **AEM Form Properties**

   ![Icona proprietà modulo](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

2. **Estensione Data Source**
   - Abilita l&#39;estensione **Origine dati** se non vedi l&#39;icona **Origini dati**

   ![Schermata di Universal Editor Extension Manager](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > Per istruzioni dettagliate sulla gestione delle estensioni, consulta [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

### Passaggio 7: configurare il servizio di preriempimento

1. Aprire il modulo adattivo nell’editor universale
2. Fai clic sull&#39;icona dell&#39;estensione **AEM Form Properties**

   ![Icona Seleziona proprietà modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. Fai clic sulla scheda **Precompila**
4. Seleziona **Servizio di precompilazione modello dati modulo**

       .[Selezionare il servizio di precompilazione](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)
   
5. Fai clic su **Salva e chiudi**

+++

+++Fase 4: Verifica della configurazione di preriempimento

### Passaggio 8: anteprima e test

1. Vai a **Forms** > **Forms e documenti**
2. Seleziona il modulo adattivo
3. Scegli **Anteprima come HTML**
4. Verifica la precompilazione aggiungendo i parametri all’URL:

       https://your-preview-url.com?&lt;bindreferencefield>=&lt;valore>
   
   **Esempio:**

       https://your-preview-url.com?petid=12345
       
       [Modulo precompilato](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)
   
Il modulo deve essere compilato automaticamente con dati basati sul parametro fornito.

+++

## Esempi

### Esempi di strutture di dati di preriempimento

**Esempio JSON per modulo basato su FDM:**

    &quot;
    
    {
    &quot;afBoundData&quot;: {
    &quot;user&quot;: {
    &quot;firstName&quot;: &quot;John&quot;,
    &quot;lastName&quot;: &quot;Doe&quot;,
    &quot;email&quot;: &quot;john.doe@example.com&quot;,
    &quot;phone&quot;: &quot;+1-555-0123&quot;
    }
    },
    &quot;afUnBoundData&quot;: {
    &quot;additionalInfo&quot;: &quot;Preferenze utente&quot; caricato&quot;
    }
    }
    
    &quot;

**Esempio XML per modulo basato su XFA:**

    &quot;
    
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?>
    &lt;afData>
    &lt;afBoundData>
    &lt;utente>
    &lt;firstName>John&lt;/firstName>
    &lt;lastName>Doe&lt;/lastName>
    &lt;email>john.doe@example.com&lt;/email>
    &lt;/user>
    &lt;/afBoundData>
    &lt;/afData>
    
    &quot;

### Esempio di URL di precompilazione

Gli URL riportati di seguito hanno solo scopo illustrativo e non funzioneranno così come sono. Durante il test della funzionalità di precaricamento, sostituisci l’host e i parametri con quelli pertinenti per il tuo ambiente.

**Test di precompilazione di base:**

    https://preview.example.com/form.html?userId=12345

**Test con più parametri:**

    https://preview.example.com/form.html?userId=12345&amp;category=premium


## Risoluzione di problemi

+++Problemi comuni e soluzioni

| Problema   | Causa possibile | Soluzione |
|-------|----------------|----------|
| **I campi modulo non vengono precompilati** | Valori `bindRef` errati | Verifica che `bindRef` corrisponda esattamente ai nomi dei campi FDM |
| **Errori di formato dati** | Struttura dei dati non corrispondente | Assicurati che i dati precompilati corrispondano allo schema del modello del modulo |
| **Servizio non trovato** | Problemi di configurazione FDM | Verificare che i servizi FDM siano configurati e salvati correttamente |
| **Errori di autenticazione** | Connettività all’origine dati | Verificare le credenziali dell’origine dati e la connettività |
| **Caricamento dati parziale** | Mappature campo mancanti | Assicurati che tutti i campi obbligatori abbiano associazioni dati corrette |

+++

+++Passaggi di debug

1. **Verifica configurazione FDM:**
   - Verifica se i servizi sono configurati correttamente
   - Test indipendente dei servizi FDM
   - Convalidare la connettività dell’origine dati

2. **Verifica configurazione modulo:**
   - Il modulo di conferma è associato a FDM corretto
   - Verifica valori campo `bindRef`
   - Modulo di prova senza precompilazione

3. **Flusso dati di prova:**
   - Utilizzare gli strumenti di sviluppo del browser per verificare le richieste di rete
   - Verifica la presenza di errori JavaScript nella console
   - Convalida formato dati risposta

4. **Messaggi di errore comuni:**
   - &quot;Servizio di precompilazione non trovato&quot;: verifica la configurazione del servizio
   - &quot;Associazione dati non riuscita&quot;: verificare la precisione di `bindRef`
   - &quot;Formato dati non valido&quot;: verifica che i dati corrispondano allo schema

+++

## Best practice

+++Best practice per la configurazione

- **Denominazione descrittiva**: assegna un nome chiaro agli FDM e ai servizi
- **Convalida schemi dati**: verificare che la struttura dati corrisponda ai requisiti del modulo
- **Test incrementale**: configura e verifica un campo alla volta
- **Mappature documenti**: tieni traccia delle mappature campo-dati

+++

+++Ottimizzazione delle prestazioni

- **Riduci al minimo il volume di dati**: precompila solo i campi necessari
- **Usa memorizzazione nella cache**: configura la memorizzazione nella cache appropriata per i dati ad accesso frequente
- **Ottimizzare le query**: garantire l&#39;efficienza delle query del database
- **Monitoraggio delle prestazioni**: tieni traccia dei tempi di caricamento dei moduli con la precompilazione abilitata

+++

+++Considerazioni sulla sicurezza

- **Convalida parametri di input**: convalida sempre parametri URL
- **Sanitizza dati**: pulisci i dati prima di precompilare i moduli
- **Implementare i controlli di accesso**: assicurarsi che gli utenti possano accedere solo ai propri dati
- **Usa HTTPS**: utilizza sempre connessioni sicure per la trasmissione dei dati

+++

+++Linee guida sull’esperienza utente

- **Fornisci feedback**: mostra gli indicatori di caricamento durante il recupero dei dati
- **Gestione corretta degli errori**: visualizzazione di messaggi di errore utili
- **Consenti sostituzioni**: consenti agli utenti di modificare i dati precompilati
- **Mantieni coerenza**: utilizza un comportamento di precompilazione coerente nei moduli

+++

## Domande frequenti

+++Come posso verificare se la precompilazione funziona correttamente?

Visualizzare l&#39;anteprima del modulo e aggiungere i parametri di precompilazione all&#39;URL utilizzando questo formato: `?<bindreferencefield>=<value>`. Assicurati che il campo abbia un `bindRef` valido che corrisponda alla struttura dati. Utilizza gli strumenti di sviluppo del browser per verificare le richieste di rete e che i dati vengano recuperati correttamente.

+++

+++Quali formati di dati sono supportati per la precompilazione di Adaptive Forms?

Forms adattivo supporta più formati a seconda del modello di modulo:

- **Moduli XFA**: XML corrispondente allo schema XFA
- **Moduli schema JSON**: dati JSON conformi allo schema
- **Moduli FDM**: JSON mappato alla struttura del modello di dati
- **Moduli schema XML**: XML corrispondente alla struttura dello schema

+++

+++Posso precompilare sia i campi associati che quelli non associati?

Sì, è possibile precompilare entrambi i tipi di campi. I campi associati utilizzano la sezione `afBoundData` e devono corrispondere allo schema del modello del modulo. I campi non associati utilizzano la sezione `afUnBoundData` e possono contenere dati aggiuntivi.

+++

+++Cosa devo fare se solo alcuni campi sono precompilati?

Verifica che tutti i campi abbiano valori `bindRef` corretti che corrispondano esattamente al tuo FDM. Verifica che l’origine dati contenga tutti i campi obbligatori e che la struttura dati corrisponda allo schema del modello del modulo.

+++

+++Come posso gestire l’autenticazione per i servizi di preriempimento?

L’autenticazione dipende dalla configurazione dell’origine dati. Per la precompilazione basata su FDM, configura l’autenticazione nelle impostazioni dell’origine dati. Per la precompilazione delle bozze, gli utenti in genere devono aver effettuato l’accesso per accedere alle bozze salvate.

+++

+++È possibile utilizzare più servizi di precompilazione in un unico modulo?

Puoi configurare un servizio di precompilazione principale per modulo. Tuttavia, per ottenere funzionalità simili, è possibile combinare diverse origini dati all’interno di un singolo modello dati modulo.

+++

=
## Argomenti correlati

- [Integrare i moduli con il modello dati modulo nell’editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [Creare modelli dati modulo](/help/forms/create-form-data-models.md)
- [Utilizzare il modello dati del modulo](/help/forms/work-with-form-data-model.md)
- [Configurare origini dati](/help/forms/configure-data-sources.md)
- [Guida introduttiva di Edge Delivery Services per AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
