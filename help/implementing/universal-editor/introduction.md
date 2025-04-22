---
title: Introduzione all’editor universale
description: Universal Editor è uno strumento di authoring visivo moderno progettato per consentire all’organizzazione di marketing di produrre esperienze web di impatto.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ae59b00e7e8149477a87d0b0b63493a6c2cfebe7
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 10%

---


# Introduzione all’editor universale {#introduction}

Universal Editor è uno strumento di authoring visivo moderno progettato per consentire all’organizzazione di marketing di produrre esperienze web di impatto.

## Panoramica {#overview}

Universal Editor è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di eseguire la modifica di ciò che vedi è ciò che ottieni (WYSIWYG) di qualsiasi esperienza headless o headful. Offre:

* **Modifica immediata**: gli autori possono modificare il contenuto direttamente nell&#39;esperienza di anteprima, eliminando la necessità di individuare e passare alle singole origini di contenuto.
* **Modifica visiva**: mentre apporti modifiche, gli autori vedono immediatamente come influiscono sull&#39;esperienza effettiva del visitatore, riducendo al minimo l&#39;attrito.
* **Opzioni individuabili**: le opzioni con etichetta chiara e un&#39;interfaccia utente intuitiva consentono agli autori di configurare i metadati e comporre layout con facilità.
* **Non tecnico**: non è necessaria alcuna esperienza specializzata per apportare modifiche, mentre le linee guida del marchio aziendale vengono applicate automaticamente, facilitando la scalabilità delle attività di contenuto in tutta l&#39;organizzazione.
* **Integrazione ed estensibilità**: completamente integrato con AEM, i [punti di estensione](#extensibility) flessibili dell&#39;editor universale consentono di unificare tutti gli strumenti essenziali in un&#39;unica interfaccia coesa. Dalle funzioni basate sull’intelligenza artificiale alle estensioni personalizzate in base alle esigenze aziendali specifiche, consente ai team di semplificare i flussi di lavoro e migliorare la produttività senza problemi.

In sintesi:

* **La flessibilità dell&#39;editor universale offre vantaggi** in quanto supporta la stessa modifica visiva coerente per tutte le forme di contenuto AEM.
* **Gli sviluppatori traggono vantaggio** dalla versatilità di Universal Editor in quanto supporta un vero e proprio disaccoppiamento dell&#39;implementazione.

Essendo un vero editor-as-a-service ed è nel complesso più flessibile, l&#39;editor universale intende alla fine sostituire l&#39;[Editor pagina.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Architetture supportate {#supported-architectures}

Universal Editor supporta le due impostazioni principali di AEM riportate di seguito.

1. **[Edge Delivery Services](/help/edge/overview.md)**: questo è l&#39;approccio preferito per la sua semplicità, il time-to-value più veloce e le prestazioni migliorate.
1. **[Implementazioni headless](/help/headless/introduction.md)**: se disponi di un progetto headless esistente o di requisiti specifici per il rendering disaccoppiato, Universal Editor consente modifiche visive di livello Enterprise senza dover rieseguire il factoring dell&#39;intero progetto. È compatibile con praticamente qualsiasi architettura (SSR, CSR), framework web (Next.js, React, Astro, ecc.) e modelli di hosting (&quot;porta la tua app&quot;).

>[!TIP]
>
>Per ulteriori dettagli sulle architetture supportate, consulta il documento [Casi d&#39;uso dell&#39;editor universale e percorsi di apprendimento](/help/implementing/universal-editor/use-cases.md).

## Versioni di AEM supportate {#aem-versions}

L’editor universale è supportato da:

* AEM as a Cloud Service (versione `2023.8.13099` o successiva)
* AEM 6.5 (service pack 21 o 22 più un feature pack)
   * Sono supportati sia l’hosting locale che AMS.

Questa documentazione è per l’utilizzo di Universal Editor con AEM as a Cloud Service. Per utilizzare Universal Editor con AEM 6.5, [consulta la documentazione di AEM 6.5.](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)

## Funzioni {#features}

Universal Editor offre numerose funzioni per supportare un&#39;ampia gamma di casi d&#39;uso per una gestione efficiente dei contenuti.

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**: consente di eseguire la modifica di qualsiasi tipo di contenuto Web, inclusi testo normale, testo RTF, file multimediali e metadati.
* **[Composizione](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**: crea, modifica, riordina, nidifica o elimina blocchi di contenuto di vari tipi (titoli, pulsanti, teaser, sezioni, incorporamenti, ecc.).
* **[Layout](/help/sites-cloud/authoring/universal-editor/templates.md)**: utilizza i modelli di pagina, applica stili visivi e compone layout con blocchi come colonne, caroselli e fisarmoniche.
* **[Simulazione dispositivo](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**: anteprima e ottimizzazione del contenuto per diversi dispositivi visitatore durante la modifica.
* **Omnichannel**: riutilizzare contenuti strutturati e non strutturati su più canali.
* **[Localizzazione](/help/sites-cloud/authoring/universal-editor/inheritance.md)**: semplificazione dei flussi di lavoro di traduzione dei contenuti e gestione efficiente dell&#39;ereditarietà dei contenuti localizzati con Multi-Site Manager.
* **Coerenza**: assicurati la conformità con le linee guida del brand e mantieni l&#39;uniformità su tutti i contenuti.
* **Sicurezza**: [Applica controllo degli accessi](/help/implementing/universal-editor/authentication.md), proteggi l&#39;integrità del contenuto e tieni traccia delle modifiche con [un controllo delle versioni affidabile.](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[Pubblicazione](/help/sites-cloud/authoring/universal-editor/publishing.md)**: integra i flussi di lavoro di revisione, approvazione e pubblicazione direttamente nell&#39;editor.
* **Unificato**: si integra completamente con gli strumenti di AEM come [Console Sites,](/help/sites-cloud/authoring/sites-console/introduction.md) [Editor frammento di contenuto,](/help/sites-cloud/administering/content-fragments/overview.md) e molti altri, fornendo un&#39;esperienza di authoring coesa.

## Estensibilità {#extensibility}

L’editor universale non solo è pronto all’uso ma offre diverse possibilità di estensione.

* **Le estensioni** sono numerose e pronte per supportare requisiti quali il supporto dei flussi di lavoro, la generazione di varianti e l&#39;abilitazione della sperimentazione per citarne alcune.
* **Un&#39;interfaccia utente estensibile** consente di creare estensioni personalizzate utilizzando gli stessi framework sottostanti utilizzati dalle estensioni pronte all&#39;uso, consentendo la massima flessibilità per adattarsi alle esigenze del progetto.
* **I punti di estensione** come blocchi, tipi di dati personalizzati ed eventi consentono un&#39;integrazione perfetta dei requisiti di business personalizzati oltre l&#39;interfaccia utente.

>[!TIP]
>
>Per ulteriori informazioni sull&#39;estensibilità di Universal Editor, vedere il documento [Estensione di Universal Editor.](/help/implementing/universal-editor/extending.md)

## Editor universale e Editor frammento di contenuto {#universal-editor-content-fragment-editor}

A prima vista, potrebbe sembrare che l’Editor universale e l’Editor frammento di contenuto forniscano funzionalità di modifica simili. Tuttavia, questi editor offrono funzionalità molto diverse e svolgono diversi compiti del professionista di marketing.

### Editor frammento di contenuto {#content-fragment-editor}

Un professionista del marketing desidera creare contenuto senza doversi preoccupare del layout, in modo che possa essere riutilizzato in numerosi contesti dell’esperienza.

* Il lavoro sottostante da realizzare è quello di scalare la strategia del contenuto.

### Editor universale {#universal-editor}

Un professionista del marketing desidera creare contenuto personalizzato in base al layout di un determinato contesto per offrire un’esperienza eccezionale.

* Il lavoro sottostante da realizzare è quello di entrare in contatto in modo convincente con i lettori.

## Limitazioni {#limitations}

Quando esplori l’Editor universale e procedi alla sua implementazione nei tuoi progetti, tieni presenti le seguenti limitazioni.

* Non più di 25 risorse AEM (frammenti di contenuto, pagine, frammenti di esperienza, Assets, ecc.) devono essere riferimenti come strumentazione su una singola pagina.
* AEM as a Cloud Service e [AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) sono gli unici backend AEM supportati.
* Per AEM as a Cloud Service è richiesta la versione `2023.8.13099` o successiva.
* Gli autori dei contenuti devono disporre di un proprio account Experience Cloud.
* Come parte di AEM, l&#39;editor universale [supporta gli stessi browser desktop di AEM.](/help/overview/supported-platforms.md)
   * Le versioni mobili di questi browser non sono supportate.

{{ip-allow-lists-ue}}

## Passaggi successivi {#next-steps}

Consulta il documento [Casi d&#39;uso e percorsi di apprendimento dell&#39;editor universale](/help/implementing/universal-editor/use-cases.md) per ulteriori informazioni sui casi d&#39;uso comuni per l&#39;editor universale e per scoprire le risorse di documentazione appropriate per supportarti nel progetto.
