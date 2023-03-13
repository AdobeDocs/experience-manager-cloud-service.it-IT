---
title: Personalizzazione e targeting dei contenuti
description: Scopri come creare contenuti personalizzati e mirati con AEM
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 566cd449c536de4179e32c94df90b46d61e0103a
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 100%

---


# Personalizzazione e targeting dei contenuti {#personalization-and-content-targeting}

Personalizzare i contenuti web che fornisci ai clienti significa adattare tali esperienze ai loro interessi e alle loro esigenze. Puoi farlo in base alle informazioni che hai su di loro; ad esempio, riepilogo degli acquisti, età, genere o area geografica.

Con Adobe Experience Manager as a Cloud Service (AEM) puoi creare una selezione di contenuti, quindi specificare quale pubblico (gruppi di utenti finali) visualizzerà ogni singola esperienza. Ciò significa che eseguire il targeting delle esperienze personalizzate a tipi di pubblico specifici.

Quando il lettore è online, il motore di targeting esamina le informazioni disponibili sull’utente finale e le confronta con le definizioni delle esperienze. Il motore poi *“decide”* quale esperienza personalizzata verrà visualizzata.

AEM fornisce un framework di strumenti per:

* Creazione di contenuti mirati, adatti a diversi tipi di pubblico, in base alle informazioni disponibili sui clienti.
* Definizione delle regole utilizzate per risolvere le informazioni utente note rispetto alla definizione di un pubblico.
* Configurazione delle pagine per presentare esperienze personalizzate mirate, in modo da rendere lo specifico contenuto applicabile all’utente finale corrente.

La panoramica seguente presenta alcuni termini utilizzati nell’ambito della personalizzazione in AEM as a Cloud Service, seguiti da un ordine di azioni consigliato.

## Esperienza {#experience}

Un’esperienza è un contenuto che desideri mostrare agli utenti finali.

## Esperienza personalizzata {#personalized-experience}

Un’esperienza personalizzata è un’esperienza che viene mostrata a un pubblico limitato. Una volta che hai definito il pubblico, il contenuto verrà visualizzato solo se le informazioni note sull’utente finale corrente corrispondono alla definizione del pubblico.

Quando crei le pagine puoi definire più esperienze, ognuna delle quali corrisponde a uno o più tipi di pubblico. Se l’utente finale non risulta idoneo per nessuno dei tipi di pubblico che hai definito, viene visualizzata l’esperienza predefinita.

### Offerta {#offer}

Un’offerta è un’esperienza personalizzata, spesso disponibile per un periodo di tempo limitato.

Ad esempio, una pagina di un sito web può utilizzare delle offerte come immagini teaser che appaiono nella parte superiore della pagina. Se la pagina è visitata da una persona sopra i 30 anni e da una sotto i 30 anni, a ciascuna verrà presentata un’offerta differente nel teaser dell’esperienza.

## Pubblico {#audience}

Un pubblico è un gruppo di utenti finali ai cui desideri indirizzare contenuti personalizzati. Quando un visitatore apre una pagina web, la logica della pagina determina il pubblico a cui appartiene in base alle informazioni note. Quindi, in base a tale valutazione, AEM mostra i contenuti creati per quello specifico pubblico.

I tipi di pubblico si basano su segmenti marketing. Vengoni creato in AEM o in Adobe Target; puoi creare i tipi di pubblico di Adobe Target direttamente in AEM utilizzando la console Pubblico.

### Segmento {#segment}

All’interno di AEM ContextHub, un pubblico è definito come un segmento, in base a regole (condizioni). Queste vengono quindi risolte per presentare i contenuti appropriati.

## Attività {#activity}

Un’attività:

