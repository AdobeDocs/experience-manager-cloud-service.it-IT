---
title: Introduzione all’editor universale
description: L’editor universale è un moderno strumento di authoring visivo progettato per consentire all’organizzazione di marketing di produrre esperienze web di impatto.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 08997c760bf1d609dce1dd17de0c549a26083917
workflow-type: ht
source-wordcount: '948'
ht-degree: 100%

---


# Introduzione all’editor universale {#introduction}

L’editor universale è un moderno strumento di authoring visivo progettato per consentire all’organizzazione di marketing di produrre esperienze web di impatto.

## Panoramica {#overview}

L’editor universale è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di apportare modifiche in modalità WYSIWYG (what you see is what you get) a qualsiasi esperienza headless o headful. Offre le seguenti funzioni:

* **Modifica immediata**: è possibile modificare il contenuto direttamente nell&#39;esperienza di anteprima, senza dover trovare e passare alle singole origini dei contenuti.
* **Modifica visiva**: mentre si apportano modifiche, si vede subito come queste influiscono sull’esperienza effettiva del visitatore, riducendo al minimo l’attrito.
* **Opzioni individuabili**: grazie alle opzioni dalle etichette chiare e all&#39;interfaccia utente intuitiva, gli autori sono in grado di configurare i metadati e comporre i layout con facilità.
* **Non tecnico**: non è necessaria alcuna esperienza specializzata per apportare modifiche; inoltre, l’applicazione automatica delle linee guida del brand offre scalabilità e consente di estendere le attività sui contenuti in tutta l’organizzazione.
* **Integrazione ed estensibilità**: completamente integrato con AEM, l’editor universale è dotato di [punti di estensione](#extensibility) flessibili che consentono di unificare tutti gli strumenti essenziali in un’unica interfaccia coesa. Dalle funzioni basate sull’IA alle estensioni personalizzate per esigenze di business specifiche, consente ai team di semplificare i flussi di lavoro e migliorare la produttività.

In sintesi:

* **La flessibilità dell’editor universale offre vantaggi** in quanto supporta la stessa modalità di modifica visiva per tutti i tipi di contenuti in AEM.
* **Gli sviluppatori traggono vantaggio** dalla versatilità dell’editor universale, che supporta un vero e proprio disaccoppiamento dell’implementazione.

Come editor-as-a-service, l’editor universale è più flessibile e nel tempo sostituirà l&#39;[editor di pagine.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Architetture supportate {#supported-architectures}

L’editor universale supporta le due impostazioni principali di AEM riportate di seguito.

1. **[Edge Delivery Services](/help/edge/overview.md)**: questo è l’approccio preferito per la sua semplicità, il time-to-value più rapido e le prestazioni migliorate.
1. **[Implementazioni headless](/help/headless/introduction.md)**: se hai un progetto headless o requisiti specifici per il rendering disaccoppiato, l’editor universale consente di apportare modifiche in modalità visiva a livello Enterprise, senza dover eseguire il refactoring dell’intero progetto. È compatibile con praticamente qualsiasi architettura (SSR, CSR), framework web (Next.js, React, Astro, ecc.) e modelli di hosting (“bring your own app&quot;).

>[!TIP]
>
>Per ulteriori informazioni sulle architetture supportate, consulta [Casi d’uso per l’editor universale e percorsi di apprendimento](/help/implementing/universal-editor/use-cases.md).

## Versioni di AEM supportate {#aem-versions}

L’editor universale è supportato da:

* AEM as a Cloud Service (versione `2023.8.13099` o successiva)
* [AEM 6.5 LTS](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Sono supportati sia l’hosting locale che l’hosting AMS.
* [AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * Sono supportati sia l’hosting locale che l’hosting AMS.

Questa documentazione riguarda l’utilizzo dell’editor universale con AEM as a Cloud Service.

## Funzioni {#features}

L’editor universale offre numerose funzioni per supportare un’ampia gamma di casi d’uso per la gestione efficiente dei contenuti.

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**: consente di apportare modifiche a qualsiasi tipo di contenuto web, inclusi testo normale, testo formattato, file multimediali e metadati.
* **[Composizione](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**: puoi creare, modificare, riordinare, nidificare o eliminare blocchi di contenuto di vari tipi (titoli, pulsanti, teaser, sezioni, incorporamenti, ecc.).
* **[Layout](/help/sites-cloud/authoring/universal-editor/templates.md)**: puoi utilizzare modelli di pagina, applicare stili visivi e comporre layout con blocchi di vario tipo, ad esempio per colonne, caroselli e pannelli a soffietto.
* **[Simulazione dispositivo](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**: durante la modifica, è possibile vedere in anteprima e ottimizzare i contenuti per i diversi dispositivi dei visitatori.
* **Omnicanale**: puoi riutilizzare contenuti strutturati e non strutturati su più canali.
* **[Localizzazione](/help/sites-cloud/authoring/universal-editor/inheritance.md)**: semplifica i flussi di lavoro di traduzione dei contenuti e gestisci in modo efficiente l’ereditarietà dei contenuti localizzati con Multi-Site Manager.
* **Coerenza**: assicura che vi sia conformità con le linee guida del brand, per tutti i contenuti.
* **Sicurezza**: [puoi applicare il controllo degli accessi](/help/implementing/universal-editor/authentication.md), proteggere l’integrità dei contenuti e tenere traccia delle modifiche con un [solido controllo delle versioni.](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[Pubblicazione](/help/sites-cloud/authoring/universal-editor/publishing.md)**: i flussi di lavoro di revisione, approvazione e pubblicazione sono integrati direttamente nell’editor.
* **Unificato**: si integra completamente con gli strumenti di AEM come la [console Sites](/help/sites-cloud/authoring/sites-console/introduction.md), l’[editor di frammenti di contenuto,](/help/sites-cloud/administering/content-fragments/overview.md) e molti altri, per un’esperienza di authoring coesa.

## Estensibilità {#extensibility}

L’editor universale è pronto all’uso e offre inoltre diverse possibilità di estensione.

* Le **estensioni** sono numerose e predefinite per soddisfare requisiti quali il supporto dei flussi di lavoro, la generazione di varianti e l’abilitazione della sperimentazione, per citarne alcuni.
* **Un’interfaccia utente estendibile** consente di creare estensioni personalizzate utilizzando gli stessi framework sottostanti che vengono sfruttati dalle estensioni predefinite, permettendo la massima flessibilità per adattarsi alle esigenze del progetto.
* **I punti di estensione**, come i blocchi, i tipi di dati personalizzati e gli eventi, consentono un’integrazione ottimizzata dei requisiti di business personalizzati oltre l’interfaccia utente.

>[!TIP]
>
>Per ulteriori informazioni sull’estendibilità dell’editor universale, consulta il documento [Estensione dell’editor universale.](/help/implementing/universal-editor/extending.md)

## Editor universale e Editor di frammenti di contenuto {#universal-editor-content-fragment-editor}

A prima vista, potrebbe sembrare che l’editor universale e l’editor di frammenti di contenuto forniscano funzionalità di modifica simili. Tuttavia, questi editor offrono funzionalità molto diverse e svolgono diversi compiti del professionista di marketing.

### Editor frammento di contenuto {#content-fragment-editor}

Un professionista del marketing desidera creare contenuto senza doversi preoccupare del layout, in modo che possa essere riutilizzato in numerosi contesti dell’esperienza.

* Il lavoro sottostante da realizzare è quello di scalare la strategia del contenuto.

### Editor universale {#universal-editor}

Un professionista del marketing desidera creare contenuto personalizzato in base al layout di un determinato contesto per offrire un’esperienza eccezionale.

* Il lavoro sottostante da realizzare è quello di entrare in contatto in modo convincente con i lettori.

## Limitazioni {#limitations}

Quando esplori l’editor universale e procedi alla sua implementazione nei tuoi progetti, tieni presenti le seguenti limitazioni.

* In una singola pagina, non dovrebbero essere presenti riferimenti a più di 25 risorse AEM (frammenti di contenuto, pagine, frammenti di esperienza, risorse, ecc.) come parte della strumentazione.
* AEM as a Cloud Service, [AEM 6.5 LTS](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction) e [AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) sono gli unici back-end di AEM supportati.
* Per AEM as a Cloud Service è obbligatoria la versione `2023.8.13099` o successiva.
* Gli autori dei contenuti devono disporre di un proprio account Experience Cloud.
* Come parte di AEM, l’editor universale [supporta gli stessi browser desktop di AEM.](/help/overview/supported-platforms.md)
   * Le versioni per dispositivi mobili di questi browser non sono supportate.

{{ip-allow-lists-ue}}

## Passaggi successivi {#next-steps}

Consulta il documento [Casi d’uso e percorsi di apprendimento dell’editor universale](/help/implementing/universal-editor/use-cases.md) per ulteriori informazioni sui casi d’uso più comuni dell’editor universale e per scoprire risorse di documentazione appropriate per supportarti nel progetto.
