---
title: Come precompilare i campi del modulo adattivo
description: Utilizza i dati esistenti per precompilare i campi di un modulo adattivo. Gli utenti possono precompilare le informazioni di base in un modulo accedendo con i loro profili social.
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: precompilare un modulo adattivo, servizi di consegna edge di moduli adattivi, riempimento automatico di moduli adattivi
exl-id: 7b6224e2-a19c-4146-8545-0ce9d1da9b29
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1803'
ht-degree: 100%

---

# Configurazione del servizio di precompilazione nei moduli adattivi tramite Edge Delivery Services

La precompilazione dei moduli è il processo di compilazione automatica dei campi modulo con i dati rilevanti provenienti da origini esterne, non appena un utente apre il modulo. Sfruttando le informazioni provenienti da profili utente, database, bozze salvate o altri sistemi back-end, la precompilazione semplifica l’esperienza di compilazione dei moduli, riducendo l’input manuale, minimizzando gli errori e accelerando il completamento. Ciò non migliora solo la soddisfazione degli utenti, ma aumenta anche la probabilità di successo dell’invio dei moduli.

## Vantaggi della precompilazione dei moduli

| Vantaggio | Descrizione |
|---------|-------------|
| **Completamento più rapido** | Riduce l’immissione manuale dei dati, consentendo agli utenti di completare i moduli in modo rapido |
| **Esperienza utente migliorata** | I moduli risultano più personalizzati e pratici, soprattutto per gli utenti di ritorno |
| **Tassi di conversione più elevati** | Riduce l’abbandono dei moduli riducendo al minimo lo sforzo richiesto agli utenti |
| **Errori di input ridotti** | I dati provenienti da fonti attendibili riducono gli errori di battitura e le voci errate |
| **Migliore qualità dei dati** | Garantisce dati strutturati, precisi e coerenti per i sistemi back-end |

## Come funziona la precompilazione

Il diagramma seguente illustra il processo di precompilazione automatica che si verifica quando un utente apre un modulo adattivo:

