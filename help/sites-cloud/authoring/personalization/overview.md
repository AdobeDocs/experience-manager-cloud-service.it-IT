---
title: Personalizzazione e targeting dei contenuti
description: Scopri come creare contenuti personalizzati e mirati con AEM
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: f2466cb5cda759f0c97cd69810d208d47fb73b98
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 10%

---


# Personalizzazione e targeting dei contenuti {#personalization-and-content-targeting}

La personalizzazione dei contenuti web che fornisci ai clienti significa adattare tali esperienze ai loro interessi e alle loro esigenze. Puoi farlo in base alle informazioni che hai su di loro; ad esempio, riepilogo acquisti, età, genere, geografia, tra gli altri.

Con Adobe Experience Manager as a Cloud Service (AEM) puoi creare una selezione di contenuti, quindi specificare quali gruppi di utenti finali visualizzeranno ogni singola esperienza. Ciò significa che stai eseguendo il targeting delle tue esperienze personalizzate a tipi di pubblico specifici.

Quando il lettore è online, il motore di destinazione esamina le informazioni disponibili sull’utente finale e le confronta con le definizioni dell’esperienza. Il motore *&quot;decide&quot;* quale esperienza personalizzata deve essere visualizzata.

AEM fornisce un quadro di strumenti per:

* Creazione di contenuti mirati, adatti a diversi tipi di pubblico, in base alle informazioni sui clienti disponibili.
* Definizione delle regole utilizzate per risolvere le informazioni utente note rispetto a una definizione di pubblico.
* Configurazione delle pagine per presentare esperienze personalizzate mirate; per rendere il contenuto specifico applicabile all’utente finale corrente.

La panoramica seguente presenta alcuni termini utilizzati per la personalizzazione in AEM as a Cloud Service, seguiti da un ordine di azione consigliato.

## Esperienza {#experience}

Un’esperienza è un contenuto che desideri mostrare agli utenti finali.

## Esperienza personalizzata {#personalized-experience}

Un’esperienza personalizzata è un’esperienza che viene mostrata a un pubblico limitato. Il pubblico è definito da te e il contenuto viene visualizzato solo quando le informazioni note sull’utente finale corrente corrispondono a tale definizione di pubblico.

Durante la creazione di pagine si definiscono più esperienze, con ogni esperienza di risoluzione a uno o più tipi di pubblico. Se non viene risolto alcun pubblico, viene visualizzata l&#39;esperienza predefinita.

### Offerta {#offer}

Un’offerta è un’esperienza personalizzata, spesso disponibile per un periodo di tempo limitato.

Ad esempio, per una pagina di un sito Web di esempio è possibile utilizzare le offerte come immagine teaser che appare nella parte superiore della pagina. Una persona sopra i 30 e una persona sotto i 30 vedranno diverse offerte come teaser di esperienza.

## Pubblico {#audience}

Un pubblico è un gruppo di utenti finali di cui desideri eseguire il targeting con contenuto personalizzato. Quando un visitatore apre una pagina web, la logica della pagina determina il pubblico a cui appartiene in base alle informazioni note. In base a tale valutazione AEM vengono visualizzati i contenuti creati per quel pubblico.

Il pubblico si basa sui segmenti di marketing. sono creati in AEM o in Adobe Target; puoi creare i tipi di pubblico di Adobe Target direttamente in AEM utilizzando la console Pubblico .

### Segmento {#segment}

All’interno AEM ContextHub, un pubblico è definito come un segmento, in base a regole (condizioni). Vengono quindi risolte per eseguire il rendering del contenuto richiesto.

## Attività {#activity}

Un’attività:

