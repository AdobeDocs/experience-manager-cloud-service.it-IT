---
title: Gestione dei metadati e best practice
description: Scopri le best practice sui metadati per gestire in modo efficace le risorse digitali.
role: User, Admin
exl-id: d90519df-55a6-4e23-81ad-ff2365d71c0d
feature: Metadata, Best Practices
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 1%

---

<!-- Keywords to focus on:
metadata best practices
aem metadata 
experience manager metadata-->

# Gestione dei metadati e best practice {#metadata-best-practices}

Per dare risalto alla tua attività e coinvolgere più clienti, è fondamentale utilizzare elementi visivi di alta qualità come immagini, video e altre risorse digitali. A questo scopo, è necessario un processo che ti consenta di aggiungere metadati a tutte le risorse digitali, affinché siano facilmente ricercabili. I metadati sono dati che forniscono dettagli essenziali sulle risorse digitali, tra cui il nome, il tipo, la posizione all’interno di un archivio, la data di modifica e i tag associati alla risorsa. I metadati semplificano la gestione delle risorse, migliorano la ricercabilità e l’accessibilità e garantiscono un controllo efficace delle versioni.

Scopri come utilizzare i metadati nel sistema di gestione delle risorse digitali (DAM) per [gestire in modo efficace i metadati delle risorse digitali](manage-metadata.md).

## Tipi di metadati

In base ai vari aspetti dei dati, i metadati sono classificati come metadati tecnici, metadati informativi e metadati amministrativi.

### Metadati tecnici

I metadati tecnici comprendono gli aspetti tecnici di una risorsa. Questo tipo di metadati è fondamentale per consentire agli utenti di comprendere le caratteristiche intrinseche delle risorse digitali, facilitando l’elaborazione e l’utilizzo efficienti.
Include dettagli quali:

* Dimensione file
* Formato
* Risoluzione
* Dimensioni
* Metodo colore

### Metadati informativi

I metadati informativi comprendono informazioni descrittive che migliorano la comprensione del contenuto di una risorsa. Questi metadati sono fondamentali per l’individuazione dei contenuti, la ricercabilità e la comprensione del significato della risorsa. I metadati informativi includono parole chiave, didascalie e descrizioni.

Ad esempio, quando gestiamo un video in Experience Manager Assets, possiamo includere i seguenti metadati informativi:

* **Parole chiave**: marketing, lancio prodotto, promozione
* **Didascalia**: Presentazione del nostro prodotto più recente con caratteristiche entusiasmanti
* **Descrizione**: panoramica dettagliata del contenuto video.

Gli utenti alla ricerca di contenuti di marketing possono trovare e comprendere facilmente il significato del video precedente.

### Metadati amministrativi

I metadati amministrativi trattano gli aspetti gestionali delle risorse digitali. Garantisce il controllo degli accessi, la conformità e la gestione del ciclo di vita complessivo delle risorse all’interno del sistema di gestione delle risorse digitali. Include informazioni relative a:

* Proprietà risorsa
* Diritti di utilizzo
* Autorizzazioni
* Altri dettagli amministrativi

I metadati amministrativi garantiscono la corretta gestione delle risorse, il controllo dell&#39;accesso e la conformità all&#39;interno del sistema di gestione delle risorse digitali.

## Best practice per i metadati

### Definire la strategia dei metadati dall’inizio

La gestione dei metadati inizia con la definizione di una strategia per i metadati che fornisca una base per valutare il valore a lungo termine.

La creazione di uno schema di metadati personalizzato in base alle tue esigenze è fondamentale per la pianificazione della strategia per i metadati. Uno schema ben progettato fornisce un framework strutturato per la classificazione e l’organizzazione delle risorse in Experience Manager.

#### Video: aggiungere campi personalizzati allo schema metadati

