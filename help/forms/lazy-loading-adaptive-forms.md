---
title: Come migliorare le prestazioni dei moduli di grandi dimensioni con il caricamento lento?
description: Scopri come migliorare le prestazioni dei moduli di grandi dimensioni con il caricamento lento. Il caricamento lento migliora in modo significativo le prestazioni di Forms adattivi complessi e di grandi dimensioni, posticipando l’inizializzazione e il caricamento dei frammenti di modulo fino a quando non sono visibili.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 0cd38edb-2201-4ca6-8b84-6b5b7f76bd90
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 1%

---

# Miglioramento delle prestazioni dei moduli di grandi dimensioni con caricamento lento{#improve-performance-of-large-forms-with-lazy-loading}

## Introduzione al caricamento lento {#introduction-to-lazy-loading}

Quando i moduli diventano grandi e complessi con centinaia e migliaia di campi, gli utenti finali ottengono tempi di risposta lunghi durante il rendering dei moduli in fase di esecuzione. Per ridurre al minimo il tempo di risposta, l’Adaptive Forms consente di suddividere i moduli in frammenti logici e di configurare per posticipare l’inizializzazione o il caricamento dei frammenti fino a quando il frammento non deve essere visibile. È noto come caricamento lento. Inoltre, i frammenti configurati per il caricamento lazy vengono scaricati quando l’utente passa ad altre sezioni del modulo e i frammenti non sono più visibili.

Comprendiamo innanzitutto i requisiti e i passaggi preparatori prima di configurare il caricamento lento.

## Preparazione della configurazione del caricamento lento {#preparing-to-configure-lazy-loading}

Prima di configurare il caricamento lento dei frammenti nel modulo adattivo, è importante definire strategie per la creazione di frammenti, identificare i valori utilizzati negli script o a cui si fa riferimento in altri frammenti e definire regole per controllare la visibilità dei campi nei frammenti caricati lentamente.

* **Identificare e creare frammenti**
Puoi configurare solo frammenti di modulo adattivi per il caricamento lento. Un frammento è un segmento autonomo che si trova al di fuori di un modulo adattivo e può essere riutilizzato in tutti i moduli. Quindi, il primo passo verso l&#39;implementazione del caricamento lento è identificare le sezioni logiche in una forma e convertirle in frammenti. È possibile creare un frammento da zero o salvare come frammento un pannello modulo esistente.

   <!--For more information about creating fragments, see [Adaptive Form Fragments](adaptive-form-fragments.md).-->

