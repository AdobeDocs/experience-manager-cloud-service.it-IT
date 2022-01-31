---
title: 'Problemi noti '
description: Best practice e limitazioni relative alle comunicazioni
source-git-commit: c38a34519822449ff2577a9474b1294d5d45d3ae
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# Considerazioni sui problemi noti e sulle best practice {#best-practices-known-issues-and-limitations}

Prima di iniziare a utilizzare le API di comunicazione, esamina le considerazioni seguenti, i problemi noti e le domande frequenti:

## Considerazioni  {#considerations-for-communications-apis}

### Dati modulo {#form-data}

Le API di comunicazione accettano come input sia una struttura del modulo generalmente creata in Designer che i dati del modulo XML. Per compilare un documento con i dati, nei dati del modulo XML deve esistere un elemento XML per ogni campo del modulo che si desidera compilare. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Non è necessario stabilire una corrispondenza con l’ordine di visualizzazione degli elementi XML. Il fattore importante è che gli elementi XML sono specificati con i valori corrispondenti.

Prendi in considerazione il seguente modulo di richiesta di prestito:

![Modulo di domanda di prestito](assets/loanFormData.png)

Per unire i dati alla struttura del modulo, creare un’origine dati XML corrispondente al modulo. L&#39;XML seguente rappresenta un&#39;origine dati XML corrispondente al modulo di applicazione per l&#39;ipoteca di esempio.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    - <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### Tipi di documenti supportati {#supported-document-types}

Per un accesso completo alle funzionalità di rendering delle API di comunicazione, si consiglia di utilizzare un file XDP come input. A volte è possibile utilizzare un file PDF. Tuttavia, l’utilizzo di un file PDF come input presenta alcune limitazioni:

Un documento PDF che non contiene un flusso XFA non può essere rappresentato come PostScript, PCL o ZPL. Le API di comunicazione possono eseguire il rendering dei documenti PDF con flussi XFA (ovvero moduli creati in Designer) in formati laser ed etichette. Se il documento PDF è firmato, certificato o contiene diritti di utilizzo (applicati utilizzando il servizio AEM Forms Reader Extensions), non può essere sottoposto a rendering in questi formati di stampa.


### Aree stampabili {#printable-areas}

Il margine non stampabile predefinito da 0,25&quot; non è esatto per le stampanti di etichette e varia dalla stampante alla stampante e dalle dimensioni dell&#39;etichetta alle dimensioni dell&#39;etichetta, tuttavia, si consiglia di mantenere il margine di 0,25&quot; o ridurlo. Tuttavia, si consiglia di non aumentare il margine non stampabile. In caso contrario, le informazioni contenute nell&#39;area stampabile non vengono stampate correttamente.

Assicurarsi sempre di utilizzare il file XDC corretto per la stampante. Ad esempio, evitare di scegliere un file XDC per una stampante a 300 dpi e inviare il documento a una stampante a 200 dpi.

### Script solo per i moduli XFA (XDP/PDF) {#scripts}

