---
title: Come creare moduli in AEM?
description: Scopri di più sulle varie piattaforme di creazione dei moduli disponibili in Adobe Experience Manager (AEM) e come scegliere quella giusta in base alle tue esigenze.
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
exl-id: bd9cb623-c272-4cdf-ad39-f97043f781a6
hide: true
hidefromToC: true
source-git-commit: 1662d1c9458f05c2e511514ce8a04247da90eaf3
workflow-type: ht
source-wordcount: '1075'
ht-degree: 100%

---

# Come creare moduli in Adobe Experience Manager (AEM)?

Adobe Experience Manager (AEM) fornisce una piattaforma flessibile per la creazione di moduli coinvolgenti, reattivi, dinamici e adattivi. Offre un’interfaccia utente intuitiva e un set completo di componenti pronti all’uso per la creazione e la gestione di moduli adattivi. I moduli possono essere creati con o senza un modello di modulo o uno schema, a seconda dei requisiti.

## Considerazioni chiave per la scelta di una piattaforma di authoring

AEM fornisce più opzioni di authoring per la creazione di moduli interattivi e coinvolgenti. Quando selezioni un ambiente di authoring di moduli, tieni presente i fattori seguenti:

| 📝 **Considerazione** | 💡 **Che cosa chiedere** |
|----------------------|--------------------|
| **Competenze utente** | Chi creerà i moduli: sviluppatori, utenti aziendali o autori di contenuti? |
| **Complessità del modulo** | Il modulo richiede regole avanzate, sezioni dinamiche o integrazioni? |
| **Esigenze di riutilizzabilità** | Parti del modulo verranno riutilizzate in diversi moduli o progetti? |
| **Flessibilità di progettazione** | Hai bisogno di un controllo completo su layout, temi e stile? |
| **Requisiti di integrazione** | Il modulo deve connettersi a modelli di dati, flussi di lavoro o sistemi esterni? |
| **Facilità d’uso** | La piattaforma è intuitiva per il livello di competenze tecniche del team? |
| **Prestazioni e scalabilità** | Il modulo verrà utilizzato su larga scala o in ambienti con traffico elevato? |
| **Consegna omnicanale** | Il modulo verrà utilizzato su siti web, app mobili, chioschi o più canali? |
| **Flessibilità di pubblicazione** | Dove verranno pubblicati i moduli su AEM, Edge Delivery o app personalizzate? |

## Panoramica dei metodi di authoring dei moduli in AEM

AEM supporta più metodi di authoring, ciascuno adatto a esigenze utente, livelli di competenza tecnica e destinazioni di pubblicazione diversi.

* [Componenti di base](/help/forms/create-adaptive-form-tutorial.md): utilizza componenti di base per creare moduli interattivi tradizionali. Ideale per moduli che si integrano con i sistemi precedenti o si basano su flussi di lavoro consolidati. I moduli creati con i componenti di base possono essere pubblicati solo su AEM e non sono compatibili con Edge Delivery Services.

* [Componenti core](/help/forms/creating-adaptive-form-core-components.md): utilizza i componenti core per creare moduli moderni, reattivi e scalabili. Supportano la riutilizzabilità, l’accessibilità e prestazioni migliori. I moduli creati con i componenti core possono essere pubblicati sia su AEM che Edge Delivery Services, offrendo flessibilità su più piattaforme.

* [Moduli Edge Delivery Services](/help/edge/docs/forms/overview.md): i moduli Edge Delivery Services trasformano il modo in cui i moduli vengono creati, eseguiti ed elaborati. Sfruttando Edge Delivery Services, le organizzazioni possono creare moduli digitali veloci, sicuri e altamente disponibili, migliorando l’esperienza utente e l’efficienza operativa con un ambiente di sviluppo rapido. Puoi creare moduli Edge Delivery Services in due modi:
   * [Authoring WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): utilizza l’editor universale per la creazione di moduli visivi e con metodo di trascinamento, ideale per autori di contenuti con conoscenze tecniche limitate. I moduli creati con l’editor universale vengono forniti con Edge Delivery Services per un rendering rapido e semplice.
   * [Authoring basato su documenti](/help/edge/docs/forms/tutorial.md): utilizza strumenti come Microsoft Excel o Fogli Google per definire la struttura del modulo e il contenuto. Questo metodo è utile per gli utenti aziendali che preferiscono un input basato su fogli di calcolo. Questi moduli vengono generalmente pubblicati tramite Edge Delivery Services e sono adatti per casi d’uso semplici e a volume elevato.
