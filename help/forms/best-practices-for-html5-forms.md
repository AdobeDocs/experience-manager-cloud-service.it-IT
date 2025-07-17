---
title: Best practice per i moduli HTML5
description: Ottimizza le prestazioni del Forms HTML5 basato su XFA.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# Best practice per i moduli HTML5{#best-practices-for-html-forms}

<span class="preview"> La funzionalità HTML5 Forms è disponibile come parte del programma di accesso anticipato. Per richiedere l’accesso, invia un’e-mail dal tuo ID e-mail ufficiale (di lavoro) a aem-forms-ea@adobe.com.
</span>

## Panoramica {#overview}

AEM Forms dispone di un componente denominato HTML5 forms. Consente di eseguire il rendering dei PDF forms basati su XFA (file XDP) esistenti in formato HTML5. Questo documento fornisce linee guida e raccomandazioni per ridurre il tempo di caricamento e migliorare le prestazioni dei moduli HTML5 sui dispositivi mobili.

La maggior parte dei dispositivi mobili ha una potenza di elaborazione e funzionalità di memoria limitate. Consente di migliorare il tempo di standby dei dispositivi mobili. I browser web in esecuzione su un dispositivo mobile hanno accesso a risorse limitate (memoria e funzionalità di elaborazione limitate). Una volta raggiunto il limite, il comportamento del browser diventa lento. Questo documento fornisce consigli per controllare le dimensioni di un modulo HTML5. Un modulo più piccolo non supera i limiti di memoria e di potenza di elaborazione di un dispositivo e offre un’esperienza fluida.

Anche se le raccomandazioni discusse in questo articolo sono mirate ai moduli HTML5, questi sono ugualmente applicabili ai PDF forms basati su XFA. Queste best practice contribuiscono collettivamente alle prestazioni complessive dei moduli HTML5. Richiede un&#39;attenta pianificazione per sviluppare forme efficienti e produttive. Iniziamo:

## I nodi sono la valuta dei moduli HTML5, spenderli con saggezza {#nodes-are-currency-of-html-forms-spend-them-wisely}

In genere, un modulo XFA ha più elementi. Ad esempio, tabella, campo di testo e immagini. Ogni elemento ha diverse proprietà per controllarne il comportamento e l&#39;aspetto. Quando si esegue il rendering di un modulo XFA in formato HTML5, tutti gli elementi XFA e le proprietà corrispondenti vengono convertiti in nodi DOM Model o HTML. Questi nodi aumentano le dimensioni e la complessità di un DOM. Rendere il rendering del modulo HTML5 più lento.

Per i browser è più semplice eseguire il rendering di un DOM più semplice. Pertanto, puoi eseguire le seguenti ottimizzazioni su un modulo XFA per ridurre il numero di nodi. Pertanto, genera una struttura DOM snella:

* Utilizzare la proprietà caption per aggiungere un&#39;etichetta a un campo. Non utilizzare un elemento di testo separato per aggiungere un&#39;etichetta. Aiuta a ridurre il peso, portando a un aumento delle prestazioni. Consente inoltre di evitare problemi di layout.
* Ridurre al minimo il numero di elementi di testo da disegnare in un modulo. Gli elementi di disegno sono utili per migliorare la leggibilità e l&#39;aspetto, ma non dispongono di alcuna funzionalità di memorizzazione delle informazioni. Si consiglia di unire più elementi di testo Draw in un singolo elemento di testo Draw. Non lasciate nulla di intentato per rendere la forma più snella.

## I moduli Lite offrono prestazioni migliori, mantenendo le risorse compresse {#lite-forms-perform-better-keep-the-resources-compressed}

Un modulo HTML5 può contenere più risorse esterne, ad esempio immagini, JavaScript e file CSS. Ogni volta che un browser richiede un modulo, le risorse esterne vengono inviate tramite la rete. Il tempo necessario per spostarsi in rete è direttamente proporzionale alle dimensioni dei file.

Pertanto, ridurre le dimensioni delle risorse esterne e utilizzare solo le risorse assolutamente necessarie è il metodo preferito per migliorare le prestazioni dei moduli. Per ridurre le dimensioni delle risorse esterne di un modulo, è possibile eseguire le seguenti ottimizzazioni su un modulo XFA:

* Usa [immagini compresse](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md). Riduce l&#39;attività di rete e la quantità di memoria necessaria per il rendering di un modulo. Pertanto, il tempo di caricamento della maschera diminuisce notevolmente.
* Utilizza l’opzione minimizza in AEM Configuration Manager (Day CQ HTML Library Manager) per comprimere i file JavaScript e CSS. Per ulteriori dettagli, vedere [Impostazioni di configurazione OSGi](/help/implementing/deploying/configuring-osgi.md).
* Attiva la compressione Web. Riduce la dimensione delle richieste e delle risposte generate da un modulo. Per ulteriori dettagli, vedere [Ottimizzazione delle prestazioni di AEM Forms Server](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html).

## Mantieni vivo l’interesse, mostra solo i campi obbligatori  {#keep-the-interest-alive-show-only-required-fields}

Un modulo HTML5 può contenere centinaia di pagine. Il caricamento di un modulo con un numero elevato di campi nel browser è lento. È possibile eseguire le seguenti ottimizzazioni su un modulo XFA per ottimizzare i moduli con un numero elevato di campi e pagine:

* Valutare la suddivisione dei moduli di grandi dimensioni in più moduli. È inoltre possibile utilizzare un set di moduli per raggruppare tutti i moduli più piccoli e presentarli come un&#39;unica unità. Un set di moduli carica solo i moduli richiesti. Inoltre, in un set di moduli è possibile configurare campi comuni in moduli diversi per condividere associazioni di dati. Le associazioni di dati consentono agli utenti di compilare le informazioni comuni una sola volta; le informazioni vengono compilate automaticamente nei moduli successivi, determinando miglioramenti sostanziali delle prestazioni. Per ulteriori dettagli sui set di moduli, vedere [Set di moduli in AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* È consigliabile suddividere le sezioni e spostare ogni sezione in una pagina diversa. I moduli HTML5 caricano dinamicamente ogni pagina nella richiesta di scorrimento delle pagine. Nella memoria vengono memorizzate solo le pagine scorrevoli (la pagina visualizzata e le pagine precedenti); le altre pagine vengono caricate su richiesta. La suddivisione e lo spostamento di una sezione in una pagina specifica riduce il tempo necessario per caricare un modulo. È inoltre possibile utilizzare la prima pagina del modulo come pagina di destinazione. È simile al sommario di un libro. Una pagina di destinazione del modulo contiene solo collegamenti alle altre sezioni del modulo. Migliora in modo significativo il tempo di caricamento della prima pagina del modulo e consente di migliorare l’esperienza utente.
* Per impostazione predefinita, le sezioni condizionali vengono nascoste. Rendi visibili queste sezioni solo quando viene soddisfatta una determinata condizione. Consente di ridurre al minimo le dimensioni del DOM. È inoltre possibile utilizzare la navigazione a schede per visualizzare una sola sezione alla volta.

## Meno è di più, riduci il numero di pagine {#less-is-more-reduce-the-number-of-pages}

I moduli HTML5 possono contenere campi basati su dati (tabelle e sottomoduli). Questi campi consentono di espandere le dimensioni del modulo in fase di esecuzione. Ad esempio, una tabella basata sui dati in un modulo di HTML5 può estendersi su migliaia di righe. Tali tabelle possono causare il deterioramento del layout e delle prestazioni. Le ottimizzazioni suggerite di seguito consentono di ridurre il tempo di caricamento dei moduli HTML5 con campi basati sui dati:

* Utilizza gli script XFA per ottenere una navigazione impaginata per visualizzare campi basati su dati (tabelle e sottomaschere). Nella navigazione impaginata, in una pagina vengono visualizzati solo dati specifici. Limita l’operazione di disegno del browser ai campi visualizzati in una sola volta e semplifica la navigazione in un modulo. Inoltre, gli utenti dei dispositivi mobili sono interessati solo a un sottoinsieme di dati. Consente di fornire un’esperienza utente ottimale e di ridurre il tempo necessario per caricare i dati richiesti. Si ottengono due soluzioni al prezzo di una.  Inoltre, la navigazione impaginata non è disponibile come funzionalità integrata. Puoi utilizzare gli script XFA per sviluppare la navigazione a pagina.

* Valuta l’unione di più colonne di sola lettura in una singola colonna. Riduce la memoria necessaria per visualizzare il modulo. Inoltre, evita di visualizzare le colonne che non richiedono alcun input da parte degli utenti.
* Valuta la suddivisione del modulo basato su dati in un [set di moduli](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html), se i suggerimenti di cui sopra non producono molti miglioramenti. Se ad esempio una tabella contiene più di 1000 righe, spostare ogni 100 righe in una maschera diversa. Ciò contribuirebbe a migliorare il tempo di caricamento e le prestazioni dei moduli.  Si noti inoltre che un set di moduli genera un XML di invio consolidato per tutti i moduli. Per differenziare i dati di ogni modulo, utilizzare radici di dati diverse. Per ulteriori informazioni, vedere [Set di moduli in AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## Potenza di due per documento record (DOR) {#power-of-two-for-document-of-record-dor}

Un modulo XFA può avere un numero elevato di sezioni dedicate solo al documento di record (DOR, Document of Record). Per ridurre il numero di nodi e migliorare le prestazioni di un modulo di questo tipo, è possibile mantenere diverse copie del modulo, una copia da compilare e un&#39;altra da generare un documento di record sul server. Nella copia per compilare il modulo XFA, mostra i campi necessari solo per acquisire i dati. In Genera documento di record XFA da, mantenere i campi obbligatori solo nell’output stampato del modulo. Prima di scegliere l&#39;approccio suggerito, valutare il miglioramento delle prestazioni e il sovraccarico di manutenzione.

## Letture consigliate  {#recommended-reads}

I moduli di Adobe Experience Manager (AEM) consentono di trasformare transazioni complesse in esperienze digitali semplici e straordinarie. Tuttavia, esso richiede uno sforzo concertato per sviluppare forme efficienti e produttive. Oltre a HTML5 Forms, di seguito sono riportate alcune indicazioni consigliate per le best practice generali di AEM:


<!--

* Best practices for Deploying and maintaining AEM
* Best practices for Authoring content
* [Best practices for Administering AEM](/help/sites-administering/administer-best-practices.md)
* [Best practices for Developing solutions](/help/sites-developing/best-practices.md)
* [Best practices for working with adaptive forms](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms server does not embed fonts to a Dynamic PDF form](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

-->

## Scheda di riferimento rapido {#quick-reference-card}

È possibile stampare la seguente scheda (fare clic sulla scheda per scaricare una versione ad alta risoluzione) e tenerla sulla scrivania per un riferimento rapido:
[![Scheda di riferimento rapido sulle best practice di HTML5 Forms](assets/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