Una struttura del modulo utilizzata con le API di comunicazione può contenere script eseguiti sul server. Assicurarsi che una struttura del modulo non contenga script eseguiti sul client. Per informazioni sulla creazione degli script di struttura del modulo, vedere [Guida di Designer](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### Mappatura dei font {#font-mapping}

Per progettare un modulo che utilizza font residenti nella stampante, scegliere un nome di font corrispondente ai font disponibili nella stampante in Designer. Un elenco di font supportati per PCL o PostScript si trova nei corrispondenti profili dispositivo (file XDC). In alternativa, è possibile creare la mappatura dei font per associare i font non residenti nella stampante ai font residenti nella stampante con un nome di font diverso. Ad esempio, in uno scenario PostScript, i riferimenti al carattere Arial® possono essere mappati al carattere Helvetica® residente nella stampante.

Se un font è installato in un computer client, è disponibile nell’elenco a discesa in Designer. Se il font non è installato, è necessario specificare manualmente il nome del font. L’opzione &quot;Sostituisci definitivamente font non disponibili&quot; in Designer può essere disattivata. In caso contrario, quando il file XDP viene salvato in Designer, il nome del font sostitutivo viene scritto nel file XDP. Ciò significa che il font residente nella stampante non viene utilizzato.

Esistono due tipi di font OpenType®. Un tipo è un font TrueType OpenType® supportato da PCL. L&#39;altro è CFF OpenType®. L&#39;output PDF e PostScript supporta i font incorporati Type-1, TrueType e OpenType®. L&#39;output PCL supporta i font TrueType incorporati.

I font Type-1 e OpenType® non sono incorporati nell&#39;output PCL. Il contenuto formattato con font Type-1 e OpenType® viene rasterizzato e generato come immagine bitmap di grandi dimensioni e più lento da generare.

I font scaricati o incorporati vengono sostituiti automaticamente durante la generazione dell’output PostScript, PCL o PDF. Ciò significa che solo il sottoinsieme dei glifi di font necessari per il corretto rendering del documento generato è incluso nell’output generato.

### Utilizzo dei file di profilo del dispositivo (file XDC) {#working-with-xdc-files}

Un profilo dispositivo (file XDC) è un file di descrizione della stampante in formato XML. Questo file consente alle API di comunicazione di inviare i documenti come formati laser o di stampa delle etichette. Le API di comunicazione utilizzano i file XDC, tra cui:

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

È possibile utilizzare i file XDC forniti per generare documenti di stampa o modificarli in base alle proprie esigenze.
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

Questi file sono file XDC di riferimento che supportano le caratteristiche di stampanti specifiche, ad esempio font residenti, vassoi di carta e graffette. Lo scopo di questo riferimento è quello di aiutarti a capire come impostare le tue stampanti utilizzando i profili dei dispositivi. Il riferimento è anche un punto di partenza per stampanti simili della stessa linea di prodotti.

### Utilizzo del file di configurazione XCI {#working-with-xci-files}

Le API di comunicazione utilizzano un file di configurazione XCI per eseguire attività quali controllare se l’output è un singolo pannello o impaginato. Anche se questo file contiene impostazioni che possono essere impostate, non è tipico modificare questo valore. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Puoi trasmettere un file XCI modificato mentre utilizzi un’API di comunicazione. In questo modo, crea una copia del file predefinito, modifica solo i valori che richiedono modifiche per soddisfare i requisiti aziendali e utilizza il file XCI modificato.

Le API di comunicazione iniziano con il file XCI predefinito (o il file modificato). Quindi applica i valori specificati utilizzando le API di comunicazione. Questi valori sostituiscono le impostazioni XCI.

La tabella seguente specifica le opzioni XCI.

| Opzione XCI | Descrizione |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/current/pdf/creator | Identifica il creatore del documento utilizzando la voce Creatore nel dizionario Informazioni documento. Per informazioni su questo dizionario, consultare la guida di riferimento di PDF. |
| config/present/pdf/produttore | Identifica il produttore del documento utilizzando la voce Produttore nel dizionario Informazioni documento. Per informazioni su questo dizionario, consultare la guida di riferimento di PDF. |
| configurazione/attuale/layout | Controlla se l&#39;output è un singolo pannello o impaginato. |
| config/current/pdf/compressione/level | Specifica il grado di compressione da utilizzare per la generazione di un documento PDF. |
| config/current/pdf/scriptModel | Controlla se le informazioni specifiche di XFA sono incluse nel documento PDF di output. |
| config/current/common/data/adjustData | Controlla se l&#39;applicazione XFA regola i dati dopo l&#39;unione. |
| config/current/pdf/renderPolicy | Controlla se la generazione del contenuto della pagina viene eseguita sul server o differita al client. |
| config/present/common/locale | Specifica le impostazioni internazionali predefinite utilizzate nel documento di output. |
| configurazione/presente/destinazione | Se contenuto da un elemento presente, specifica il formato di output. Se contenuto in un elemento openAction, specifica l&#39;azione da eseguire all&#39;apertura del documento in un client interattivo. |
| configurazione/attuale/uscita/tipo | Specifica il tipo di compressione da applicare a un file o il tipo di output da produrre. |
| config/current/common/temp/uri | Specifica l’URI del modulo. |
| config/present/common/template/base | Fornisce una posizione di base per gli URI nella struttura del modulo. Quando questo elemento è assente o vuoto, la posizione della struttura del modulo viene utilizzata come base. |
| config/present/common/log/to | Controlla la posizione in cui vengono scritti i dati di registro o di output. |
| config/current/output/to | Controlla la posizione in cui vengono scritti i dati di registro o di output. |
| config/present/script/currentPage | Specifica la pagina iniziale all&#39;apertura del documento. |
| config/present/script/exclude | Indica alle API server/comunicazioni di AEM Forms gli eventi da ignorare. |
| config/current/pdf/linearized | Controlla se il documento PDF di output è linearizzato. |
| config/present/script/runScripts | Controlla quale insieme di script viene eseguito da AEM Forms. |
| config/present/pdf/tagged | Controlla l’inclusione dei tag nel documento PDF di output. I tag, nel contesto di PDF, sono informazioni aggiuntive incluse in un documento per esporre la struttura logica del documento. I tag facilitano gli strumenti di accessibilità e la riformattazione. Ad esempio, un numero di pagina può essere contrassegnato come artefatto in modo che l’assistente vocale non lo pronunci al centro del testo. Anche se i tag rendono un documento più utile, aumentano anche le dimensioni del documento e il tempo di elaborazione necessario per crearlo. |
| config/present/pdf/version | Specifica la versione del documento PDF da generare. |


## Problemi noti

* È possibile utilizzare un tipo di rendering specifico (PDF, STAMPA) una sola volta nell&#39;elenco delle opzioni di stampa. Ad esempio, non è possibile avere due opzioni PRINT ciascuna che specificano un tipo di rendering PCL.

* Per una configurazione batch, una sola istanza di combinazione di valori di OutputType(PDF, PRINT) e RenderType(PostScript, PCL, IPL, ZPL, ecc.) è consentito.

## Best practice  

* Adobe consiglia di ospitare l’archivio dei contenitori BLOB di file di dati nell’area cloud utilizzata da AEM Cloud Service.

## Domande frequenti {#faq}

**È possibile utilizzare una cartella controllata o altri meccanismi di archiviazione per memorizzare l&#39;input e l&#39;output?**

Al momento, è possibile utilizzare l’archiviazione Microsoft Azure per salvare i dati di input e i documenti generati. L’archiviazione di Microsoft Azure offre diverse opzioni per [automatizzare le operazioni di spostamento dei dati](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Un account di archiviazione Microsoft Azure è incluso con la licenza di Cloud Service Experience Manager Forms?**

L’account di archiviazione Microsoft Azure è indipendente dalla licenza del Cloud Service Experience Manager Forms.

**Le API di comunicazione memorizzano i dati sui server di Cloud Service Experience Manager Forms?**

I dati di input e output vengono salvati solo nell’archiviazione Microsoft Azure.

**Le API di comunicazione sono disponibili solo per il Cloud Service Experience Manager Forms? Posso ottenere funzionalità simili in ambiente on-premise?**

È possibile utilizzare il servizio AEM Forms Output per combinare un modello (XFA o PDF) con i dati dei clienti per generare documenti nei formati PDF, PS, PCL e ZPL.

Rispetto all&#39;ambiente on-premise, il Cloud Service offre ulteriori vantaggi in termini di scalabilità automatica ed efficienza in termini di costi.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**È possibile eseguire più operazioni batch contemporaneamente?**
Sì, è possibile eseguire più operazioni batch contemporaneamente. Utilizzare sempre cartelle di origine e di destinazione diverse per ogni operazione per evitare conflitti.