>[!VIDEO](https://video.tv.adobe.com/v/3425977)

La strategia di metadati può includere la definizione di quanto segue:

* **Obiettivi:** Descrivere chiaramente gli obiettivi e i risultati previsti dei metadati. Identifica l’obiettivo da raggiungere aggiungendo i metadati.

* **Scopo:** definire il motivo per cui si stanno acquisendo i metadati. Specificare il valore aggiunto ai processi, ai sistemi o all&#39;organizzazione.

* **Piano di accessibilità:** Creare un piano per rendere i metadati facilmente accessibili e individuabili. Spiegare chi lo utilizzerà e gli strumenti o i metodi da utilizzare.

* **Proprietà metadati:** Identificare e definire con attenzione ogni proprietà metadati. Assicurati che ogni proprietà abbia un motivo chiaro per essere inclusa, collegandola agli obiettivi e allo scopo.

Per garantire risultati coerenti in tutto l’archivio, pianifica con attenzione la strategia. Ulteriori informazioni su [schemi metadati](metadata-schemas.md).

### Creare un piano di governance dei metadati

La governance dei dati garantisce che le attività di gestione dei metadati dell’organizzazione siano allineate agli obiettivi aziendali generali.
La strategia di governance può comprendere:

* Definizione di regole e procedure per la gestione dei dati e dei metadati.
* Definizione di standard per la qualità e l&#39;integrità dei dati.
* Definizione di ruoli e responsabilità nella gestione dei dati.

Determina da dove provengono le informazioni ed esamina i dettagli della strategia dei metadati, incluse le proprietà e le relative fonti. Può essere scalata a seconda della complessità della strategia. Nelle aziende più grandi, esiste un sistema di gestione dei metadati principale che controlla più sistemi nello stack principale.

>[!NOTE]
>
>Scopri come [gestire i metadati delle risorse digitali](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=it).

### Coerenza con la strategia per i metadati

Una strategia coerente per i metadati garantisce un&#39;organizzazione e un recupero efficaci delle risorse digitali. Adottare un approccio strategico per l&#39;acquisizione e l&#39;implementazione dei valori dei metadati, consentendo la flessibilità necessaria per l&#39;evoluzione senza modifiche non necessarie. <br>

Nella gestione dei metadati a livello aziendale, la coerenza è importante per la denominazione e il riferimento alle risorse. Ad esempio, quando gestisci più risorse contemporaneamente, &quot;puoi aggiungere metadati in blocco. <br>

Ecco alcune delle best practice da seguire:

* **Evita valori duplicati:** Se disponi di una raccolta di immagini da una campagna di marketing, utilizza nomi coerenti ed evita duplicati.

  Ad esempio, invece di utilizzare nomi duplicati come *campaign_image_001* e *campaign_image_002*, implementa una convenzione di denominazione sistematica come *event_promotion* e *product_launch*, garantendo un&#39;identificazione chiara e ordinata.

* **Utilizza i vocabolari controllati in modo efficace:** Implementa i vocabolari controllati utilizzando termini standardizzati per i tag. Scopri come implementare [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md) in modo efficace.

  Ad esempio, utilizza in modo coerente termini come *product_launch* o *event_promotion* quando assegni tag alle immagini con temi per mantenere una sequenza sistematica.

* **Mantieni precisione e completezza:** Per mantenere coerenti i metadati, sono fondamentali precisione, completezza e allineamento tra le varie origini.
Ad esempio, quando aggiungi metadati a un documento PDF, verifica che dettagli come i nomi degli autori e le parole chiave siano precisi e completi.

#### Video: aggiungere metadati in blocco alle risorse

>[!VIDEO](https://video.tv.adobe.com/v/3425978)

### Valutare e migliorare la ricercabilità dei metadati

Valuta la tua strategia di metadati per migliorare la ricercabilità dei metadati. Semplificare i flussi di lavoro e migliorare le funzionalità di ricerca per un riutilizzo efficiente. Evita di trattare i metadati privi di uno scopo chiaro.

Per ottimizzare la ricercabilità dei metadati, considera le seguenti best practice:

* **Ottimizzazione parole chiave:** Migliora la ricercabilità dei metadati ottimizzando le parole chiave associate alle risorse. Per migliorare la pertinenza delle parole chiave per determinate risorse in [!UICONTROL Assets Manager], effettua le seguenti operazioni:

   1. Vai a **[!UICONTROL Assets]** > **[!UICONTROL File]** > **[!UICONTROL [Cartella risorse]]**.
   1. Selezionare la risorsa per la quale si desidera aggiornare i metadati, quindi fare clic su **[!UICONTROL Proprietà]**.
   1. Passa alla scheda **[!UICONTROL Avanzate]**, quindi fai clic su **[!UICONTROL Aggiungi]** in **[!UICONTROL Privilegi elevati per parole chiave di ricerca]**. <br>È necessario utilizzare lo schema metadati predefinito per elevare le parole chiave di ricerca.
   1. Immettere la parola chiave per la quale si desidera aumentare la ricerca, quindi fare clic su **[!UICONTROL Aggiungi]**.<br>
Puoi aggiungere più parole chiave e disporle in base alla tua priorità.
   1. Fai clic su **[!UICONTROL Salva e chiudi]**.
Cerca la risorsa utilizzando le parole chiave aggiunte. La risorsa viene visualizzata tra i primi risultati di ricerca.

  Scopri come [aumentare la ricerca in Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html?lang=it).

* **Campi metadati personalizzati:** Personalizza i campi metadati per acquisire informazioni aggiuntive sulle risorse. Ad esempio, aggiungi campi specifici per i dettagli del progetto, le informazioni sul copyright o qualsiasi altro dato rilevante che migliori le funzionalità di ricerca. Scopri [come modificare o aggiungere metadati personalizzati](meta-edit.md) in Experience Manager Assets.


* **Convalida metadati:** Implementa controlli di convalida per le voci di metadati per garantire coerenza e precisione. L’utilizzo di vocabolari controllati rende il processo di convalida più fluido e diminuisce la possibilità di voci non chiare o incoerenti. Ciò può richiedere l’impostazione di linee guida per determinate proprietà di metadati al fine di evitare informazioni ambigue o incoerenti.

* **Tracciamento dell&#39;utilizzo:** valutare la rilevanza e l&#39;utilizzo di diverse proprietà di metadati nel tempo. Identifica e assegna priorità ai metadati utilizzati di frequente o contribuisce in modo significativo ai processi di ricerca e recupero.

#### Video: aggiungi parole chiave per migliorare la ricercabilità

>[!VIDEO](https://video.tv.adobe.com/v/3425979)

### Metadati semplici e di facile comprensione

Metadati semplificati per una migliore governance e adozione da parte degli utenti. Semplificalo e facile da capire, incoraggiando gli utenti ad aggiungere informazioni essenziali.
Per semplificare i metadati, prova le seguenti best practice:

* **Opzioni di ottimizzazione delle proprietà:** Evidenzia le proprietà essenziali senza sovraccaricare gli utenti con troppi campi di metadati da compilare. Ad esempio, quando aggiungi i metadati per un’immagine, includi solo i campi chiave come titolo, descrizione e tag per una categorizzazione efficace.

* **Eliminare le proprietà predefinite non necessarie:** Semplificare il modulo metadati eliminando le proprietà predefinite non rilevanti per il caso d&#39;uso. Rimuovi le proprietà predefinite raramente utilizzate per un’interfaccia e un’esperienza più pulite.

* **Rivedi e aggiorna periodicamente i metadati:** Aggiorna regolarmente i metadati e adattali alle esigenze e alle tecnologie in continua evoluzione per garantire che gli utenti forniscano informazioni preziose nel tempo.

### Analizza percorso di contenuti

Esaminare la catena di fornitura dei contenuti per individuare le origini dei metadati e coinvolgere tutte le parti interessate, a partire dall&#39;alto, per un approccio completo basato sulle best practice. Coinvolgi diversi membri del personale per garantire il supporto completo in tutta l’organizzazione. <br>Incorpora i metadati in varie fasi per condividere la responsabilità di fornire i dettagli delle risorse durante il caricamento. Ad esempio, l&#39;integrazione di [!DNL Experience Manager Assets] e [!DNL Workfront] offre notevoli vantaggi in termini di gestione dei metadati, migliorando l&#39;efficienza e la collaborazione nella creazione e nella gestione dei contenuti. Questa integrazione garantisce un&#39;efficace sincronizzazione dei metadati per le risorse collegate, aggiornando automaticamente i dettagli del progetto quando vengono apportate modifiche in [!DNL Workfront].

Comunica tempestivamente obiettivi, progressi, tappe fondamentali e sfide per ricevere il contributo e la cooperazione di tutte le parti interessate. Incoraggiare la collaborazione all&#39;interno dell&#39;organizzazione per creare processi efficienti e metadati preziosi.

Ulteriori informazioni su [metadati e i concetti correlati](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-concepts.html?lang=it) per gestire in modo efficace i metadati di Experience Manager.
