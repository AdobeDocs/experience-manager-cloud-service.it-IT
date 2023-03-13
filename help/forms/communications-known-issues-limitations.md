---
title: Considerazioni sui problemi noti e sulle best practice
description: Best practice di comunicazione, problemi noti e limitazioni
exl-id: e95615dd-e494-40cd-9cdf-6e9761ca3b3e
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 0%

---

# Considerazioni sui problemi noti e sulle best practice {#best-practices-known-issues-and-limitations}

Prima di iniziare a utilizzare le API di comunicazione, esamina le considerazioni seguenti, i problemi noti e le domande frequenti:

## Considerazioni  {#considerations-for-communications-apis}

### Dati modulo {#form-data}

Le API di comunicazione accettano come input sia la struttura di un modulo creata in genere nella finestra di progettazione che i dati del modulo XML. Per compilare un documento con dati, è necessario che nei dati del modulo XML sia presente un elemento XML per ogni campo modulo che si desidera compilare. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Non è necessario che corrisponda all&#39;ordine in cui vengono visualizzati gli elementi XML. Il fattore importante è che gli elementi XML vengono specificati con i valori corrispondenti.

Prendi in considerazione il seguente esempio di modulo di richiesta di prestito:

![Modulo di richiesta di prestito](assets/loanFormData.png)

Per unire i dati in questa struttura di modulo, creare un&#39;origine dati XML corrispondente al modulo. Il codice XML riportato di seguito rappresenta un&#39;origine dati XML che corrisponde al modulo di applicazione ipotecaria di esempio.

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

Per un accesso completo alle funzionalità di rendering delle API di comunicazione, si consiglia di utilizzare un file XDP come input. A volte è possibile utilizzare un file PDF. Tuttavia, l’utilizzo di un file PDF come input presenta le limitazioni seguenti:

Non è possibile eseguire il rendering di un documento PDF che non contiene un flusso XFA come PostScript, PCL o ZPL. Le API di comunicazione possono eseguire il rendering di documenti PDF con flussi XFA (ovvero, moduli creati in Designer) in formati laser ed etichette. Se il documento PDF è firmato, certificato o contiene diritti di utilizzo (applicati mediante il servizio AEM Forms Reader Extensions), non può essere sottoposto a rendering in questi formati di stampa.


### Aree stampabili {#printable-areas}

Il margine non stampabile predefinito di 0,25 pollici non è esatto per le stampanti di etichette e varia da stampante a stampante e da dimensioni etichetta a dimensioni etichetta. Tuttavia, si consiglia di mantenere il margine di 0,25 pollici o ridurlo. Si consiglia tuttavia di non aumentare il margine non stampabile. In caso contrario, le informazioni nell&#39;area di stampa non vengono stampate correttamente.

Assicurarsi sempre di utilizzare il file XDC corretto per la stampante. Ad esempio, evitare di scegliere un file XDC per una stampante da 300 dpi e di inviare il documento a una stampante da 200 dpi.

### Solo script per moduli XFA (XDP/PDF) {#scripts}