* definisce la mappatura di un pubblico specifico (segmento) con un’esperienza specifica
* definisce il periodo di tempo per il quale viene applicato il targeting
* identifica [motore di destinazione](#targeting-engine) che le pagine utilizzano

L’attività può essere un’attività di personalizzazione o un’attività Test A/B (nel caso del flusso di lavoro di personalizzazione AEM e Adobe Target).

Ad esempio, un’attività potrebbe definire le esperienze per due tipi di pubblico separati: persone di età superiore ai 30 anni e persone di età inferiore ai 30 anni. Una pagina del sito web potrebbe quindi visualizzare prodotti diversi per ogni pubblico.

Oppure, come altro esempio, il catalogo dei prodotti può includere teaser che focalizzano l’attenzione sui prodotti stagionali. Quindi un&#39;attività sportiva estiva potrebbe definire il pubblico a cui i teaser devono far fronte durante i mesi estivi.

Utilizza la [Console Attività](/help/sites-cloud/authoring/personalization/activities.md) per creare e gestire le attività per [Marchi](#brand). Puoi anche creare attività durante la creazione del tuo [contenuto di destinazione](/help/sites-cloud/authoring/personalization/targeted-content.md) con [Modalità di targeting](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode).

### Marchio {#brand}

Un marchio offre una selezione di attività e aree di marketing.

Quando crei un marchio utilizzando la console Attività , questo viene visualizzato anche nella console Offerte .

### Area {#area}

Un’area è una suddivisione di un marchio.

## Modalità di targeting {#targeting-mode}

Durante l’authoring, si tratta della modalità di modifica utilizzata per attivare e configurare i componenti per la personalizzazione.

È possibile [Contenuto mirato dell’autore](/help/sites-cloud/authoring/personalization/targeted-content.md) utilizzando la modalità Targeting di AEM. La modalità di targeting e i componenti di destinazione forniscono gli strumenti per la creazione di contenuti per le esperienze delle vostre attività di marketing.

## Frammento esperienza {#experience-fragments}

Un set raggruppato di componenti che compongono un’esperienza.

[Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) sono fatti di contenuto e informazioni (stile, ecc.) per creare un’esperienza; possono essere utilizzati direttamente durante l’authoring delle pagine. Possono essere considerati come un sottoinsieme di una pagina AEM. Consentono agli autori di contenuti di riutilizzare i contenuti tra canali diversi, incluse le pagine Sites e i sistemi di terze parti.

Per un esempio di personalizzazione, è possibile combinare un’esperienza teaser con un pulsante Titolo, Immagine, Descrizione e Invito all’azione . L’utilizzo dei frammenti esperienza è una parte chiave dell’utilizzo della personalizzazione Adobe Target.

## Motore di destinazione {#targeting-engine}

Il motore di destinazione è il meccanismo che risolve la logica per il contenuto di destinazione. Le [Attività](/help/sites-cloud/authoring/personalization/activities.md) sono configurate per l&#39;utilizzo di uno di due motori di targeting a tua disposizione: AEM e Adobe Target.

Il motore di targeting è la piattaforma o il meccanismo che determina quale sistema di personalizzazione utilizzare.

Attualmente AEM utilizzare:

* [AEM ContextHub](#aem-contexthub) (AEM standard)
* la [Adobe Target](#adobe-target) motore di personalizzazione

>[!CAUTION]
>
>Una singola pagina AEM non può utilizzare entrambi i motori contemporaneamente.
>
>È possibile utilizzare entrambi i motori su pagine separate all’interno dello stesso sito.

### AEM ContextHub {#aem-contexthub}

AEM fornisce il motore di targeting integrato [ContextHub](/help/implementing/developing/personalization/contexthub.md) elabora le richieste di pagina e determina il contenuto da visualizzare. Quando utilizzi il motore di destinazione AEM, puoi usare solo i segmenti creati con AEM per definire il pubblico delle esperienze.

### Adobe Target {#adobe-target}

La [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) il motore di destinazione fa sì che le informazioni raccolte dalle visite di pagina siano tracciate in Adobe Target.

* Con questo motore di destinazione, si utilizzano i segmenti importati da Adobe Target per definire il pubblico delle esperienze.
* Le attività che sfruttano Adobe Target vengono [sincronizzate con Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Puoi utilizzare questo motore quando hai [integrato con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

## Come impostare contenuti personalizzati {#how-to-setup-personalized-content}

Sono necessari vari passaggi e definizioni per la distribuzione dei contenuti personalizzati:

1. Imposta il motore di destinazione effettuando una delle seguenti operazioni:

   1. Configurazione [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md)
   1. Integrazione con [Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)

1. Configura i tipi di pubblico.

   1. A seconda del motore di destinazione, definisci le [Pubblico di destinazione](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) o [Segmento ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md), insieme alle regole.

1. Crea il tuo [Marchio e attività](/help/sites-cloud/authoring/personalization/activities.md).

1. Crea la selezione delle esperienze da mostrare ai vari tipi di pubblico.

1. Personalizza queste esperienze, per [targeting](/help/sites-cloud/authoring/personalization/targeted-content.md) per tipi di pubblico specifici (segmenti).