---
title: Cefalea e senza testa in AEM
description: AEM progetti possono essere implementati in un modello headful e headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto.
translation-type: tm+mt
source-git-commit: 772717b7ad3baa17a58e251c128663035eb89931
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---


# Cuffia e testa senza testa in AEM {#headful-headless}

I progetti Adobe Experience Manager possono essere implementati sia in modelli headful che headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto. Questo documento fornisce una panoramica dei diversi modelli e descrive i livelli di integrazione SPA.

## Panoramica {#overview}

AEM offre potenti strumenti per gestire sia la creazione dei contenuti che la distribuzione in un&#39;unica piattaforma. Si tratta di un modello tradizionale di gestione dei contenuti, caratterizzato da un elevato livello di esperienza, in cui autori e sviluppatori di contenuti lavorano sulla stessa piattaforma per distribuire le esperienze ai consumatori di contenuti.

AEM può essere utilizzato anche per gestire semplicemente i contenuti, consentendo la presentazione e la distribuzione dei contenuti da parte di un&#39;altra piattaforma. Questo è il modello &quot;headless&quot; della gestione dei contenuti, in cui autori e sviluppatori di contenuti lavorano su piattaforme diverse per offrire esperienze ai consumatori di contenuti.

Ma questa non deve essere una scelta binaria. AEM offre una flessibilità senza precedenti, che consente di sfruttare i vantaggi di entrambi i modelli per il progetto.

![Modelli di implementazione AEM](headless/assets/aem-implementation-models.png)

In un modello headful o full-stack, il contenuto viene gestito nell’archivio AEM e nei componenti AEM basati su Java, HTL e così via. vengono utilizzati per eseguire il rendering del contenuto per l&#39;esperienza utente. In questo modello, creare il contenuto, formattarlo, presentarlo e distribuirlo avviene in AEM.

In un modello headless, il contenuto viene gestito nell&#39;archivio AEM, ma distribuito tramite API quali REST e GraphQL a un altro sistema per eseguire il rendering del contenuto per l&#39;esperienza utente. In questo modello, il contenuto viene creato in AEM, ma formattandolo, presentandolo e distribuendolo avviene su un&#39;altra piattaforma.

Le applicazioni per pagina singola (SPA) sono spesso la destinazione del contenuto distribuito senza problemi da AEM. Tuttavia, questi SPA non devono essere del tutto esterni ai AEM. AEM consente di decidere in che misura i SPA sono integrati in AEM. Facciamo un esempio.

## Esempio di negozio Web {#web-shop-example}

Supponiamo di avere un negozio web esistente per la vostra azienda come SPA. Contiene tutti i dettagli e le immagini del prodotto. Poi introduci AEM per potenziare le tue attività di marketing, come siti promozionali, blog e contenuti delle campagne. Come si integrano le due? AEM consente una serie di opzioni:

* **Consentire il funzionamento indipendente dei sistemi.**
* **Fornite al negozio Web contenuti limitati da AEM tramite GraphQL.** I contenuti possono essere creati dagli autori in AEM, ma solo visualizzati tramite il SPA del negozio Web.
* **Incorpora il negozio Web SPA in AEM.** I contenuti possono essere creati da autori in AEM e visualizzati in AEM nel contesto del negozio Web, ma non modificati.
* **Incorpora il SPA del negozio Web in AEM e abilita punti modificabili.** I contenuti possono essere creati da autori in AEM e visualizzati in AEM nel contesto del negozio Web, e gli autori hanno una capacità limitata di manipolare i contenuti del negozio SPA all&#39;interno di AEM.
* **Incorpora il negozio di webs SPA in AEM e abilita intere aree per la modifica.** I contenuti possono essere creati da autori in AEM e visualizzati in AEM nel contesto del negozio Web, e gli autori hanno una capacità limitata di manipolare i contenuti del negozio SPA all&#39;interno di AEM.