* definisce la mappatura di un pubblico specifico (segmento) con un’esperienza specifica;
* definisce il periodo di tempo per il quale viene applicato il targeting;
* identifica il [motore di targeting](#targeting-engine) utilizzato dalle pagine.

L’attività può essere un’attività di personalizzazione o un’attività Test A/B (nel caso del flusso di lavoro di personalizzazione AEM e Adobe Target).

Ad esempio, un’attività può definire le esperienze per due segmenti di pubblico distinti: persone over 30 e persone under 30. Una pagina del sito web potrebbe quindi presentare prodotti diversi per ogni pubblico.

Un altro esempio potrebbe essere un catalogo di prodotti con teaser su prodotti stagionali. Un’attività “Sport estate” potrebbe quindi definire i tipi di pubblico a cui verranno indirizzati i teaser durante i mesi estivi.

Usa la [console Attività](/help/sites-cloud/authoring/personalization/activities.md) per creare e gestire le attività dei tuoi [marchi](#brand). Puoi anche creare le attività mentre realizzi i [contenuti mirati (di destinazione)](/help/sites-cloud/authoring/personalization/targeted-content.md) con [modalità di targeting](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Marchio {#brand}

Un marchio offre una selezione di attività e aree di marketing.

Quando crei un marchio utilizzando la console Attività, questo viene visualizzato anche nella console Offerte.

### Area {#area}

Un’area è una suddivisione di un marchio.

## Modalità di targeting {#targeting-mode}

Durante l’authoring, si tratta della modalità di modifica utilizzata per attivare e configurare i componenti per la personalizzazione.

Puoi [creare contenuti mirati (di destinazione)](/help/sites-cloud/authoring/personalization/targeted-content.md) utilizzando la modalità di targeting di AEM. La modalità di targeting e i componenti di destinazione forniscono gli strumenti necessari per creare i contenuti da usare nelle esperienze delle attività di marketing.

## Frammento di esperienza {#experience-fragments}

Un set raggruppato di componenti che compongono un’esperienza.

I [frammenti di esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) sono costituiti da contenuti e informazioni (stile, ecc.) per creare un’esperienza; possono essere utilizzati direttamente durante l’authoring delle pagine. Possono essere considerati come un sottoinsieme di una pagina AEM. Consentono agli autori di contenuti di riutilizzare i contenuti tra canali diversi, incluse le pagine Sites e i sistemi di terze parti.

Una personalizzazione, ad esempio, può essere ottenuta combinando insieme un titolo, un’immagine, una descrizione e pulsante di invito all’azione in modo da creare un’esperienza teaser. I frammenti di esperienza hanno un ruolo chiave nell’utilizzo delle funzioni di personalizzazione di Adobe Target.

## Motore di targeting {#targeting-engine}

Il motore di targeting è il meccanismo che risolve la logica per la creazione di contenuti mirati. Le [attività](/help/sites-cloud/authoring/personalization/activities.md) sono configurate per utilizzare uno di due motori di targeting disponibili: AEM e Adobe Target.

Il motore di targeting è la piattaforma o il meccanismo che determina quale sistema di personalizzazione utilizzare.

Attualmente AEM può utilizzare:

* [AEM ContextHub](#aem-contexthub) (AEM standard);
* il motore di personalizzazione di [Adobe Target](#adobe-target).

>[!CAUTION]
>
>Una singola pagina AEM non può utilizzare entrambi i motori contemporaneamente.
>
>È possibile utilizzare entrambi i motori su pagine diverse all’interno dello stesso sito.

### AEM ContextHub {#aem-contexthub}

AEM fornisce il motore di targeting integrato [ContextHub](/help/implementing/developing/personalization/contexthub.md) che elabora le richieste delle pagine e determina il contenuto da visualizzare. Quando utilizzi il motore di targeting di AEM, puoi usare solo i segmenti creati con AEM per definire il pubblico delle esperienze.

### Adobe Target {#adobe-target}

Il motore di targeting di [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) permette di tenere traccia delle informazioni raccolte dalle visite della pagina in Adobe Target.

* Con questo motore di destinazione, si utilizzano i segmenti importati da Adobe Target per definire il pubblico delle esperienze.
* Le attività che sfruttano Adobe Target vengono [sincronizzate con Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Puoi usare questo motore di targeting dopo averlo [integrato con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

## Come impostare i contenuti personalizzati {#how-to-setup-personalized-content}

Per distribuire i contenuti personalizzati, sono necessari vari passaggi e definizioni:

1. Imposta il motore di targeting effettuando una delle seguenti operazioni:

   1. Configurando [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. Integrando [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. Configura i tipi di pubblico.

   1. A seconda del motore di targeting, definisci il [pubblico Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=it) o il [segmento ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md), e le relative regole.

1. Crea il tuo [marchio e le attività](/help/sites-cloud/authoring/personalization/activities.md).

1. Crea la selezione di esperienze da mostrare ai vari tipi di pubblico.

1. Personalizza queste esperienze, eseguendo il [targeting](/help/sites-cloud/authoring/personalization/targeted-content.md) per tipi di pubblico specifici (segmenti).