---
title: Come connettere un database a [!DNL AEM Forms] as a Cloud Service?
seo-title: AEM Forms Data Integration
description: È possibile recuperare e salvare dati in servizi Web RESTful, servizi Web basati su SOAP e servizi OData da [!DNL AEM Forms] as a Cloud Service. Il servizio fornisce uno strumento dedicato per recuperare, testare, convalidare e inviare dati a vari tipi di origini dati.
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 3%

---

# Collegare le origini dati al Cloud Service {#aem-forms-data-integration}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html) |
| AEM as a Cloud Service | Questo articolo |


![Integrazione dei dati](do-not-localize/data-integeration.png)

L&#39;infrastruttura aziendale include diversi sistemi back-end o origini dati come database, servizi Web, servizi REST, servizi OData e soluzioni CRM. Insieme, creano un sistema di informazioni che fornisce dati alle applicazioni aziendali per eseguire le attività quotidiane. D&#39;altra parte, le applicazioni acquisiscono i dati e li inviano ad aggiornare le origini dati.

[!DNL AEM Forms] applicazioni come Adaptive Forms e le comunicazioni interattive richiedono l’integrazione con le origini dati per recuperare i dati dei clienti durante il rendering dei moduli e la creazione di comunicazioni interattive. In alcuni casi i dati vengono recuperati da origini dati in base agli input dell’utente in Adaptive Forms. Inoltre, i dati del modulo adattivo inviati possono essere riscritti per aggiornare le rispettive origini dati.

Anche se un sistema modulare distribuito ha i propri vantaggi, la sfida consiste nell’integrare e creare associazioni di dati tra diverse origini dati. L&#39;integrazione dei dati è la chiave di un&#39;infrastruttura aziendale funzionale ed efficiente con diverse origini dati collegate alle applicazioni per lo scambio di dati aziendali.

## Panoramica sull’integrazione dei dati {#data-integration-overview}

![aem-forms-data-integer](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] L’integrazione dei dati consente di configurare e collegare diverse origini dati con [!DNL AEM Forms]. Fornisce un’interfaccia utente intuitiva per creare uno schema unificato di rappresentazione dei dati di entità business e servizi tra origini dati connesse. La rappresentazione unificata è nota come modello di dati del modulo, un’estensione dello schema JSON. Le entità in un modello dati modulo sono denominate oggetti modello dati. Un modello dati modulo consente di:

* Accesso a oggetti, proprietà e servizi del modello dati da origini dati connesse.
* Creare oggetti e proprietà del modello dati personalizzato
* Creare associazioni tra oggetti modello dati all’interno e tra origini dati.
* Richiama i servizi oggetto modello dati per eseguire query o scrivere dati da e verso origini dati.

Dopo aver creato un modello di dati modulo, puoi utilizzarlo in vari flussi di lavoro per moduli adattivi e comunicazioni interattive, ad esempio:

* Creare Forms adattivo e comunicazioni interattive basate sul modello di dati del modulo
* Precompila Forms adattivo e comunicazioni interattive da origini dati configurate
* Richiama servizi/operazioni dell’origine dati tramite le regole del modulo adattivo
* Scrivere i dati del modulo adattivo inviati nelle origini dati

## Introduzione all’integrazione dei dati {#get-started-with-data-integration}

Il primo passaggio per implementare l’integrazione dei dati consiste nell’identificare e configurare le origini dati in cui sono memorizzate le informazioni che desideri utilizzare nei casi di utilizzo di Adaptive Forms e delle comunicazioni interattive. Successivamente, verrà creato un modello dati modulo che utilizza oggetti, proprietà e servizi del modello dati da una o più origini dati. Puoi creare Forms adattivo e comunicazioni interattive basate su un modello dati modulo in cui i campi o i segnaposto di Moduli adattivi nelle comunicazioni interattive sono associati alle rispettive proprietà dell’origine dati.

[!DNL AEM Forms] consente inoltre di creare un modello dati modulo indipendente dalle origini dati e di associare o associare in un secondo momento gli oggetti e le proprietà del modello dati modulo all’origine dati. Elimina tutte le dipendenze dalle origini dati mentre si lavora su un modello dati modulo.

Consulta quanto segue per iniziare, comprendere e implementare l’integrazione dei dati.

* [Configurare origini dati](configure-data-sources.md)
* [Crea modello dati modulo](create-form-data-models.md)
* [Utilizzare il modello dati del modulo](work-with-form-data-model.md)
* [Usa modello dati modulo](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] non supporta il database relazionale.
