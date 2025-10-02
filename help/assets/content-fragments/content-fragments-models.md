---
title: Modelli per frammenti di contenuto (Assets - Frammenti di contenuto)
description: Scopri come i modelli per frammenti di contenuto fungono da base per i contenuti headless in AEM, consentendoti di creare frammenti di contenuto con contenuti strutturati.
exl-id: fd706c74-4cc1-426d-ab56-d1d1b521154b
feature: Content Fragments, GraphQL API
role: User, Admin, Architect
solution: Experience Manager Sites
source-git-commit: 8c9c51c349317250ddf7ef07e1b545860fd18351
workflow-type: tm+mt
source-wordcount: '3588'
ht-degree: 71%

---

# Modelli per frammenti di contenuto {#content-fragment-models}

I modelli per frammenti di contenuto in AEM definiscono la struttura del contenuto per i [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md), che fungono da base per i contenuti headless.

Per utilizzare i modelli di frammento di contenuto:

1. [Abilita la funzionalità modello Frammento di contenuto per un’istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Crea](#creating-a-content-fragment-model) e [configura](#defining-your-content-fragment-model) i modelli per frammenti di contenuto
1. [Abilitare i modelli di frammenti di contenuto](#enabling-disabling-a-content-fragment-model) da utilizzare per la creazione di frammenti di contenuto
1. [Consenti modelli di frammento di contenuto nelle cartelle Risorse richieste](#allowing-content-fragment-models-assets-folder) configurando i **Criteri**.

>[!NOTE]
>
>I frammenti di contenuto sono una funzione di Sites, ma vengono memorizzati come **Risorse**.
>
>I frammenti di contenuto e i modelli di frammenti di contenuto ora sono gestiti principalmente con la console **[Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, anche se i frammenti di contenuto possono ancora essere gestiti dalla console **Assets** e i modelli di frammenti di contenuto dalla console **Strumenti**. Questa sezione riguarda la gestione dalle console **Assets** e **Tools**.

>[!NOTE]
>
>Se è stato creato un modello con il [nuovo editor modelli](/help/sites-cloud/administering/content-fragments/content-fragment-models.md), utilizzare sempre tale editor per il modello.
>
>Se poi apri il modello con questo editor di modelli (originale), verrà visualizzato il messaggio:
>
>* &quot;Questo modello ha uno schema di interfaccia utente personalizzato configurato. L’ordine dei campi visualizzati in questa interfaccia utente potrebbe non corrispondere allo schema dell’interfaccia utente. Per visualizzare i campi allineati con lo schema dell’interfaccia utente, devi passare al nuovo Editor frammento di contenuto.&quot;

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.
1. Passa alla cartella appropriata per la [configurazione o configurazione secondaria](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Utilizza **Crea** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l’[utilizzo di modelli per frammenti di contenuto non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), l’opzione **Crea** non sarà disponibile.

1. Specifica il **titolo modello**.
Puoi anche definire varie proprietà; ad esempio, aggiungi **Tag**, **Descrizione** e seleziona **Abilita modello** per [abilitare il modello](#enabling-disabling-a-content-fragment-model), se necessario.

   >[!NOTE]
   >
   >Per informazioni dettagliate sul **Pattern URL di anteprima predefinito** vedi [Modello per frammenti di contenuto - Proprietà](#content-fragment-model-properties).

   ![titolo e descrizione](assets/cfm-models-02.png)

1. Utilizza **Crea** per salvare il modello vuoto. Un messaggio indica il successo dell’azione: puoi selezionare **Apri** per modificare immediatamente il modello, oppure **Fine** per tornare alla console.

## Definizione del modello per frammenti di contenuto {#defining-your-content-fragment-model}

Il modello per frammenti di contenuto definisce efficacemente la struttura dei frammenti di contenuto risultanti utilizzando una selezione di **[Tipi di dati](#data-types)**. Utilizzando l’editor modelli è possibile aggiungere istanze dei tipi di dati, quindi configurarle per creare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello per frammento di contenuto esistente può avere un impatto sui frammenti dipendenti.

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello per frammenti di contenuto.
1. Apri il modello che desideri **modificare** utilizzando l’azione rapida oppure selezionando il modello e quindi l’azione dalla barra degli strumenti.

   Una volta aperto, l’editor modelli mostra:

   * a sinistra: campi già definiti
   * a destra: **Tipi di dati** disponibili per la creazione di campi, oltre alle **Proprietà** da utilizzare dopo la creazione
   * top: opzione per provare il [nuovo editor](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

   >[!NOTE]
   >
   >Quando un campo è **obbligatorio**, l’**Etichetta** indicata nel riquadro a sinistra è contrassegnata da un asterisco (**&#42;**).

![proprietà](assets/cfm-models-03.png)

1. **Per aggiungere un campo**

   * Trascina un tipo di dati obbligatorio nella posizione desiderata per un campo:

     ![tipo di dati per il campo](assets/cfm-models-04.png)

   * Una volta aggiunto un campo al modello, il pannello di destra visualizza le **Proprietà** che possono essere definite per quel particolare tipo di dati. Qui puoi definire ciò che è necessario per quel campo.

      * Molte proprietà sono auto-esplicative, per ulteriori dettagli vedi [Proprietà](#properties).
      * La digitazione di un’**Etichetta campo** completerà automaticamente il **Nome proprietà**. Se vuoto, può essere aggiornato manualmente in seguito.

        >[!CAUTION]
        >
        >Quando aggiorni manualmente la proprietà **Nome proprietà** per un tipo di dati, tieni presente che i nomi devono contenere solo caratteri A-Z, a-z, 0-9 e il carattere speciale di sottolineatura “_”.
        >
        >Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

     Esempio:

     ![proprietà del campo](assets/cfm-models-05.png)

1. **Per rimuovere un campo**

   Seleziona il campo richiesto, quindi seleziona l’icona del cestino. Viene richiesto di confermare l’azione.

   ![rimuovere](assets/cfm-models-06.png)

1. Aggiungi tutti i campi obbligatori e definisci le relative proprietà in base alle esigenze. Esempio:

   ![salva](assets/cfm-models-07.png)

1. Seleziona **Salva** per mantenere la definizione.

## Tipi di dati {#data-types}

Per definire il modello è disponibile una selezione di tipi di dati:

* **Testo su riga singola**
   * Aggiungi un campo per una singola riga di testo; è possibile definire la lunghezza massima
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo

* **Testo su più righe**
   * Area di testo che può essere RTF, Testo normale o Markdown
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo

  >[!NOTE]
  >
  >Se l&#39;area di testo è RTF, Testo normale o Markdown, è definito nel modello dalla proprietà **Tipo predefinito**.
  >
  >Questo formato non può essere modificato dall&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md), ma solo dal modello.

* **Numero**
   * Aggiungere un campo numerico
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo

* **Booleano**
   * Aggiungi una casella di controllo booleana

* **Data e ora**
   * Aggiungere un campo data e/o ora

* **Enumerazione**
   * Aggiungere un set di campi Casella di controllo, Pulsante di scelta o A discesa
      * Puoi specificare le opzioni disponibili per l’autore del frammento

* **Tag**
   * Consente agli autori di frammenti di accedere alle aree dei tag e di selezionarle

* **Riferimento frammento**
   * I riferimenti ad altri frammenti di contenuto possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
      * Modificare direttamente il frammento a cui si fa riferimento.
      * Creare un nuovo frammento di contenuto basato sul modello appropriato
      * Crea nuove istanze del campo
   * Il riferimento specifica il percorso della risorsa di riferimento, ad esempio `/content/dam/path/to/resource`

* **Riferimento frammento (UUID)**
   * I riferimenti ad altri frammenti di contenuto possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
      * Modificare direttamente il frammento a cui si fa riferimento.
      * Creare un nuovo frammento di contenuto basato sul modello appropriato
      * Crea nuove istanze del campo
   * Nell’editor i riferimenti specificano il percorso della risorsa a cui si fa riferimento; internamente tali riferimenti vengono considerati come ID universalmente univoci (UUID) che fanno riferimento alla risorsa.
      * Non è necessario conoscere l’UUID; nell’editor frammenti puoi individuare il frammento richiesto

  >[!NOTE]
  >
  >Gli UUID sono specifici dell’archivio. Se si utilizza lo strumento [Copia contenuto](/help/implementing/developing/tools/content-copy.md) per copiare frammenti di contenuto, gli UUID verranno ricalcolati nell&#39;ambiente di destinazione.

* **Riferimento contenuto**
   * I riferimenti ad altri contenuti di qualsiasi tipo possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Se si fa riferimento a un’immagine, è possibile scegliere di mostrare una miniatura
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo
   * Il riferimento specifica il percorso della risorsa di riferimento, ad esempio `/content/dam/path/to/resource`

* **Riferimento contenuto (UUID)**
   * I riferimenti ad altri contenuti di qualsiasi tipo possono essere utilizzati per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Se si fa riferimento a un’immagine, è possibile scegliere di mostrare una miniatura
   * Il campo può essere configurato per consentire agli autori di frammenti di creare nuove istanze del campo
   * Nell’editor i riferimenti specificano il percorso della risorsa a cui si fa riferimento; internamente tali riferimenti vengono considerati come ID universalmente univoci (UUID) che fanno riferimento alla risorsa.
      * Non è necessario conoscere l’UUID; nell’editor frammenti puoi individuare la risorsa richiesta

  >[!NOTE]
  >
  >Gli UUID sono specifici dell’archivio. Se si utilizza lo strumento [Copia contenuto](/help/implementing/developing/tools/content-copy.md) per copiare frammenti di contenuto, gli UUID verranno ricalcolati nell&#39;ambiente di destinazione.

* **Oggetto JSON**
   * Consente all’autore del frammento di contenuto di immettere la sintassi JSON negli elementi corrispondenti di un frammento.
      * Questo fa sì che AEM possa memorizzare direttamente JSON con copia e incolla da un altro servizio.
      * Il codice JSON viene trasmesso e riprodotto come codice JSON in GraphQL.
      * Include le funzioni di evidenziazione della sintassi JSON, completamento automatico ed evidenziazione degli errori nell’editor dei frammenti di contenuto.

* **Segnaposto scheda**
   * Consente l’introduzione di schede da utilizzare per la modifica del contenuto di Frammenti di contenuto.
      * Vengono visualizzati come divisori nell’editor modelli, separando le sezioni dell’elenco dei tipi di dati di contenuto. Ogni istanza rappresenta l’inizio di una nuova scheda.
      * Nell’editor frammenti ogni istanza viene visualizzata come una scheda.

     >[!NOTE]
     >
     >Questo tipo di dati viene utilizzato esclusivamente per la formattazione e viene ignorato dallo schema GraphQL AEM.

## Proprietà {#properties}

Molte proprietà sono auto-esplicative, qui sotto ulteriori dettagli per alcune proprietà:

* **Nome proprietà**

  Quando aggiorni manualmente questa proprietà per un tipo di dati, tieni presente che i nomi **devono** contenere *solo* caratteri A-Z, a-z, 0-9 e il carattere speciale di sottolineatura “_“.

  >[!CAUTION]
  >
  >Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

* **Rendering come** 
Sono disponibili varie opzioni per realizzare o riprodurre il campo in un frammento. Spesso questa proprietà ti consente di definire se l’autore vede una singola istanza del campo o se può creare più istanze. Quando si utilizza **Campo multiplo** è possibile definire il numero minimo e massimo di elementi. Per ulteriori dettagli, vedere [Convalida](#validation).

* **Etichetta campo**
L&#39;immissione di un **Etichetta campo** genererà automaticamente un **Nome proprietà**, che può quindi essere aggiornato manualmente, se necessario.

* **Convalida**
La convalida di base è disponibile tramite meccanismi quali la proprietà **Obbligatorio**. Alcuni tipi di dati dispongono di campi di convalida aggiuntivi. Vedi [Convalida](#validation) per ulteriori dettagli.

* Per il tipo di dati **Testo su più righe** è possibile definire il **Tipo predefinito** come:

   * **Formato RTF**
   * **Markdown**
   * **Testo normale**

  Se non viene specificato diversamente, per questo campo viene utilizzato il valore predefinito **Rich Text**.

  La modifica del **Tipo predefinito** in un modello per frammenti di contenuto avrà effetto solo su un frammento esistente correlato, una volta che il frammento è stato aperto nell’editor e successivamente salvato.

* **Univoco**
Il contenuto (per il campo specifico) deve essere univoco in tutti i frammenti di contenuto creati dal modello corrente.

  Questo viene utilizzato per impedire agli autori di contenuti di ripetere contenuti già aggiunti in un altro frammento dello stesso modello.

  Ad esempio, un campo **Testo a riga singola** denominato `Country` nel modello per frammenti di contenuto non può avere il valore `Japan` in due frammenti di contenuto dipendenti. Viene visualizzato un avviso quando si tenta di eseguire la seconda istanza.

  >[!NOTE]
  >
  >L’unicità è assicurata da directory principale lingua.

  >[!NOTE]
  >
  >Le varianti possono avere lo stesso valore *unico* come varianti dello stesso frammento, ma non lo stesso valore utilizzato in qualsiasi variante di altri frammenti.

  >[!CAUTION]
  >
  >Se desideri utilizzare MSM (che crea copie dei frammenti di contenuto), tutti i vincoli **Unique** devono essere rimossi da qualsiasi tipo di dati utilizzato nei rispettivi modelli per frammenti di contenuto.

* Vedi **[Riferimento contenuto](#content-reference)** per ulteriori dettagli su quel tipo di dati specifico e sulle relative proprietà.

* Vedi **[Riferimento frammento (frammenti nidificati)](#fragment-reference-nested-fragments)** per ulteriori dettagli su quel tipo di dati specifico e sulle relative proprietà.

* **Traducibile**

  Selezionando la casella di controllo **Traducibile** in un campo dell’editor modelli di frammenti di contenuto:

   * Fa sì che il nome della proprietà del campo sia aggiunto alla configurazione di traduzione, al contesto `/content/dam/<sites-configuration>`, se non già presente.
   * Per GraphQL: impostare una proprietà `<translatable>` nel campo Frammento di contenuto su `yes`, per consentire al filtro query GraphQL di restituire output JSON con solo contenuto traducibile.

## Convalida {#validation}

Diversi tipi di dati includono ora la possibilità di definire requisiti di convalida per l’immissione di contenuto nel frammento risultante:

* **Testo su riga singola**
   * Confronta con un regex predefinito.
* **Numero**
   * Verifica la presenza di valori specifici.
* **Riferimento contenuto**
   * Controlla tipi specifici di contenuto.
   * È possibile fare riferimento solo alle risorse di dimensioni file specificate o inferiori.
   * È possibile fare riferimento solo alle immagini entro un intervallo di larghezza e/o altezza predefinito (in pixel).
* **Riferimento frammento**
   * Verifica un modello di frammento di contenuto specifico.
* **Numero minimo di elementi** / **Numero massimo di elementi**

  I campi definiti come **Campo multiplo** (impostati con **Rendering come**) dispongono delle opzioni seguenti:

   * **Numero minimo di elementi**
   * **Numero massimo di elementi**

  Questi vengono convalidati:

   * Il valore massimo viene convalidato nell&#39;[Editor frammento di contenuto originale](/help/assets/content-fragments/content-fragments-variations.md).
   * Entrambi sono convalidati nell&#39;[Editor frammento di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md).

## Utilizzo di riferimenti per creare contenuti nidificati {#using-references-to-form-nested-content}

I frammenti di contenuto possono formare contenuto nidificato utilizzando uno dei seguenti tipi di dati:

* [Riferimento contenuto](#content-reference)
   * Fornisce un semplice riferimento ad altri contenuti; di qualsiasi tipo.
   * Forniti dai tipi di dati:
      * **Riferimento contenuto** - basato su percorso
      * **Riferimento contenuto (UUID)** - basato su UUID
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

* [Riferimento frammento](#fragment-reference-nested-fragments) (frammenti nidificati)
   * Fa riferimento ad altri frammenti, a seconda dei modelli specifici indicati.
   * Forniti dai tipi di dati:
      * **Riferimento frammento** - basato su percorso
      * **Riferimento frammento (UUID)** - basato su UUID
   * Consente di includere/recuperare dati strutturati.

     >[!NOTE]
     >
     >Questo metodo è particolarmente interessante quando si utilizza [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

>[!NOTE]
>
>Consulta [Aggiornare i frammenti di contenuto per i riferimenti UUID](/help/headless/graphql-api/uuid-reference-upgrade.md) per ulteriori informazioni su contenuto/riferimento frammento e riferimento contenuto/riferimento frammento (UUID) e per l&#39;aggiornamento ai tipi di dati basati su UUID.

>[!NOTE]
>
>AEM ha una protezione di ricorrenze per:
>
>* Riferimenti contenuto
>  &#x200B;>  Questo impedisce all’utente di aggiungere un riferimento al frammento corrente. Inoltre la finestra di dialogo selettore del riferimento frammento può risultare vuota.
>
>* Riferimenti frammento in GraphQL
>  &#x200B;>  Se crei una query approfondita che restituisce più frammenti di contenuto a cui fanno riferimento l’un l’altro, alla prima occorrenza restituirà null.

### Riferimento contenuto {#content-reference}

I tipi di dati **Riferimento contenuto** e **Riferimento contenuto (UUID)** consentono di eseguire il rendering del contenuto da un&#39;altra origine, ad esempio immagine, pagina o frammento di esperienza.

Oltre alle proprietà standard puoi specificare:

* Il **Percorso directory principale** per qualsiasi contenuto a cui si fa riferimento
* I tipi di contenuto a cui è possibile fare riferimento
* Le limitazioni per le dimensioni dei file
* Se si fa riferimento a un’immagine:
   * Mostra miniatura
   * Limiti di altezza e larghezza dell’immagine

![Riferimento contenuto](assets/cfm-content-reference.png)

### Riferimento frammento (frammenti nidificati) {#fragment-reference-nested-fragments}

I tipi di dati **Riferimento frammento** e **Riferimento frammento (UUID)** possono fare riferimento a uno o più frammenti di contenuto. Questa funzione è particolarmente interessante per il recupero dei contenuti da utilizzare nell’app, in quanto consente di recuperare dati strutturati con più livelli.

Esempio:

* Un modello che definisce i dettagli di un dipendente, tra cui:
   * Un riferimento al modello che definisce il datore di lavoro (azienda)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>Ciò è di particolare interesse in combinazione con [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Oltre alle proprietà standard puoi definire:

* **Rendering come**:

   * **multifield**: l’autore del frammento può creare più riferimenti individuali

   * **fragmentreference**: consente all’autore del frammento di selezionare un singolo riferimento a un frammento

* **Tipo di modello**
È possibile selezionare più modelli. Durante l’authoring del frammento di contenuto, tutti i frammenti a cui si fa riferimento devono essere stati creati utilizzando questi modelli.

* **Percorso radice**

Specifica un percorso radice per tutti i frammenti a cui si fa riferimento.

* **Consenti creazione di frammenti**

  Questo consente all’autore del frammento di creare un frammento basato sul modello appropriato.

   * **fragmentreferencecomposite**: consente all’autore del frammento di creare un elemento composito selezionando più frammenti

  ![Riferimento frammento](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>È presente un meccanismo di protezione per evitare le ricorrenze. Non consente all’utente di selezionare il frammento di contenuto corrente nel riferimento frammento. Inoltre la finestra di dialogo selettore del riferimento frammento può risultare vuota.
>
>In GraphQL è inoltre disponibile una protezione di ricorrenza per i riferimenti di frammenti. Se crei una query approfondita tra due frammenti di contenuto con riferimento l’uno all’altro, verrà restituito null.

## Modello per frammenti di contenuto - Proprietà {#content-fragment-model-properties}

Puoi modificare le **Proprietà** di un modello per frammenti di contenuto:

* **Base**
   * **Titolo modello**
   * **Tag**
   * **Descrizione**
   * **Carica immagine**
   * **Pattern URL anteprima predefinito**

     >[!NOTE]
     >
     >Utilizzato solo dall&#39;*new* Editor frammento di contenuto. Per ulteriori informazioni, vedere [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties).


## Abilitazione o disabilitazione di un modello per frammenti di contenuto {#enabling-disabling-a-content-fragment-model}

I modelli per frammenti di contenuto dispongono di uno stato che puoi impostare per avere il controllo completo del loro utilizzo.

### Abilitazione di un modello per frammenti di contenuto {#enabling-a-content-fragment-model}

Quando viene creato un modello, questo deve essere abilitato in modo che:

* Può essere selezionato quando si crea un frammento di contenuto.
* Possibilità di utilizzarlo come riferimento all’interno di un modello per frammento di contenuto
* Possibilità di utilizzarlo in GraphQL, affinché venga generato lo schema

Per abilitare un modello contrassegnato come:

* **Bozza**: nuovo (mai abilitato)
* **Disabilitato**: che è stato specificamente disabilitato

puoi utilizzare l’opzione **Abilita** dalle seguenti aree:

* Dalla barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Con l’azione rapida corrispondente (passando il mouse sul modello richiesto).

![Abilitare un modello in stato Bozza o Disabilitato](assets/cfm-status-enable.png)

### Disabilitazione di un modello per frammenti di contenuto {#disabling-a-content-fragment-model}

Un modello può anche essere disabilitato, con i seguenti risultati:

* Il modello non sarà più disponibile come base per la creazione di *nuovi* frammenti di contenuto.
* Tuttavia:
   * Lo schema GraphQL continua a essere generato ed è ancora interrogabile (per evitare di influenzare l’API JSON).
   * È comunque possibile eseguire query su qualsiasi frammento di contenuto basato sul modello e restituirlo dall’endpoint GraphQL.
* Non è più possibile fare riferimento al modello, ma i riferimenti esistenti vengono mantenuti intatti e possono ancora essere interrogati e restituiti dall’endpoint GraphQL.

Per disattivare un modello contrassegnato come **Abilitato** si utilizza l’opzione **Disattiva** selezionabile:

* Dalla barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Con l’azione rapida corrispondente (passando il mouse sul modello richiesto).

![Disattivare un modello abilitato](assets/cfm-status-disable.png)

## Consentire modelli per frammenti di contenuto nella cartella delle risorse {#allowing-content-fragment-models-assets-folder}

Per implementare la governance dei contenuti, puoi configurare dei **Criteri** nella cartella Risorse per controllare quali modelli per frammenti di contenuto sono consentiti per la creazione di frammenti in tale cartella.

>[!NOTE]
>
>Il meccanismo è simile a [consentire modelli di pagina](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) per una pagina e i relativi elementi secondari, nelle proprietà avanzate di una pagina.

Per configurare i **Criteri** dei **Modelli per frammenti di contenuto consentiti**:

1. Naviga e apri **Proprietà** per la cartella Risorse desiderata.

1. Apri la scheda **Criteri**, dove puoi configurare:

   * **Ereditato da`<folder>`**

     I criteri vengono ereditati automaticamente durante la creazione di nuove cartelle secondarie; il criterio può essere riconfigurato (interrompendo l’ereditarietà) se le sottocartelle devono consentire modelli diversi dalla cartella principale.

   * **Modelli per frammenti di contenuto consentiti per percorso**

     Possono essere consentiti più modelli.

   * **Modelli per frammenti di contenuto consentiti per tag**

     Possono essere consentiti più modelli.

   ![Criterio del modello per frammento di contenuto](assets/cfm-model-policy-assets-folder.png)

1. **Salva** eventuali modifiche.

I modelli per frammenti di contenuto consentiti per una cartella vengono risolti come segue:

* I **Criteri** dei **Modelli per frammenti di contenuto consentiti**.
* Se vuoto, prova a determinare il criterio utilizzando le regole di ereditarietà.
* Se la catena di ereditarietà non fornisce un risultato, consulta la sezione Configurazione di **Servizi cloud** per quella cartella (anche prima direttamente e poi tramite ereditarietà).
* Se nessuno dei risultati di cui sopra fornisce risultati, allora non ci sono modelli consentiti per quella cartella.

## Eliminazione di un modello per frammenti di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>L’eliminazione di un modello per frammenti di contenuto può avere un impatto sui frammenti dipendenti.

Per eliminare un modello per frammenti di contenuto:

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello per frammenti di contenuto.
1. Seleziona il modello e poi **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   >
   >Se ci sono riferimenti al modello, viene visualizzata un’avvertenza. Agisci di conseguenza.

## Pubblicazione di un modello per frammenti di contenuto {#publishing-a-content-fragment-model}

I modelli per frammenti di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

Per pubblicare un modello per frammenti di contenuto:

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello per frammenti di contenuto.
1. Seleziona il modello e poi **Pubblica** dalla barra degli strumenti.
Lo stato di pubblicazione viene indicato nella console.

   >[!NOTE]
   >
   >Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, questo viene segnalato in un elenco di selezione e il modello viene pubblicato con il frammento.

## Annullamento della pubblicazione di un modello per frammenti di contenuto {#unpublishing-a-content-fragment-model}

Si può annullare la pubblicazione di modelli per frammenti di contenuto che non sono referenziati da alcun frammento.

Per annullare la pubblicazione di un modello per frammenti di contenuto:

1. Passa a **Strumenti**, **Generale**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello per frammenti di contenuto.
1. Seleziona il modello e poi **Annulla pubblicazione** dalla barra degli strumenti.
Lo stato di pubblicazione viene indicato nella console.

Se tenti di annullare la pubblicazione di un modello attualmente utilizzato da uno o più frammenti, un avviso di errore segnala quanto segue:

![Messaggio di errore di modello per frammenti di contenuto quando si annulla la pubblicazione di un modello in uso](assets/cfm-model-unpublish-error.png)

Il messaggio suggerirà di controllare il pannello [Riferimenti](/help/sites-cloud/authoring/basic-handling.md#references) per approfondire l’analisi:

![Modello per frammenti di contenuto nei riferimenti](assets/cfm-model-references.png)

## Modelli per frammenti di contenuto bloccati (pubblicati) {#locked-published-content-fragment-models}

Questa funzione garantisce la governance dei modelli per frammenti di contenuto pubblicati.

### La sfida {#the-challenge}

* I modelli per frammenti di contenuto determinano lo schema per le query GraphQL in AEM.

   * Gli schemi GraphQL AEM vengono creati non appena viene creato un modello per frammenti di contenuto e possono esistere sia nell’ambiente di creazione che in quello di pubblicazione.

   * Gli schemi in fase di pubblicazione sono i più critici in quanto forniscono le basi per la consegna live di contenuti di frammenti di contenuto in formato JSON.

* Possono verificarsi problemi quando i modelli per frammenti di contenuto vengono modificati o in altre parole modificate. Ciò significa che lo schema cambia, e questo può di conseguenza influenzare le query GraphQL esistenti.

* L’aggiunta di nuovi campi a un modello per frammenti di contenuto non dovrebbe avere effetti negativi, in genere. Tuttavia, la modifica dei campi dati esistenti (ad esempio il nome) o l’eliminazione delle definizioni dei campi interromperà le query GraphQL esistenti quando richiedono questi campi.

### Requisiti {#the-requirements}

* Sensibilizzare gli utenti sui rischi derivanti dalla modifica di modelli già utilizzati per la distribuzione di contenuti live, in altre parole, di modelli pubblicati.

* Inoltre, per evitare modifiche non desiderate.

Una di queste potrebbe interrompere le query se i modelli modificati vengono ripubblicati.

### Soluzione {#the-solution}

Per risolvere questi problemi, i modelli di frammento di contenuto sono *bloccati* in modalità di SOLA LETTURA su autore, non appena sono stati pubblicati. Questo stato è indicato con **Bloccato**:

![Scheda del modello per frammenti di contenuto bloccato](assets/cfm-model-locked.png)

Quando il modello è **Bloccato** (in modalità di SOLA LETTURA), è possibile visualizzare il contenuto e la struttura dei modelli, ma non è possibile modificarli.

Puoi gestire i modelli **Bloccati** dalla console o dall’editor modelli:

* Console

  Dalla console, è possibile gestire la modalità SOLA LETTURA con le azioni **Sblocca** e **Blocca** nella barra degli strumenti:

  ![Barra degli strumenti del modello per frammenti di contenuto bloccato](assets/cfm-model-locked.png)

   * È possibile **Sbloccare** un modello per abilitare le modifiche.

     Se selezioni **Sblocca** viene mostrata un’avvertenza in cui ti si chiede di confermare l’azione **Sblocca**:
     ![Messaggio relativo allo sblocco del modello per frammenti di contenuto](assets/cfm-model-unlock-message.png)

     Puoi quindi aprire il modello per la modifica.

   * Puoi anche **Bloccare** successivamente il modello.
   * La ripubblicazione del modello lo rimette immediatamente in modalità **Bloccato** (SOLA LETTURA).

* Editor modelli

   * Quando apri un modello bloccato, viene visualizzato un avviso con tre possibili azioni: **Annulla**, **Visualizza sola lettura**, **Modifica**:

     ![Messaggio relativo alla visualizzazione di un modello per frammenti di contenuto bloccato](assets/cfm-model-editor-lock-message.png)

   * Se selezioni **Visualizza sola lettura** puoi visualizzare il contenuto e la struttura del modello:

     ![Visualizza solo lettura: modello per frammenti di contenuto bloccato](assets/cfm-model-editor-locked-view-only.png)

   * Se selezioni **Modifica** puoi modificare e salvare gli aggiornamenti:

     ![Modifica: modello per frammenti di contenuto bloccato](assets/cfm-model-editor-locked-edit.png)

     >[!NOTE]
     >
     >Potrebbe ancora essere presente un avviso nella parte superiore, ma si verifica quando il modello è già utilizzato da frammenti di contenuto esistenti.

   * **Annulla** ti riporterà alla console.