![Flusso del processo di precompilazione del modulo](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

Il processo di precompilazione prevede quattro passaggi chiave:

1. **Apertura del modulo da parte dell’utente**: l’utente accede a un modulo adattivo tramite URL o navigazione
1. **Identificare l’origine dati**: il servizio di precompilazione determina l’origine dati configurata (modello dati modulo o servizio bozza)
1. **Recuperera i dati**: il sistema recupera i dati utente pertinenti in base al contesto, ai parametri o all’identificazione dell’utente
1. **Mappare e visualizzare**: i dati vengono mappati nei campi modulo utilizzando le proprietà `bindRef` e il modulo compilato viene mostrato all’utente

Questo processo automatizzato garantisce agli utenti di visualizzare un modulo precompilato con le informazioni pertinenti, migliorando in modo significativo l’esperienza utente e i tassi di completamento del modulo.

## Struttura dei dati per la precompilazione

I moduli adattivi supportano due tipi di campi:

- **Campi associati**: campi connessi a un’origine dati con una proprietà `bindRef` non vuota
- **Campi non associati**: campi autonomi con valori `bindRef` vuoti

La struttura dei dati di precompilazione include:

- **afBoundData**: contiene i dati per i campi e i pannelli associati
- **afUnBoundData**: contiene i dati per i campi non associati

Il formato dei dati deve corrispondere al modello del modulo:

- **Moduli XFA**: XML conforme allo schema del modello XFA
- **Moduli con schema XML**: XML corrispondente alla struttura dello schema
- **Moduli con schema JSON**: JSON conforme allo schema
- **Moduli con modelli dati modulo (FDM)**: JSON corrispondente alla struttura FDM
- **Moduli senza schema**: tutti i campi non sono associati e utilizzano XML non associati

## Prerequisiti

Prima di configurare i servizi di precompilazione, assicurati di disporre di:

### Configurazione richiesta

- [Archivio GitHub configurato per Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [Blocco di moduli adattivi aggiunto al progetto](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [Origine dati configurata](/help/forms/configure-data-sources.md)
- [Modello dati modulo (FDM) creato](/help/forms/create-form-data-models.md)

### Requisiti di accesso

- Accesso ad AEM Forms as a Cloud Service
- Autorizzazioni per creare e modificare i moduli
- Accesso all’editor universale con le estensioni richieste abilitate

>[!TIP]
>
> Puoi inoltre modificare i moduli per integrare il modello dati modulo (FDM) nell’editor universale per recuperare dati da varie origini back-end. Per ulteriori informazioni, consulta l’articolo [Integrare i moduli con il modello dati modulo nell’editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

## Opzioni del servizio di precompilazione

L’editor universale offre due opzioni di servizio di precompilazione:

| Tipo di servizio | Scopo | Origine dati | Ideale per |
|--------------|---------|-------------|----------|
| **Precompilazione bozza del portale dei moduli** | Riprendere i moduli parzialmente completati | Bozze salvate nel portale dei moduli | Continuazione delle applicazioni incomplete |
| **Precompilazione modello dati modulo** | Compilare i campi da sistemi esterni | Database di back-end tramite FDM | Compilazione automatica dei dati del profilo utente |

### Confronto dettagliato

| Funzione | Servizio di precompilazione bozza | Servizio precompilazione FDM |
|---------|----------------------|---------------------|
| **Autenticazione** | Richiede il login dell’utente per l’accesso alla bozza | Configurabile in base all’origine dati |
| **Complessità di configurazione** | Configurazione minima | Richiede la configurazione e la mappatura FDM |
| **Tipo di dati** | Dati statici salvati | Dati dinamici in tempo reale |
| **Caso d’uso** | Riprendere le applicazioni salvate | Precompilare da profili utente o database |


## Configurare il servizio di precompilazione per un modulo

+++Fase 1: impostazione del modello dati modulo

### Passaggio 1: creare il modello dati modulo

1. Accedi all’istanza di AEM Forms as a Cloud Service.
1. Passa a: **Adobe Experience Manager** > **Moduli** > **Integrazioni dati**
1. Seleziona **Crea** > **Modello dati modulo**
1. Scegli la **configurazione dell’origine dati** e seleziona l’**Origine dati** configurata

   ![Modello dati modulo creato](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >Per istruzioni dettagliate sulla creazione di modelli dati modulo, consulta [Creare il modello dati modulo](/help/forms/create-form-data-models.md).

### Passaggio 2: configurare i servizi FDM

1. Passa a **Adobe Experience Manager** > **Moduli** > **Integrazioni dati**
1. Apri il modello dati modulo in modalità di modifica
1. Seleziona un oggetto modello dati e fai clic su **Modifica proprietà**
1. Configurare i servizi **Lettura** e **Scrittura** per gli oggetti modello dati selezionati

   ![Configurare il servizio di lettura/scrittura](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. Configura gli argomenti del servizio:

   - Fai clic sull’icona di modifica per l’argomento Servizio di lettura
   - Associa l’argomento a un **attributo profilo utente**, **attributo richiesta** o **valore letterale**
   - Specifica il valore di binding (ad esempio, `petid` per un modulo di registrazione per animali domestici)

   ![Configurare l’argomento ID animale domestico](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. Fare clic su **Fine** per salvare l’argomento e su **Salva** per salvare FDM

   >[!NOTE]
   >
   > Ulteriori informazioni sulla configurazione dei servizi FDM in [Utilizzare il modello dati modulo (FDM)](/help/forms/work-with-form-data-model.md).

+++

+++Fase 2: creazione e configurazione del modulo adattivo

### Passaggio 3: creare un modulo adattivo

1. Passare a **Adobe Experience Manager** > **Moduli** > **Moduli e documenti**
1. Selezionare **Crea** > **Moduli adattivi**
1. Nella scheda **Origine**, seleziona un modello Edge Delivery Services:

   ![Modello di Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

1. Fare clic su **Crea** per aprire la procedura guidata **Crea modulo**

   >
   >
   > Puoi configurare l’origine dati dalla scheda **Dati** o successivamente modificando le proprietà del modulo.

1. Specificare i dettagli del modulo:

   - **Nome**: immettere un nome descrittivo per il modulo
   - **Titolo**: fornire un titolo intuitivo
   - **URL GitHub**: immettere l’URL dell’archivio (ad esempio, `https://github.com/wkndforms/edsforms`)

1. Fai clic su **Crea**

   ![Creare un modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

Il modulo viene aperto nell’editor universale per l’authoring.

### Passaggio 4: configurare l’origine dati modulo

1. Selezionare il modulo e fare clic su **Proprietà**

   ![Selezionare proprietà modulo](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. Aprire la scheda **Modello modulo**
3. Dal menu a discesa **Seleziona da**, scegliere **Modello dati modulo (FDM)**
4. Selezionare il modello dati modulo creato (ad esempio, AnimaleDomesticoFDM) dal menu a discesa

   ![Seleziona la scheda Modello del modulo](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. Fare clic su **Salva e chiudi**
6. Aprire il modulo per la modifica nell’editor universale

Gli elementi del modulo dal tuo FDM vengono visualizzati nella scheda **Origine dati** del **Browser contenuti**.

### Passaggio 5: aggiungere il binding dei dati ai campi modulo

1. Selezionare gli elementi dati dalla scheda **Origine dati**
2. Fare clic su **Aggiungi** o trascinare gli elementi per creare il modulo

   ![Schermata dell’editor universale che mostra il modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. Aggiungi il binding dei dati ai campi modulo:

   - Selezionare un campo modulo
   - Nel pannello **Proprietà**, individuare la proprietà **Riferimento binding**
   - Selezionare il riferimento di binding dei dati appropriato

     ![Binding dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++Fase 3: configurazione del servizio di precompilazione

### Passaggio 6: abilitare le estensioni richieste

Assicurati che queste estensioni siano abilitate nell’editor universale:

1. **Estensione proprietà AEM Form**

   - Aprire **Extension Manager** nell’editor universale
   - Abilitare l’estensione **Proprietà AEM Form**

   ![Icona proprietà modulo](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **Estensione origine dati**

   - Abilita l’estensione **Origine dati** se non visualizzi l’icona **Origini dati**

   ![Schermata dell’editor universale di Extension Manager](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > Per istruzioni dettagliate sulla gestione delle estensioni, consulta [Funzioni principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

### Passaggio 7: configurare il servizio di precompilazione

1. Apri il modulo adattivo nell’editor universale
2. Fai clic sull’icona dell’estensione **Proprietà AEM Form**

   ![Seleziona l’icona Proprietà modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. Fai clic sulla scheda **Precompila**
4. Seleziona **Servizio di precompilazione modello dati modulo**

   ![Seleziona il servizio di precompilazione](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. Fai clic su **Salva e chiudi**

+++

+++Fase 4: test della configurazione di precompilazione

### Passaggio 8: visualizzazione in anteprima e test

1. Passa a **Moduli** > **Moduli e documenti**
2. Selezionare il modulo adattivo
3. Scegli **Anteprima come HTML**
4. Testa la precompilazione aggiungendo i parametri all’URL:

   `https://your-preview-url.com?<bindreferencefield>=<value>`

   **Esempio:**

   https://your-preview-url.com?petid=12345

   ![Precompilare il modulo](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

Il modulo deve essere compilato automaticamente con dati basati sul parametro fornito.

+++

## Esempi

### Esempi di strutture di dati di precompilazione

**Esempio JSON per modulo basato su FDM:**

```
  {
    "afBoundData": {
      "user": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@example.com",
        "phone": "+1-555-0123"
      }
    },
    "afUnBoundData": {
      "additionalInfo": "User preferences loaded"
    }
  }
```

**Esempio XML per modulo basato su XFA:**

```
  <?xml version="1.0" encoding="UTF-8"?>
  <afData>
    <afBoundData>
      <user>
        <firstName>John</firstName>
        <lastName>Doe</lastName>
        <email>john.doe@example.com</email>
      </user>
    </afBoundData>
  </afData>
```

### Esempio di URL di precompilazione

Gli URL riportati di seguito hanno solo scopo illustrativo e non funzioneranno così come sono. Durante il test della funzionalità di precompilazione, sostituisci l’host e i parametri con quelli pertinenti per il tuo ambiente.

**Test di precompilazione di base:**

`https://preview.example.com/form.html?userId=12345`

**Test con più parametri:**

`https://preview.example.com/form.html?userId=12345&category=premium`


## Risoluzione di problemi

+++Problemi comuni e soluzioni

| Problema | Causa possibile | Soluzione |
|-------|----------------|----------|
| **I campi modulo non vengono precompilati** | Valori `bindRef` non corretti | Verifica che `bindRef` corrisponda esattamente ai nomi dei campi FDM |
| **Errori di formato dati** | Struttura dei dati non corrispondente | Assicurati che i dati precompilati corrispondano allo schema del modello del modulo |
| **Servizio non trovato** | Problemi di configurazione FDM | Verifica che i servizi FDM siano configurati e salvati correttamente |
| **Errori di autenticazione** | Connettività dell’origine dati | Verifica le credenziali dell’origine dati e la connettività |
| **Caricamento dati parziale** | Mappature campo mancanti | Assicurati che tutti i campi obbligatori abbiano associazioni di dati corrette |

+++

+++Passaggi per il debug

1. **Verificare la configurazione FDM:**

   - verifica se i servizi sono configurati correttamente
   - Testare i servizi FDM in modo indipendente
   - Convalidare la connettività dell’origine dati

2. **Verificare la configurazione del modulo:**

   - il modulo di conferma è associato a un FDM corretto
   - Verificare valori `bindRef` del campo
   - Testare prima il modulo senza precompilazione

3. **Testare il flusso di dati:**

   - utilizza gli strumenti di sviluppo del browser per controllare le richieste di rete
   - Verificare la presenza di errori JavaScript nella console
   - Convalidare il formato dei dati di risposta

4. **Messaggi di errore comuni:**

   - “Servizio di precompilazione non trovato”: verifica la configurazione del servizio
   - “Associazione dati non riuscita”: verifica la precisione di `bindRef`
   - “Formato dati non valido”: assicurati che i dati corrispondano allo schema

+++

## Best practice

+++Best practice di configurazione

- **Utilizzare una denominazione descrittiva**: assegna un nome chiaro ai FDM e ai servizi
- **Convalidare gli schemi dei dati**: verifica che la struttura dei dati corrisponda ai requisiti del modulo
- **Testare in modo incrementale**: configura e testa un campo alla volta
- **Mappature dei documenti**: tieni traccia delle mappature tra campi e dati

+++

+++Ottimizzazione delle prestazioni

- **Ridurre al minimo il volume di dati**: precompila solo i campi necessari
- **Utilizzare la memorizzazione nella cache**: configura la memorizzazione nella cache appropriata per i dati ad accesso frequente
- **Ottimizzare le query**: assicurati che le query del database siano efficienti
- **Monitoraggio delle prestazioni**: tieni traccia dei tempi di caricamento dei moduli con la precompilazione abilitata

+++

+++Considerazioni sulla sicurezza

- **Convalidare i parametri di input**: convalida sempre parametri URL
- **Sanificare i dati**: pulisci i dati prima di precompilare i moduli
- **Implementare i controlli di accesso**: assicurati che gli utenti possano accedere solo ai propri dati
- **Utilizzare HTTPS**: utilizza sempre connessioni sicure per la trasmissione dei dati

+++

+++Linee guida per l’esperienza utente

- **Fornire feedback**: mostra gli indicatori di caricamento durante il recupero dei dati
- **Gestire con criterio gli errori**: visualizza messaggi di errore utili
- **Consentire le sostituzioni**: consenti agli utenti di modificare i dati precompilati
- **Mantenere la coerenza**: utilizza un comportamento di precompilazione coerente nei moduli

+++

## Domande frequenti

+++Come posso testare se la precompilazione funziona correttamente?

Visualizza l’anteprima del modulo e aggiungi i parametri di precompilazione all’URL utilizzando questo formato: `?<bindreferencefield>=<value>`. Assicurati che il campo abbia un `bindRef` valido che corrisponda alla struttura dei dati. Utilizza gli strumenti di sviluppo del browser per controllare le richieste di rete e verifica che i dati vengano recuperati correttamente.

+++

+++Quali formati di dati sono supportati per la precompilazione dei moduli adattivi?

I moduli adattivi supportano più formati a seconda del modello di modulo:

- **Moduli XFA**: XML corrispondente allo schema XFA
- **Moduli con schema JSON**: dati JSON conformi allo schema
- **Moduli FDM**: JSON che mappa la struttura del modello di dati
- **Moduli con schema XML**: XML corrispondente alla struttura dello schema

+++

+++Posso precompilare sia i campi associati sia quelli non associati?

Sì, puoi precompilare entrambi i tipi di campi. I campi associati utilizzano la sezione `afBoundData` e devono corrispondere allo schema del modello del modulo. I campi non associati utilizzano la sezione `afUnBoundData` e possono contenere dati aggiuntivi.

+++

+++Cosa devo fare se solo alcuni campi vengono precompilati?

Verifica che tutti i campi abbiano valori `bindRef` corretti e che corrispondano esattamente al tuo FDM. Verifica che l’origine dati contenga tutti i campi obbligatori e che la struttura dati corrisponda allo schema del modello del modulo.

+++

+++Posso utilizzare più servizi di precompilazione in un unico modulo?

Puoi configurare un servizio di precompilazione principale per modulo. Tuttavia, per ottenere funzionalità simili, puoi combinare diverse origini dati all’interno di un singolo modello dati modulo.

+++

+++Come posso gestire l’autenticazione per i servizi di precompilazione?

L’autenticazione dipende dalla configurazione dell’origine dati. Per la precompilazione basata su FDM, configura l’autenticazione nelle impostazioni dell’origine dati. Per la precompilazione delle bozze, gli utenti in genere devono aver effettuato l’accesso per accedere alle bozze salvate.

+++



## Argomenti correlati

- [Integrare i moduli con il modello dati modulo nell’editor universale](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [Creare un modello dati modulo](/help/forms/create-form-data-models.md)
- [Utilizzare il modello dati modulo (FDM)](/help/forms/work-with-form-data-model.md)
- [Configurare le origini dati](/help/forms/configure-data-sources.md)
- [Guida introduttiva a Edge Delivery Services per AEM Forms.](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