La sezione successiva esamina più dettagliatamente questi livelli di integrazione.

>[!NOTE]
>
>Naturalmente si potrebbe anche riimplementare il negozio web SPA come un AEM completamente funzionante SPA [utilizzando il AEM SPA Editor framework.](/help/implementing/developing/hybrid/introduction.md) Se avete già AEM e desiderate creare un nuovo negozio Web o altri SPA, questo è il metodo consigliato, ma non rientra nell&#39;ambito di questo documento.

## SPA livelli di integrazione {#integration-levels}

SPA&#39;integrazione si sviluppa su quattro livelli di AEM.

* **Livello 0: Nessuna integrazione**
   * Le SPA e AEM esistono separatamente e non scambiano informazioni.
   * I contenuti vengono creati, gestiti e distribuiti in modo indipendente in due sistemi separati.
* **Livello 1: Integrazione con i frammenti di contenuto**
   * [I ](/help/assets/content-fragments/content-fragments.md) frammenti di contenuto vengono utilizzati in AEM per creare e gestire contenuti limitati per il SPA.
   * Il SPA recupera questo contenuto tramite AEM [GraphQL API.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alcuni contenuti vengono gestiti in AEM e altri in un sistema esterno.
   * Il contenuto può essere visualizzato solo nella SPA.
* **Livello 2: Incorpora SPA in AEM**
   * [I ](/help/assets/content-fragments/content-fragments.md) frammenti di contenuto vengono utilizzati AEM per creare e gestire il contenuto per il SPA.
   * Il SPA recupera questo contenuto tramite AEM [GraphQL API.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alcuni contenuti vengono gestiti in AEM e altri in un sistema esterno.
   * Il contenuto può essere visualizzato contestualmente all’interno di AEM.
   * I contenuti limitati possono essere modificati in AEM.
* **Livello 3: Incorpora e abilita completamente SPA in AEM**
   * [I ](/help/assets/content-fragments/content-fragments.md) frammenti di contenuto vengono utilizzati AEM per creare e gestire il contenuto per il SPA.
   * Il SPA recupera questo contenuto tramite AEM [GraphQL API.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Il contenuto può essere visualizzato contestualmente all’interno di AEM.
   * La maggior parte dei contenuti può essere modificata all’interno AEM.

Il livello 1 è un esempio di implementazione senza problemi tipici. Tuttavia, gli autori dei contenuti possono visualizzare solo il contenuto contestuale all’interno del SPA. AEM è solo uno strumento di authoring.

Il vantaggio e la flessibilità di AEM diventano evidenti con i livelli 2 e 3 pur mantenendo i vantaggi di SPA. Gli autori dei contenuti possono creare i propri contenuti in AEM, ma anche visualizzarli contestualmente in AEM. Il SPA acquisisce la capacità di essere creato in AEM, ma rimane comunque distribuito come SPA.

## Implementazione dei livelli di integrazione {#implementing}

Sono disponibili diversi strumenti in AEM a seconda del livello di integrazione scelto. Ogni livello si basa sugli strumenti utilizzati in precedenza. L&#39;elenco seguente è collegato alle relative risorse.

* **Livello 1:** Frammenti di contenuto e  [AEM ](/help/implementing/developing/headless/introduction.md) framework headless possono essere utilizzati per distribuire AEM contenuto al SPA.
* **Livello 2:** Oltre al livello 1:
   * [Il ](/help/implementing/developing/hybrid/remote-page.md) componente RemotePage può essere utilizzato per incorporare il SPA esterno in AEM dove è possibile visualizzare AEM contenuto nel contesto.
   * Alcuni punti del SPA possono essere abilitati anche per [consentire modifiche limitate in AEM.](/help/implementing/developing/hybrid/editing-external-spa.md)
* **Livello 3:** Oltre al livello 2:
   * È possibile abilitare intere aree del SPA per consentire la modifica completa in AEM.
