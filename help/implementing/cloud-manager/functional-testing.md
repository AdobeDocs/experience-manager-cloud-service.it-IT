---
title: Test funzionali
description: Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 7d15440159a8e24314753acd5b37fcd2c5e8ec4c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 83%

---


# Test funzionali {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionali"
>abstract="Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice."

Scopri i tre diversi tipi di test funzionali integrati nel [processo di distribuzione di AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) per garantire la qualità e l’affidabilità del codice.

## Ambito

I passaggi dei test funzionali nella pipeline di Cloud Manager hanno lo scopo di garantire che le funzionalità essenziali dell’applicazione funzionino come previsto.

Questa fase di test è l’ultimo livello di test automatizzato prima della distribuzione del codice in produzione.

I test funzionali non devono sostituire, ma piuttosto integrare ed estendere altre strategie di test, come gli unit test, i test di integrazione o i test funzionali eseguiti al di fuori dell’esecuzione della pipeline in Cloud Manager.

## Panoramica {#overview}

AEM as a Cloud Service offre tre diversi tipi di test funzionali.

* [Test funzionali del prodotto](#product-functional-testing)
* [Test funzionali personalizzati](#custom-functional-testing)
* [Test dell’interfaccia utente personalizzati](#custom-ui-testing)

Per tutti i test funzionali, è possibile scaricare i risultati dettagliati come file `.zip` utilizzando il pulsante **Scarica registro build** nella schermata di panoramica della build come parte del [processo di distribuzione.](/help/implementing/cloud-manager/deploy-code.md)

Questi registri non includono i registri del processo di runtime effettivo di AEM. Per ulteriori informazioni su come accedere ai registri, consulta il documento [Accesso e gestione dei registri](/help/implementing/cloud-manager/manage-logs.md).

I test funzionali del prodotto e i test funzionali personalizzati di esempio sono basati sui [client di test di AEM.](https://github.com/adobe/aem-testing-clients)

### Test funzionali del prodotto {#product-functional-testing}

I test funzionali del prodotto sono una serie di test stabili di integrazione HTTP (IT) delle funzionalità principali in AEM, come le attività di authoring e replica. Questi test vengono gestiti da Adobe e hanno lo scopo di impedire la distribuzione di modifiche al codice personalizzato dell’applicazione nel caso in cui interrompano le funzionalità core.

* [Pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): i test funzionali del prodotto vengono eseguiti automaticamente ogni volta che si distribuisce un nuovo codice in Cloud Manager e non possono essere ignorati.
* [Pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): facoltativamente, è possibile selezionare i test funzionali del prodotto da eseguire ogni volta che si esegue la pipeline non di produzione.

I test vengono gestiti come progetto open source. Per ulteriori informazioni, consulta i [test funzionali del prodotto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) su GitHub.

### Test funzionali personalizzati {#custom-functional-testing}

Anche se i test funzionali del prodotto sono definiti da Adobe, puoi creare test di qualità personalizzati per la tua applicazione. Verranno eseguiti come test funzionali personalizzati nell’ambito della [pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) o facoltativamente della [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) per garantire la qualità dell’applicazione.

I test funzionali personalizzati vengono eseguiti sia per le distribuzioni del codice personalizzato sia per gli aggiornamenti push, per questo è particolarmente importante scrivere test funzionali che impediscano alle modifiche apportate al codice AEM di interrompere il codice dell’applicazione. Il passaggio dei test funzionali personalizzati è sempre presente e non può essere ignorato.

Fare riferimento a [Test funzionali Java](/help/implementing/cloud-manager/java-functional-testing.md) per ulteriori informazioni.


### Test dell’interfaccia utente personalizzati {#custom-ui-testing}

I test dell’interfaccia utente personalizzati sono una funzione facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni. I test dell’interfaccia utente sono test basati su Selenium assemblati in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium.

Fare riferimento a [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) per ulteriori informazioni.

