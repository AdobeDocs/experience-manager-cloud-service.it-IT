---
title: Come collegare un database a [!DNL AEM Forms] as a Cloud Service?
seo-title: AEM Forms Data Integration
description: È possibile recuperare e salvare i dati in servizi web RESTful, servizi web basati su SOAP e servizi OData da [!DNL AEM Forms] as a Cloud Service. Il servizio fornisce uno strumento dedicato per recuperare, testare, convalidare e inviare dati a vari tipi di origini dati.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# Collegare le origini dati al Cloud Service {#aem-forms-data-integration}

![Integrazione dei dati](do-not-localize/data-integeration.png)

Le infrastrutture aziendali includono diversi sistemi back-end o origini dati come database, servizi web, servizi REST, servizi OData e soluzioni CRM. Insieme, creano un sistema informativo che distribuisce i dati alle applicazioni aziendali per eseguire attività quotidiane. D&#39;altro canto, le applicazioni acquisiscono i dati e li inviano nuovamente per aggiornare le origini dati.

[!DNL AEM Forms] applicazioni come Adaptive Forms e comunicazioni interattive richiedono l&#39;integrazione con le origini dati per recuperare i dati dei clienti durante il rendering dei moduli e la creazione di comunicazioni interattive. Ci sono casi d&#39;uso in cui i dati vengono recuperati da origini dati in base agli input dell&#39;utente in Adaptive Forms. Inoltre, i dati del modulo adattivo inviati possono essere riscritti per aggiornare le rispettive origini dati.

Mentre un sistema modulare distribuito ha i suoi vantaggi, la sfida consiste nell&#39;integrare e creare associazioni di dati tra le origini dati. L&#39;integrazione dei dati è la chiave per un&#39;infrastruttura aziendale funzionale ed efficiente con diverse fonti di dati collegate alle applicazioni per lo scambio di dati aziendali.

## Panoramica sull’integrazione dei dati {#data-integration-overview}

![integrazione aem-forms-data-data](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] L&#39;integrazione dei dati consente di configurare e collegare diverse origini dati con [!DNL AEM Forms]. Offre un’interfaccia utente intuitiva per creare uno schema di rappresentazione dei dati unificato di entità e servizi aziendali tra origini dati collegate. La rappresentazione unificata è nota come modello di dati modulo, un&#39;estensione dello schema JSON. Le entità in un modello dati modulo sono definite oggetti modello dati. Un modello dati modulo consente di:

* Accedere a oggetti, proprietà e servizi del modello dati da origini dati connesse.
* Creazione di oggetti e proprietà del modello dati personalizzato
* Creare associazioni tra oggetti del modello dati all’interno e tra origini dati.
* Richiamare i servizi oggetti del modello dati per eseguire query o scrivere dati da e verso origini dati.

Una volta creato un modello dati del modulo, è possibile utilizzarlo in vari flussi di lavoro Moduli adattivi e comunicazioni interattive, ad esempio:

* Creare comunicazioni adattive per Forms e interattive basate sul modello di dati del modulo
* Precompilazione di comunicazioni adattive Forms e interattive da origini dati configurate
* Richiamare servizi/operazioni dell’origine dati utilizzando le regole del modulo adattivo
* Scrittura dei dati del modulo adattivo inviati alle origini dati

## Guida introduttiva all’integrazione dei dati {#get-started-with-data-integration}

Il primo passo per implementare l’integrazione dei dati è identificare e configurare le origini dati che memorizzano le informazioni che desideri sfruttare nei casi di utilizzo di Adattivo Forms e nelle comunicazioni interattive. Successivamente, si crea un modello dati modulo che utilizza oggetti modello dati, proprietà e servizi provenienti da una o più origini dati. È possibile creare comunicazioni adattive Forms e interattive basate su un modello di dati modulo in cui i campi o i segnaposto Modulo adattivo nelle comunicazioni interattive sono associati alle rispettive proprietà dell’origine dati.

[!DNL AEM Forms] consente inoltre di creare un modello dati modulo indipendente dalle origini dati e di associare o eseguire il binding degli oggetti e delle proprietà del modello dati modulo con un’origine dati in un secondo momento. Elimina tutte le dipendenze dalle origini dati mentre si lavora su un modello dati modulo.

Consulta i seguenti argomenti per iniziare, comprendere e implementare l’integrazione dei dati.

* [Configurare origini dati](configure-data-sources.md)
* [Crea modello dati modulo](create-form-data-models.md)
* [Utilizzare il modello dati del modulo](work-with-form-data-model.md)
* [Utilizzare il modello dati del modulo](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] non supporta il database relazionale.