* **Identificare e contrassegnare i valori globali**
Le transazioni basate su Forms richiedono elementi dinamici per acquisire dati rilevanti dagli utenti ed elaborarli per semplificare l&#39;esperienza di compilazione dei moduli. Ad esempio, il modulo include il campo A nel frammento X il cui valore determina la validità del campo B in un altro frammento. In questo caso, se il frammento X è contrassegnato per il caricamento lazy, il valore del campo A deve essere disponibile per convalidare il campo B anche quando il frammento X non è caricato. A questo scopo, puoi contrassegnare il campo A come globale, in modo che il relativo valore sia disponibile per la convalida del campo B quando il frammento X non viene caricato.

   Per informazioni su come rendere globale un valore di campo, vedere [Configurazione del caricamento lento](lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Scrivere regole per controllare la visibilità dei campi**
Forms include alcuni campi e sezioni che non sono applicabili a tutti gli utenti e in tutte le condizioni. Gli autori e gli sviluppatori di Forms utilizzano le regole di visibilità o di visualizzazione per controllarne la visibilità in base agli input degli utenti. Ad esempio, il campo Indirizzo ufficio non viene visualizzato agli utenti che scelgono Disoccupato nel campo Stato impiego di un modulo. Per ulteriori informazioni sulla scrittura delle regole, consulta [Utilizzo dell’editor di regole](rule-editor.md).

   Puoi utilizzare le regole di visibilità nei frammenti caricati in modo differito in modo che i campi condizionali vengano visualizzati solo quando sono obbligatori. Inoltre, contrassegna il campo condizionale globale in modo che faccia riferimento a esso nell’espressione di visibilità del frammento caricato in modo differito.

## Configurazione del caricamento lento {#configuring-lazy-loading}

Per abilitare il caricamento lento in un frammento di modulo adattivo, effettua le seguenti operazioni:

1. Apri il modulo adattivo in modalità di authoring che contiene il frammento che desideri abilitare per il caricamento lento.
1. Seleziona il frammento di modulo adattivo e tocca ![configura](assets/configure-icon.svg).
1. Nella barra laterale, abilita **[!UICONTROL Carica frammento in modo differito]** e tocca **Fine**.

   ![Abilita il caricamento lento per il frammento di modulo adattivo](assets/lazy-loading-fragment.png)

   Il frammento è ora abilitato per il caricamento lento.

Puoi contrassegnare i valori degli oggetti nel frammento caricato in modo differito come globali, in modo che siano disponibili per l’utilizzo negli script quando il frammento che li contiene non viene caricato. Effettua le seguenti operazioni:

1. Apri il frammento di modulo adattivo in modalità di authoring.
1. Tocca il campo di cui desideri contrassegnare il valore come globale, quindi tocca ![configura](assets/configure-icon.svg).
1. Nella barra laterale, abilita **[!UICONTROL Usa valore durante il caricamento lento]**.

   ![Campo di caricamento lazy nella barra laterale](assets/enable-lazy-loading.png)

   Il valore è ora contrassegnato come globale ed è disponibile per l’utilizzo negli script anche quando il frammento che lo contiene viene scaricato.

## Considerazioni e best practice per la configurazione del caricamento lento {#considerations-and-best-practices-for-configuring-lazy-loading}

Alcune limitazioni, raccomandazioni e punti importanti da tenere a mente quando si lavora con il caricamento lento sono i seguenti:

* Si consiglia di utilizzare Forms adattivo basato su schema XSD su Forms adattivo basato su XFA per configurare il caricamento lento su moduli di grandi dimensioni. L’aumento delle prestazioni dovuto all’implementazione di caricamento lento in Adaptive Forms basato su XFA è relativamente inferiore al guadagno in Adaptive Forms basato su XSD.
* Non configurare il caricamento lento per i frammenti in un modulo adattivo che utilizzano **[!UICONTROL Reattivo: tutto su una pagina senza navigazione]** layout del pannello principale. Con la configurazione del layout Reattivo, tutti i frammenti vengono caricati contemporaneamente in un modulo adattivo. ma può anche causare un peggioramento delle prestazioni.
* Si consiglia di non configurare il caricamento lento sui frammenti nel primo pannello riprodotto al caricamento del modulo adattivo.
* Il caricamento lento è supportato fino a due livelli nella gerarchia dei frammenti.
* Assicurati che i campi contrassegnati come globali siano univoci all’interno di un modulo adattivo.
* È consigliabile scrivere regole di visibilità per i frammenti che devono essere visualizzati o nascosti in base a una condizione. Ad esempio, puoi mostrare o nascondere il frammento Dettagli coniuge in base allo stato civile specificato da un utente.
* I componenti Allegato file e Termini e condizioni non sono supportati nei frammenti caricati in modo differito.

### Best practice per lo scripting per la configurazione del caricamento lento {#scripting-best-practices-for-configuring-lazy-loading}

Di seguito sono riportati alcuni punti importanti da tenere presenti durante lo sviluppo di script per pannelli con caricamento lazy:

* Assicurati che gli script di inizializzazione e calcolo utilizzati nei campi di un frammento con caricamento lazy siano idempotenti. Gli script idempotenti sono quelli che hanno lo stesso effetto anche dopo più esecuzioni.
* Utilizzare la proprietà globally available dei campi per rendere disponibili a tutti gli altri pannelli di un modulo i campi presenti in un pannello di caricamento lazy.
* Non inoltrare il valore di riferimento di un campo all’interno di un pannello lento indipendentemente dal fatto che il campo sia contrassegnato globalmente tra frammenti o meno.
* Utilizza la funzione di ripristino del pannello per ripristinare tutto ciò che è visibile nel pannello utilizzando la seguente espressione di clic.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;}).resetData()
