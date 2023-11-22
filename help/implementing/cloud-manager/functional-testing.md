---
title: Test funzionali
description: Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 181a0fd3097e1af2c432afbd8d2a170d792918be
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 10%

---


# Introduzione {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionali"
>abstract="Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice."

Scopri i gate di qualità disponibili nella sezione [Processo di implementazione as a Cloud Service dell’AEM](/help/implementing/cloud-manager/deploy-code.md), i diversi tipi di test funzionali incorporati, come contribuire e come utilizzarli al meglio nel contesto di una strategia di test globale.

## Panoramica

Il diagramma seguente fornisce una panoramica di alto livello delle pipeline disponibili nel contesto di una strategia di test complessiva e [Processo di implementazione as a Cloud Service dell’AEM](/help/implementing/cloud-manager/deploy-code.md).

![gate di qualità dell’implementazione di AEM Cloud Service](assets/functional-testing/quality-gates-compact.svg)

## Scopo

Lo scopo delle pipeline di distribuzione di AEM Cloud Service è facilitare distribuzioni solide e sicure in varie fasi dello sviluppo e del ciclo di vita del rilascio del prodotto AEM. Queste pipeline incorporano più gate di qualità a diversi livelli per garantire l’integrità e la sicurezza delle distribuzioni sia per le modifiche dell’applicazione AEM che per gli aggiornamenti dei prodotti AEM.

Adobe fornisce diversi gate di qualità incorporati, mentre altri richiedono il tuo intervento per l’implementazione e la configurazione. Questi gate di qualità sono versatili, alcuni sono applicabili in varie fasi del ciclo di vita e persino integrabili nella tua configurazione di sviluppo e nei processi CI/CD.

I gate di qualità incorporati convalidano principalmente la funzionalità del prodotto AEM nel contesto dell’applicazione AEM. Al contrario, i gate di qualità personalizzati configurati sono progettati per verificare che le funzioni critiche e le interazioni dell’utente dell’applicazione funzionino come previsto. Collettivamente, questi due set di gate di qualità collaborano per garantire implementazioni automatizzate solide e sicure sia per le modifiche al codice che per gli aggiornamenti dei prodotti AEM.

È importante notare che questi gate di qualità non sono destinati a essere un framework di test completo per l’intera strategia di test. Il prodotto AEM è sottoposto a test approfonditi prima di entrare nel processo di implementazione del servizio cloud AEM. Allo stesso modo, l’applicazione deve essere di alta qualità prima di raggiungere la fase di distribuzione. Questo approccio garantisce che i gate di qualità si concentrino sul loro obiettivo principale di salvaguardare il processo di implementazione, anziché sostituire un regime di test completo.

## Gate di qualità

Il diagramma seguente fornisce una panoramica dettagliata dei gate di qualità disponibili e del loro utilizzo nella strategia complessiva di test e nella [Processo di implementazione as a Cloud Service dell’AEM](/help/implementing/cloud-manager/deploy-code.md).

![gate di qualità dell’implementazione di AEM Cloud Service](assets/functional-testing/quality-gates-overview.svg)

### Riepilogo dei gate di qualità forniti dal cliente

|                               | Test di unità | Personalizzato<br/> Test funzionali | Personalizzato<br/> Test dell’interfaccia utente | Cliente<br/> Convalide | Manuale<br/> Test |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Pipeline di produzione** | Sì<br/>Blocco<br/> | Sì<br/>Blocco<br/>Timeout 60 m | Sì<br/>Blocco<br/>Timeout 60 m | No | No |
| **Pipeline non di produzione** | Sì<br/>Blocco<br/> | Opt-in<br/>Blocco<br/>Timeout 60 m | Opt-in<br/>Blocco<br/>Timeout 60 m | No | No |
| **Adobe di convalida interna** | Sì<br/>Blocco<br/> | Sì<br/>Blocco<br/>Timeout 60 m | Sì<br/>Blocco<br/>Timeout 60 m | No | No |
| **CI/CD cliente** | Sì | Sì | Sì | Sì | Sì |
| **Sviluppatore locale del cliente** | Sì | Sì | Sì | Sì | Sì |

### Test di unità

Ti invitiamo a fornire gli unit test per l’applicazione AEM, su cui si basa ogni strategia di test. Hanno lo scopo di essere veloci e frequenti e di fornire feedback rapidi e tempestivi. Sono strettamente integrati nei flussi di lavoro per sviluppatori, nel tuo CI/CD e nelle pipeline di implementazione del servizio cloud AEM.