* [Authoring headless](https://experienceleague.adobe.com/it/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service): utilizza le API per eseguire il rendering dei moduli come JSON per qualsiasi front-end, ad esempio React, Angular, app mobili o chioschi, senza dipendere da AEM. Attualmente, solo i componenti core supportano la consegna headless. I moduli headless sono ideali per casi di utilizzo omnicanale e vengono utilizzati indipendentemente dal rendering delle pagine di AEM, rendendoli flessibili per le distribuzioni front-end personalizzate.

### Analisi comparativa dei metodi di authoring dei moduli di AEM

La tabella seguente offre un breve confronto tra vari metodi di authoring dei moduli di AEM, evidenziando gli approcci, le funzioni, le opzioni di pubblicazione e i casi d’uso ideali per aiutare a scegliere il metodo più adatto alle tue esigenze.

| **Valutazione** | **Componenti di base** | **Componenti core** | **Editor universale (WYSIWYG)** | **Authoring basato su documenti** | **Authoring headless** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Ideale per** | Manutenzione dei moduli e flussi di lavoro precedenti in AEM | Moduli scalabili e moderni con flussi di lavoro e integrazioni complessi | Creazione di moduli per siti di Edge Delivery Service con requisiti complessi | Creazione rapida di prototipi o moduli di base senza servizi di invio avanzati | Esperienze omnicanale tra piattaforme (web, dispositivi mobili, chioschi, ecc.) |
| **Competenze utente** | Sviluppatori, autori dei contenuti | Sviluppatori, autori avanzati | Utenti aziendali, autori di contenuti | Utenti aziendali | Sviluppatori |
| **Complessità del modulo** | Moduli di base | Moduli complessi con sezioni dinamiche | Moduli complessi con azioni personalizzate | Moduli semplici | Moduli basati su API altamente complessi |
| **Flessibilità di progettazione** | Limitata | Elevata (personalizzazione CSS/JS) | Moderata (in base ai modelli) | Limitata | Elevata (controllo del framework front-end) |
| **Capacità di integrazione** | Flussi di lavoro di base AEM | Avanzati (modelli di dati, flussi di lavoro) | Integrati con sistemi esterni | Base (Fogli Google, Excel) | Controllo completo tramite API |
| **Metodo di pubblicazione** | Solo AEM | AEM e Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | Qualsiasi front-end tramite API |
| **Prestazioni e SEO** | Standard | Migliorate rispetto ai componenti di base | Punteggi elevati di Google Lighthouse per un rendering più veloce e una SEO migliore | Punteggi elevati di Google Lighthouse per un rendering più veloce e una SEO migliore | Dipende dall’implementazione |
| **Consegna omnicanale** | Limitata | Moderata | Moderata | Limitata | Alta |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### Confronto delle funzioni dei metodi di authoring dei moduli di AEM

La tabella seguente fornisce un confronto dettagliato delle funzioni chiave tra i diversi metodi di authoring dei moduli di AEM, utili per scegliere l’approccio più adatto alle tue esigenze.

| **Funzionalità** | **Componenti di base** | **Componenti core** | **Editor universale (WYSIWYG)** | **Authoring basato su documenti** | **Authoring headless** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Composizione unificata con Sites** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Incorporazione del supporto dei moduli** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Regole (comportamento dinamico)** | Editor di regole avanzate con funzioni personalizzate | Editor di regole avanzate con funzioni personalizzate | Editor di regole avanzate con funzioni personalizzate | Limitato: Mostra/nascondi, valore di calcolo, funzioni personalizzate | Limitato: richiede implementazione personalizzata |
| **Supporto allegato** | ✅ | ✅ | ✅ | ℹ️ (Accesso anticipato) | ❌ |
| **Supporto CAPTCHA** | reCAPTCHA v2/Enterprise, hCaptcha (EA), Turnstile (EA) | reCAPTCHA v2/Enterprise, hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Richiede l’integrazione personalizzata |
| **Funzioni di invio** | Endpoint REST, e-mail, modello dati modulo (FDM), Richiama il flusso di lavoro AEM, SharePoint, OneDrive, archiviazione BLOB di Azure, Power Automate, Workfront Fusion (EA) | Endpoint REST, e-mail, modello dati modulo (FDM), Richiama il flusso di lavoro AEM, SharePoint, OneDrive, archiviazione BLOB di Azure, Power Automate, Workfront Fusion (EA) | Endpoint REST, e-mail, modello dati modulo (FDM), Richiama il flusso di lavoro AEM, SharePoint, OneDrive, archiviazione BLOB di Azure, Power Automate, Workfront Fusion (EA) | Solo foglio di calcolo | Endpoint API personalizzati |
| **Schema dati** | FDM, personalizzato | FDM, personalizzato | FDM, personalizzato | Personalizzato | Personalizzato |
| **Precompilazione** | ✅ | ✅ | 💡 (tramite procedura guidata) | ✅ | Implementazione personalizzata |
| **Frammenti** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **Editor di regole visivo** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Localizzazione** | ✅ | ✅ | 💡 (tramite Sites) | ℹ️ (Excel - Manuale, funzione Fogli di Google) | Implementazione personalizzata |
| **Schema dati (struttura dati)** | ✅ | ✅ | 💡 (tramite estensione dell’interfaccia utente) | ❌ | Implementazione personalizzata |
| **Supporto modello** | ✅ | ✅ | Solo contenuto iniziale, nessun criterio | ❌ | Implementazione personalizzata |
| **Portale** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **Authoring DoR** | ✅ | ✅ | 💡 (tramite Derlina) | ❌ | ❌ |
| **Generazione DoR** | ✅ | ✅ | 💡 (FORMS-2475 Nuovo) | ❌ | ❌ |
| **Tema** | ✅ | ✅ | ℹ️ (a livello di progetto) | ℹ️ (a livello di progetto) | Implementazione personalizzata |
| **Componente personalizzato** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Funzioni OOTB e personalizzate** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Riferimento frammento** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Integrazione di Sign** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Supporto RTL** | ❌ | ✅ | 💡 | 💡 | Implementazione personalizzata |
| **Sperimentazione** | ❌ | ❌ | ✅ | ✅ | Implementazione personalizzata |
| **Gestione attività tramite Workfront** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Estensione della personalizzazione** | ❌ | ❌ | 💡 | ❌ | Implementazione personalizzata |
| **Personalizzazione dell’editor** | ❌ | ❌ | ✅ (tramite estensione dell’interfaccia utente) | ❌ | Implementazione personalizzata |
| **Azione di invio** | ✅ | ✅ | ✅ | Solo foglio di calcolo | Implementazione personalizzata |


## Articolo correlato

* [Creazione basata su documenti con Microsoft Excel o Fogli Google](/help/edge/docs/forms/create-forms.md)
* [Editor universale per l’authoring WYSIWYG](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creare un modulo adattivo (componenti di base)](/help/forms/creating-adaptive-form.md)
* [Creare un modulo adattivo (componenti core)](/help/forms/create-an-adaptive-form.md)
