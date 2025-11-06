---
title: Test funzionali
description: Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service per garantire la qualità e l’affidabilità del codice.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 5%

---


# Introduzione {#functional-testing-introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Test funzionali"
>abstract="Scopri i tre diversi tipi di test funzionali integrati nel processo di distribuzione di AEM as a Cloud Service. I test garantiscono la qualità e l’affidabilità del codice."

Scopri i gate di qualità disponibili nel [processo di distribuzione di AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) e i vari tipi di test funzionali incorporati. Scopri come contribuire e ottimizzarne l’utilizzo nel quadro di una strategia di test completa.

## Informazioni sui test funzionali

Il diagramma seguente fornisce una panoramica di alto livello delle pipeline disponibili nel contesto di una strategia complessiva di test e del [processo di distribuzione di AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md).

![Gate di qualità dell&#39;implementazione di AEM Cloud Service](assets/functional-testing/quality-gates-compact.svg)

## Scopo dei test funzionali

Lo scopo delle pipeline di implementazione di AEM Cloud Service è facilitare implementazioni solide e sicure in varie fasi dello sviluppo e del ciclo di vita del rilascio del prodotto AEM. Queste pipeline incorporano più gate di qualità a diversi livelli per garantire l’integrità e la sicurezza delle distribuzioni sia per le modifiche dell’applicazione AEM che per gli aggiornamenti dei prodotti AEM.

Adobe fornisce diversi gate di qualità incorporati, mentre altri richiedono il tuo intervento per l’implementazione e la configurazione. Questi gate di qualità sono versatili e si applicano in varie fasi del ciclo di vita, integrandosi direttamente nella configurazione di sviluppo e nei processi CI/CD.

I gate di qualità incorporati convalidano principalmente la funzionalità del prodotto AEM nel contesto dell’applicazione AEM. Al contrario, i gate di qualità personalizzati configurati sono progettati per verificare che le funzioni critiche e le interazioni dell’utente dell’applicazione funzionino come previsto. Collettivamente, questi due set di gate di qualità collaborano per garantire implementazioni automatizzate solide e sicure sia per le modifiche al codice che per gli aggiornamenti dei prodotti AEM.

È importante notare che questi gate di qualità non sono destinati a essere un framework di test completo per l’intera strategia di test. Il prodotto AEM è sottoposto a test approfonditi prima di entrare nel processo di distribuzione di AEM Cloud Service. Allo stesso modo, l’applicazione deve essere di alta qualità prima di raggiungere la fase di distribuzione. Questo approccio garantisce che i gate di qualità si concentrino sul loro obiettivo principale di salvaguardare il processo di implementazione, anziché sostituire un regime di test completo.

## Gate di qualità nel test

Il diagramma seguente fornisce una visualizzazione dettagliata dei gate di qualità disponibili e del loro utilizzo nella strategia complessiva di test e nel [processo di distribuzione di AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md).

![Gate di qualità dell&#39;implementazione di AEM Cloud Service](assets/functional-testing/quality-gates-overview.svg)

### Riepilogo dei gate di qualità forniti dal cliente

|                               | Test di unità | Test funzionali <br/> personalizzati | Test dell&#39;interfaccia utente <br/> personalizzati | Customer<br/> Validations | Test <br/> manuali |
|:------------------------------|:---------------------:|:-----------------------------------:|:-----------------------------------:|:-------------------------:|:-------------------:|
| **Pipeline di produzione** | Sì<br/>Blocco<br/> | Sì<br/>Timeout blocco<br/>60m | Sì<br/>Timeout blocco<br/>30m | No | No |
| **Pipeline non di produzione** | Sì<br/>Blocco<br/> | Consenso<br/>Blocco<br/>Timeout di 60m | Consenso<br/>Blocco<br/>Timeout di 30m | No | No |
| **Convalida interna Adobe** | Sì<br/>Blocco<br/> | Sì<br/>Timeout blocco<br/>60m | Sì<br/>Timeout blocco<br/>30m | No | No |
| **IC cliente/CD** | Sì | Sì | Sì | Sì | Sì |
| **Sviluppatore locale cliente** | Sì | Sì | Sì | Sì | Sì |

### Test di unità

Ti invitiamo a fornire gli unit test per l’applicazione AEM, su cui si basano tutte le strategie di test. Hanno lo scopo di essere veloci e frequenti e di fornire feedback rapidi e tempestivi. Sono strettamente integrati nei flussi di lavoro per sviluppatori, nel tuo CI/CD e nelle pipeline di implementazione di AEM Cloud Service.

Vengono implementati utilizzando JUnit e vengono eseguiti con Maven. Per un esempio di unit test per AEM e una guida introduttiva, consulta il modulo [core dell&#39;Archetipo progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/using#unit-tests).

### Qualità del codice

Questo gate di qualità è configurato come preconfigurato ed esegue l’analisi del codice statico sul codice dell’applicazione AEM.

Per ulteriori informazioni, vedere [Test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) e [Regole per la qualità del codice personalizzato](/help/implementing/cloud-manager/custom-code-quality-rules.md).

### Test del prodotto

I test funzionali del prodotto sono test stabili di integrazione HTTP (IT) per le funzionalità principali di AEM, incluse le attività di authoring e replica. Adobe li fornisce e li mantiene pronti all’uso. Hanno lo scopo di impedire la distribuzione di modifiche al codice personalizzato dell’applicazione se interrompono le funzionalità core nel prodotto AEM.

Utilizzano JUnit per l&#39;implementazione, vengono eseguiti con Maven e si basano sui [client di test AEM](https://github.com/adobe/aem-testing-clients) ufficiali. La suite di test del prodotto viene mantenuta come
un [progetto open-source](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke), segue le best practice e può essere considerato un buon punto di partenza per l&#39;implementazione dei test.

### Test funzionali personalizzati

Analogamente ai test del prodotto, i test funzionali del cliente sono test di integrazione HTTP (IT) implementati con JUnit, eseguiti con Maven e generati sui [client di test AEM](https://github.com/adobe/aem-testing-clients) ufficiali.

>[!NOTE]
>
>I test funzionali personalizzati vengono eseguiti sia nelle pipeline di produzione che in quelle non di produzione (opt-in) utilizzate per le distribuzioni di modifiche delle applicazioni AEM e per gli aggiornamenti push dei prodotti AEM. Svolgono un ruolo fondamentale nel garantire il corretto funzionamento dell’applicazione e nel migliorare la sicurezza del rilascio. I test funzionali del cliente vengono eseguiti anche in pipeline interne di convalida pre-release per ogni cliente, per fornire un feedback tempestivo.

Per mantenere efficienti le esecuzioni delle pipeline, Adobe consiglia di concentrarsi sulle funzioni chiave e sui flussi di interazione dell’utente primario, con l’obiettivo di ottenere un runtime di test funzionale di circa 15 minuti o meno. Le suite di test funzionali complete che superano questo limite di tempo devono essere eseguite come parte delle pipeline di convalida generali del cliente durante il processo di sviluppo.

Per alcuni esempi, consulta [test del prodotto open source](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) o il modulo [it.tests dell&#39;Archetipo progetti AEM](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/it.tests).

Consulta [Test funzionali Java](/help/implementing/cloud-manager/java-functional-testing.md) per ulteriori informazioni.

### Test dell’interfaccia utente personalizzati

Per massimizzare il controllo dei rischi per lo sviluppo specifico del cliente, Adobe ti incoraggia a acquisire in AEM as a Cloud Service i test critici dell’interfaccia utente. Mantenerli limitati ma focalizzati sulla massimizzazione del loro impatto sulla customer experience.

I test sono inclusi in un’immagine Docker progettata per essere il più volatile possibile (con supporto per Cypress, Playwright, Selenium, Java e JavaScript). Seguono le stesse caratteristiche e gli stessi scopi dei test funzionali personalizzati.

>[!NOTE]
>
>I test dell’interfaccia utente personalizzati vengono eseguiti sia nelle pipeline di produzione che in quelle non di produzione (opt-in) utilizzate per le distribuzioni di modifiche alle applicazioni AEM e per gli aggiornamenti push dei prodotti AEM. Sono essenziali per garantire il corretto funzionamento dell’applicazione e migliorare la sicurezza del rilascio. I test dell’interfaccia utente del cliente vengono eseguiti anche in pipeline interne di convalida pre-release per ogni cliente, per fornire un feedback tempestivo.
>
>I contenitori non Selenium devono eseguire i test utilizzando un proxy HTTP basato sulle variabili di ambiente nella [Sezione test interfaccia utente](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing).

Per mantenere efficienti le esecuzioni della pipeline, Adobe consiglia di concentrarsi sulle funzioni chiave e sui flussi di interazione dell’utente principale. Le suite di test dell’interfaccia utente complete che superano questo gate di qualità devono essere eseguite come parte delle pipeline generali di convalida dei clienti. Incorporali nel processo di sviluppo del cliente.

Per esempi, consulta [esempi open source](https://github.com/adobe/aem-test-samples/tree/aem-cloud/) o il modulo [ui.tests dell&#39;Archetipo progetti AEM](/help/implementing/cloud-manager/ui-testing.md).

Consulta [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) per ulteriori informazioni.

### Audit dell’esperienza

Il gate di qualità dell&#39;audit dell&#39;esperienza sta eseguendo [controlli Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/) sulla pagina Web del cliente.

Questo gate di qualità è fornito da AEM pronto all’uso, ma non blocca le pipeline di distribuzione. Per impostazione predefinita, viene eseguito un controllo di audit sulla pagina principale (`/`) dell&#39;istanza Publish. Puoi contribuire configurando fino a 25 percorsi personalizzati considerati per i controlli di audit.

Per ulteriori informazioni, vedere [Test di verifica dell&#39;esperienza](/help/implementing/cloud-manager/reports/report-experience-audit.md).

### Convalide cliente

Il gate di qualità delle convalide del cliente è un segnaposto per la strategia e l’impegno di test del cliente stesso, eseguiti prima che le modifiche dell’applicazione del cliente raggiungano le pipeline di implementazione cloud di AEM.

Qui puoi scegliere gli strumenti e i framework che preferisci. A differenza dei test delle funzioni dei clienti e dei test dell’interfaccia utente personalizzati, non esistono limiti relativi ad AEM as a Cloud Service. Adobe consiglia pertanto di eseguire test funzionali e dell’interfaccia utente di lunga durata qui.

Sebbene tu possa scegliere qualsiasi strumento e framework, Adobe consiglia di allineare l’integrazione basata su HTTP e i test dell’interfaccia utente con gli strumenti e i framework utilizzati nei gate di qualità dei test funzionali e dell’interfaccia utente personalizzati. Inoltre, Adobe consiglia di incorporare [Rapid Development Environments (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) nella strategia di test locale per rispecchiare da vicino gli ambienti cloud AEM.

### Test manuale

Il gate di qualità del test manuale è un segnaposto per i clienti che eseguono test manuali. Poiché le pipeline cloud di AEM non supportano i test manuali, devono essere incluse nella strategia di test locale.

Per il test manuale, può essere utile eseguire l’integrazione con un ambiente di sviluppo AEM Cloud Service aggiuntivo.
