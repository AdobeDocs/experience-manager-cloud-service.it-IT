---
title: Personalizzazione e targeting dei contenuti
description: Scopri in che modo AEM può creare contenuti personalizzati
exl-id: b9b5dbf6-d491-48a6-99b1-19bc1b651b8c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '518'
ht-degree: 100%

---

# Personalizzazione e targeting dei contenuti {#personalization}

## Personalizzazione e targeting dei contenuti {#personalization-and-content-targeting}

AEM fornisce un set di strumenti per la creazione e modifica di contenuti con destinazione e la presentazione di esperienze personali.

## Modalità di targeting {#targeting-mode}

[Puoi creare contenuti mirati (di destinazione) utilizzando la modalità di targeting di AEM. ](/help/sites-cloud/authoring/personalization/targeted-content.md) La modalità di targeting e i componenti di destinazione forniscono gli strumenti per la creazione di contenuti per le esperienze delle vostre attività di marketing.

## Attività {#activities}

Le attività definiscono e organizzano le iniziative di marketing. Le attività comprendono il pubblico di destinazione e il periodo di tempo in cui il targeting viene applicato.

Ad esempio, il catalogo dei prodotti potrebbe includere teaser che focalizzano l’attenzione sui prodotti stagionali. L&#39;attività &quot;Sports estivi&quot; definisce i segmenti di mercato a cui i teaser si rivolgono durante i mesi estivi.

Le attività identificano anche il [motore di destinazione](#targeting-engine) utilizzato dalle tue pagine.

Usa la [console Attività](/help/sites-cloud/authoring/personalization/activities.md) per creare e gestire le attività dei tuoi marchi. Puoi anche creare delle attività mentre [realizzi contenuti mirati](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Esperienze {#experiences}

Per ogni attività, definisci una o più esperienze che identificano il pubblico di destinazione. AEM ti consente di controllare il contenuto che comprende ogni esperienza.

La definizione del pubblico si basa sulla segmentazione del mercato creata con AEM o Adobe Target. Quando un visitatore apre una pagina web, la logica della pagina determina a che tipo di pubblico appartiene e visualizza il contenuto che hai creato per quel pubblico.

Ad esempio, un&#39;attività definisce le esperienze per due segmenti di pubblico distinti: le donne over 30 anni e le donne under 30 anni. La pagina Donne di un sito web potrebbe mostrare prodotti diversi per ogni esperienza.

È possibile definire le esperienze per un&#39;attività. Usa la [console Attività](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) o la [modalità Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) per aggiungere le esperienze a un&#39;attività.

## Offerte {#offers}

Un&#39;offerta è un contenuto visualizzato in una certa ubicazione della pagina per una certa esperienza. Utilizza offerte diverse per le diverse esperienze e massimizza l&#39;efficacia dei contenuti per il tuo pubblico.

Ad esempio, la pagina Donne di un sito web di esempio utilizza le offerte come immagini teaser che appaiono nella parte superiore della pagina. Le offerte utilizzate come teaser sono diverse per l&#39;esperienza Donna Over 30 e per l&#39;esperienza Donna Under 30.

Usa la [console Offerte](/help/sites-cloud/authoring/personalization/offers.md) per creare offerte da utilizzare in più esperienze. Crea le offerte per un uso singolo o aggiungi le offerte da una libreria di offerte durante la [creazione di contenuti personalizzati](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Motore di destinazione {#targeting-engine}

Il motore di destinazione è il meccanismo che definisce la logica per la creazione dei contenuti mirati. Le [Attività](/help/sites-cloud/authoring/personalization/activities.md) sono configurate per l&#39;utilizzo di uno di due motori di targeting a tua disposizione: AEM e Adobe Target.

### AEM {#aem}

AEM fornisce un motore di destinazione integrato che elabora le richieste delle pagine e determina il contenuto da visualizzare. Quando utilizzi il motore di destinazione AEM, puoi usare solo i segmenti creati con AEM per definire il pubblico delle esperienze.

### Adobe Target {#adobe-target}

Il motore di destinazione Adobe Target permette di tenere traccia e raccogliere le informazioni sulle visite della pagina.

* Con questo motore di destinazione, si utilizzano i segmenti importati da Adobe Target per definire il pubblico delle esperienze.
* Le attività che sfruttano Adobe Target vengono [sincronizzate con Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Puoi usare questo motore dopo aver eseguito l’integrazione con Adobe Target. <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