Vengono implementati utilizzando JUnit e vengono eseguiti con Maven. Consulta la sezione
[modulo core del progetto Archetipo AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/core.html#unit-tests)
ad esempio, unit test per AEM e guida introduttiva.

### Qualità del codice

Questo gate di qualità è configurato come preconfigurato ed esegue l’analisi del codice statico sul codice dell’applicazione AEM.

Consulta [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) e
[Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md) per ulteriori informazioni.

### Test del prodotto

I test funzionali del prodotto sono una serie di test stabili di integrazione HTTP (IT) delle funzionalità principali in AEM, come le attività di authoring e replica. Adobe li fornisce e li mantiene pronti all’uso. Queste misure hanno lo scopo di impedire l’implementazione di modifiche al codice personalizzato dell’applicazione nel caso in cui interrompano le funzionalità principali del prodotto AEM.

Vengono implementati utilizzando Junit, vengono eseguiti utilizzando Maven e fanno uso del [Client di test AEM](https://github.com/adobe/aem-testing-clients).
La suite di test del prodotto viene mantenuta come [progetto open-source](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke), segue le best practice e può essere considerato un buon punto di partenza per l’implementazione dei test.

### Test funzionali personalizzati

Come i test del prodotto, i test funzionali del cliente sono test di integrazione HTTP (IT) e sono anche implementati utilizzando Junit, vengono eseguiti utilizzando Maven e costruiti sul server ufficiale [Client di test AEM](https://github.com/adobe/aem-testing-clients).

>[!NOTE]
>
>I test funzionali personalizzati vengono eseguiti nelle pipeline di produzione e non di produzione (opt-in) utilizzate dalle modifiche dell’applicazione AEM, dalle implementazioni e dagli aggiornamenti push dei prodotti AEM e rappresentano pertanto un contributo chiave per garantire il corretto funzionamento dell’applicazione e aumentare la sicurezza della versione.
>I test funzionali del cliente vengono eseguiti anche in pipeline interne di convalida pre-release per ogni cliente, per fornire un feedback tempestivo.

Per mantenere efficienti le esecuzioni della pipeline, consigliamo di concentrarci sulle funzioni chiave e sui principali flussi di interazione degli utenti.
Si consiglia un tempo di esecuzione di circa 15 minuti o meno per i test funzionali. Si consiglia di eseguire suite di test funzionali complete che non rientrano in questo gate di qualità come parte delle pipeline di convalida generali del cliente durante il flusso di sviluppo del cliente.

Consulta la sezione [test di prodotto open source](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) o
[Modulo it.tests di Archetipo progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/ittests.html)
ad esempio.

Consulta [Test funzionali Java](/help/implementing/cloud-manager/java-functional-testing.md) per ulteriori informazioni.

### Test interfaccia utente personalizzati

Per massimizzare il controllo dei rischi per lo sviluppo specifico del cliente, Adobe consiglia vivamente di acquisire in AEMCS i test critici dell’interfaccia utente. L’obiettivo è mantenerli in numero piuttosto limitato, ma con il massimo impatto sulla customer experience.

I test sono inclusi in un’immagine Docker, progettata per essere il più volatile possibile (con supporto per Cypress, Selenium, Java, Java, Java, ecc.). Seguono le stesse caratteristiche e gli stessi scopi dei test funzionali personalizzati.

>[!NOTE]
>
>I test personalizzati dell’interfaccia utente vengono eseguiti nelle pipeline di produzione e non di produzione (opt-in) utilizzate dalle modifiche dell’applicazione AEM, dalle implementazioni e dagli aggiornamenti push dei prodotti AEM e rappresentano pertanto un contributo chiave per garantire il corretto funzionamento dell’applicazione e aumentare la sicurezza della versione.
>I test dell’interfaccia utente del cliente vengono eseguiti anche in pipeline interne di convalida pre-release per ogni cliente, per fornire un feedback tempestivo.

Per mantenere efficienti le esecuzioni della pipeline, consigliamo di concentrarci sulle funzioni chiave e sui principali flussi di interazione degli utenti.
Si consiglia di eseguire suite di test dell’interfaccia utente complete che non rientrano in questo gate di qualità come parte delle pipeline di convalida generali del cliente durante il flusso di sviluppo del cliente.

Consulta la sezione [esempi di test open source](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) o
[Modulo ui.tests di Archetipo progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uitests.html)
ad esempio.

Consulta [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) per ulteriori informazioni.

### Audit dell’esperienza

Il gate di qualità dell’audit dell’esperienza sta eseguendo [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/)
controlli di audit sulla pagina web del cliente.

Questo gate di qualità è fornito da AEM predefinito, ma non blocca le pipeline di distribuzione. Per impostazione predefinita, un controllo di audit sulla pagina principale (`/`) dell&#39;istanza Publish. Puoi contribuire configurando fino a 25 percorsi personalizzati considerati per i controlli di audit.

Consulta [Test di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md)
per ulteriori informazioni.

### Convalide cliente

Il gate di qualità delle convalide del cliente è un segnaposto per la strategia e l’impegno di test del cliente stesso, eseguiti prima che le modifiche dell’applicazione del cliente raggiungano le pipeline di implementazione cloud dell’AEM.

Qui puoi, ovviamente, scegliere gli strumenti e i framework che preferisci. A differenza dei test delle funzioni dei clienti e dei test dell’interfaccia utente personalizzati, non esistono limiti correlati all’AEM as a Cloud Service e pertanto consigliamo di eseguire qui test funzionali e dell’interfaccia utente di lunga durata.

Anche se sei libero di scegliere qualsiasi strumento e framework, ti consigliamo di allineare i test di integrazione e i test dell’interfaccia utente basati su HTTP con gli strumenti e i framework disponibili nei test funzionali personalizzati e nei gate di qualità dei test dell’interfaccia utente personalizzati.
Si consiglia di integrare
[Ambienti di sviluppo rapido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md)
nella tua strategia di test locale per eseguire test il più vicino possibile agli ambienti cloud AEM.

### Test manuale

Il gate di qualità del test manuale è un segnaposto per i clienti che eseguono test manuali. Le pipeline cloud AEM non supportano i test manuali, pertanto questo deve accadere come parte della tua strategia di test locale.

Per il test manuale, può essere utile eseguire l’integrazione con un ambiente di sviluppo AEM Cloud Service aggiuntivo.