Una progettazione di moduli utilizzata con le API di comunicazione può contenere script eseguiti sul server. Verificare che la struttura di un modulo non contenga script eseguiti sul client. Per informazioni sulla creazione di script di progettazione di moduli, vedere [Guida di Designer](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### Mappatura font {#font-mapping}

Per progettare un modulo che utilizza tipi di carattere residenti nella stampante, scegliere un nome di tipo in Designer che corrisponda ai tipi di carattere disponibili nella stampante. Un elenco di font supportati per PCL o PostScript si trova nei profili dispositivo corrispondenti (file XDC). In alternativa, è possibile creare la mappatura dei caratteri per mappare i caratteri non residenti nella stampante ai caratteri residenti nella stampante con un nome di font diverso. Ad esempio, in uno scenario PostScript, i riferimenti al font Arial® possono essere mappati al font Helvetica® residente nella stampante.

Se in un computer client è installato un tipo di carattere, questo sarà disponibile nell&#39;elenco a discesa di Designer. Se il tipo di carattere non è installato, è necessario specificarne manualmente il nome. L&#39;opzione &quot;Sostituisci definitivamente i caratteri non disponibili&quot; in Designer può essere disattivata. In caso contrario, quando il file XDP viene salvato in Designer, il nome del font di sostituzione viene scritto nel file XDP. Ciò significa che non viene utilizzato il tipo di carattere residente nella stampante.

Esistono due tipi di OpenType ® i caratteri. Un tipo di carattere è un&#39;OpenType TrueType® supportata da PCL. L&#39;altro è OpenType CFF®. L&#39;output di PDF e PostScript supporta i font Type-1, TrueType e OpenType® incorporati. L&#39;output PCL supporta i caratteri TrueType incorporati.

Tipo-1 e OpenType ® i font non sono incorporati nell&#39;output PCL. Contenuto formattato con tipo-1 e OpenType ® i font vengono rasterizzati e generati come immagini bitmap che possono essere grandi e più lente da generare.

I font scaricati o incorporati vengono automaticamente sostituiti durante la generazione dell&#39;output PostScript, PCL o PDF. Ciò significa che nell&#39;output generato viene incluso solo il sottoinsieme dei glifi di font necessari per il corretto rendering del documento generato.

### Utilizzo dei file dei profili dispositivo (file XDC) {#working-with-xdc-files}

Un profilo dispositivo (file XDC) è un file di descrizione della stampante in formato XML. Questo file consente alle API di comunicazione di generare documenti come formati di stampanti laser o di etichette. Le API di comunicazione utilizzano i file XDC tra cui:

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

Puoi utilizzare i file XDC forniti per generare documenti di stampa o modificarli in base alle tue esigenze.
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

Si tratta di file XDC di riferimento che supportano le funzioni di stampanti specifiche, ad esempio caratteri residenti, cassetti della carta e cucitrici. Lo scopo di questo riferimento è quello di aiutarti a capire come impostare le tue stampanti utilizzando i profili dispositivo. Il riferimento è anche un punto di partenza per stampanti simili nella stessa linea di prodotti.

### Utilizzo del file di configurazione XCI {#working-with-xci-files}

Le API di comunicazione utilizzano un file di configurazione XCI per eseguire attività quali controllare se l’output è un singolo pannello o impaginato. Anche se questo file contiene impostazioni che possono essere impostate, non è tipico modificare questo valore. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Puoi trasmettere un file XCI modificato mentre utilizzi un’API di comunicazione. In questo caso, crea una copia del file predefinito, modifica solo i valori che richiedono modifiche per soddisfare i requisiti aziendali e utilizza il file XCI modificato.

Le API di comunicazione iniziano con il file XCI predefinito (o il file modificato). Quindi applica i valori specificati utilizzando le API di comunicazione. Questi valori sostituiscono le impostazioni XCI.

La tabella seguente specifica le opzioni XCI.

| Opzione XCI | Descrizione |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/present/pdf/creator | Identifica il creatore del documento utilizzando la voce Creator nel dizionario Document Information. Per informazioni su questo dizionario, consulta la guida di riferimento per le PDF. |
| config/present/pdf/producer | Identifica il produttore del documento utilizzando la voce Producer nel dizionario Document Information. Per informazioni su questo dizionario, consulta la guida di riferimento per le PDF. |
| config/present/layout | Controlla se l’output è un singolo pannello o impaginato. |
| config/present/pdf/compression/level | Specifica il grado di compressione da utilizzare durante la generazione di un documento PDF. |
| config/present/pdf/scriptModel | Controlla se le informazioni specifiche XFA vengono incluse nel documento di output PDF. |
| config/present/common/data/adjustData | Controlla se l&#39;applicazione XFA regola i dati dopo l&#39;unione. |
| config/present/pdf/renderPolicy | Controlla se la generazione del contenuto della pagina viene eseguita sul server o differita al client. |
| config/present/common/locale | Specifica le impostazioni locali predefinite utilizzate nel documento di output. |
| config/present/destination | Quando è contenuto da un elemento presente, specifica il formato di output. Quando è contenuto in un elemento openAction, specifica l&#39;azione da eseguire all&#39;apertura del documento in un client interattivo. |
| config/present/output/type | Specifica il tipo di compressione da applicare a un file o il tipo di output da produrre. |
| config/present/common/temp/uri | Specifica l&#39;URI del modulo. |
| config/present/common/template/base | Specifica una posizione di base per gli URI nella progettazione del modulo. Quando questo elemento è assente o vuoto, la posizione della struttura del modulo viene utilizzata come base. |
| config/present/common/log/to | Controlla la posizione in cui vengono scritti i dati di log o di output. |
| config/present/output/to | Controlla la posizione in cui vengono scritti i dati di log o di output. |
| config/present/script/currentPage | Specifica la pagina iniziale all&#39;apertura del documento. |
| config/present/script/exclude | Informa il server AEM Forms/le API di comunicazione degli eventi da ignorare. |
| config/present/pdf/linearized | Controlla se il documento PDF di output è linearizzato. |
| config/present/script/runScript | Controlla il set di script eseguiti da AEM Forms. |
| config/present/pdf/tagged | Controlla l&#39;inclusione dei tag nel documento PDF di output. I tag, nel contesto di PDF, sono informazioni aggiuntive incluse in un documento per esporre la struttura logica del documento. I tag facilitano l’accesso facilitato e la riformattazione. Ad esempio, un numero di pagina può essere contrassegnato come un artefatto in modo che un assistente vocale non lo enunci al centro del testo. Sebbene i tag rendano un documento più utile, aumentano anche le dimensioni del documento e il tempo di elaborazione necessario per crearlo. |
| config/present/pdf/version | Specifica la versione del documento PDF da generare. |


## Problemi noti

* È possibile utilizzare un tipo di rendering specifico (PDF, PRINT) solo una volta nell&#39;elenco delle opzioni di stampa. Ad esempio, non potete avere due opzioni PRINT ciascuna che specificano un tipo di rendering PCL.

* Per una configurazione batch, solo un&#39;istanza di combinazione di valori di OutputType(PDF, PRINT) e RenderType(PostScript, PCL, IPL, ZPL, ecc.) è consentito.

* Per le API asincrone (elaborazione in batch), il livello di record predefinito è impostato su 2. Puoi utilizzare un XCI personalizzato per cambiare il livello di record in 1.

* Quando l’XCI predefinito è configurato, include il percorso fino alla rappresentazione originale. Esempio `/content/dam/formsanddocuments/default.xci/jcr:content/renditions/original`



## Best practice  

* L’Adobe consiglia di ospitare l’archivio dei contenitori blob dei file di dati nell’area cloud utilizzata da AEM Cloud Service.

## Domande frequenti {#faq}

**È possibile utilizzare una cartella controllata o altri meccanismi di archiviazione per memorizzare input e output?**

Al momento, è possibile utilizzare Archiviazione di Microsoft Azure per salvare i dati di input e i documenti generati. L’archiviazione di Microsoft Azure offre diverse opzioni per [automatizzare le operazioni di spostamento dei dati](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Un account di archiviazione di Microsoft Azure è incluso nella licenza di Cloud Service di Experience Manager Forms?**

L&#39;account di archiviazione di Microsoft Azure è indipendente dalla licenza di Cloud Service di Experience Manager Forms.

**Le API di comunicazione memorizzano i dati sui server di Cloud Service Experience Manager Forms?**

I dati di input e output vengono salvati solo nell&#39;archiviazione di Microsoft Azure.

**Le API di comunicazione sono disponibili solo per il Cloud Service Experience Manager Forms? È possibile ottenere funzionalità simili in un ambiente on-premise?**

Puoi utilizzare il servizio di output di AEM Forms per combinare un modello (XFA o PDF) con i dati del cliente per generare documenti in formato PDF, PS, PCL e ZPL.

Rispetto all&#39;ambiente on-premise, il Cloud Service offre ulteriori vantaggi in termini di scalabilità automatica e convenienza economica.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**È possibile eseguire più operazioni batch contemporaneamente?**
Sì, è possibile eseguire più operazioni batch contemporaneamente. Utilizzare sempre cartelle di origine e di destinazione diverse per ogni operazione per evitare conflitti.
