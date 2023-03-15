---
title: Estensione [!DNL Adobe Experience Manager] as a Cloud Service con Adobe Developer App Builder.
description: Estensione [!DNL Adobe Experience Manager] as a Cloud Service con Adobe Developer App Builder.
exl-id: 50d82745-5deb-4bfa-961b-714842403601
source-git-commit: a14ee350b3fdc3ac197b703aa36957d1d1dd7355
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Estensione [!DNL Adobe Experience Manager] as a Cloud Service con Adobe Developer App Builder {#extend-using-app-builder}

## Cos’è App Builder per AEM as a Cloud Service {#project-appbuilder}

Il nuovo Adobe Developer App Builder fornisce un framework di estensibilità per uno sviluppatore per estendere facilmente AEM funzionalità as a Cloud Service.

App Builder fornisce un framework di estensibilità unificato di terze parti per l’integrazione e la creazione di esperienze personalizzate che estendono Adobe Experience Manager. Con questo framework di estensibilità completo, basato sull’infrastruttura di Adobe, gli sviluppatori possono creare microservizi personalizzati, estendere e integrare Adobe Experience Manager tra le soluzioni di Adobe e il resto dello stack IT.

App Builder consente ai clienti di estendere facilmente Adobe Experience Manager in vari casi d’uso:

* Estensibilità middleware: connette i sistemi esterni con le applicazioni Adobe creando connettori personalizzati o sfrutta una suite di integrazioni predefinite.
* Estensibilità servizi di base : estende le funzionalità delle applicazioni di base estendendo il comportamento predefinito con funzioni personalizzate e logica di business.
* Estensibilità dell’esperienza utente : estende l’esperienza di base per supportare i requisiti aziendali o creare proprietà digitali, vetrine e app back-office specifiche per i clienti.

App Builder è disponibile per clienti e partner aziendali tramite la nostra anteprima per sviluppatori dall’estate 2020. La disponibilità generale (GA) di App Builder è prevista per dicembre 2021. Gli sviluppatori possono provare App Builder tramite la nostra [Programma di prova](https://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> Per i clienti AEM 6.5 che desiderano sfruttare l&#39;App Builder, visita [Estensione di Adobe Experience Manager 6.5 tramite Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Architettura {#architecture}

Invece di una soluzione standard, Adobe Developer App Builder fornisce una piattaforma di sviluppo comune, coerente e standardizzata per l’estensione delle soluzioni Adobe Cloud, come AEM, che include:

* Console Adobe Developer : per lo sviluppo di microservizi ed estensioni personalizzati, gli sviluppatori possono creare e gestire progetti accedendo a tutti gli strumenti e le API necessari per creare plug-in e integrazioni.
* Strumenti per sviluppatori: strumenti open-source, SDK e librerie per consentire agli sviluppatori di creare facilmente estensioni e integrazioni personalizzate. Utilizza React Spectrum (toolkit per l’interfaccia utente di Adobe) per avere un’interfaccia utente comune per tutte le app di Adobe.
* Servizi: I/O Runtime per l&#39;hosting di infrastrutture sulla piattaforma senza server ed eventi I/O per integrazioni basate su eventi. Offriamo inoltre supporto integrato per la memorizzazione di dati e file.
* Adobe Experience Cloud: gli sviluppatori possono inviare estensioni e integrazioni da pubblicare nell’organizzazione Experience Cloud. Gli amministratori di sistema possono quindi rivedere, gestire e approvare queste estensioni. Una volta pubblicato, le estensioni e gli strumenti personalizzati di App Builder si trovano accanto ad altre app Adobe Experience Cloud.

Il diagramma seguente illustra come un’applicazione standard creata con App Builder sfrutta queste funzionalità:

![Architettura](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

Per ulteriori dettagli sull’architettura di App Builder, consulta [Panoramica dell’architettura](https://www.adobe.io/app-builder/docs/guides/).

## Guida introduttiva ad App Builder {#additional-resources}

Per aiutarti a iniziare con App Builder, abbiamo creato una serie di documentazione per aiutarti a iniziare:

* [Guida introduttiva di App Builder](https://www.adobe.io/app-builder/docs/getting_started/)

## Continua a imparare con la documentazione {#appbuilder-documentation}

App Builder fornisce video e documentazione per gli sviluppatori, incluse guide e documentazione di riferimento, per aiutarti a iniziare a sviluppare applicazioni personalizzate:

* [Documentazione di App Builder](https://www.adobe.io/app-builder/docs/overview/)
* [Video di App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Provare una delle applicazioni di esempio {#appbuilder-codesamples}

Pronti per iniziare lo sviluppo? Sono disponibili numerose applicazioni di esempio per aiutarti a procedere rapidamente:

* [Labs di codice di App Builder sul sito web Adobe Developer](https://www.adobe.io/app-builder/docs/resources/)