---
title: Navigazione nell’interfaccia utente di Cloud Manager
description: Scopri come è organizzata l’interfaccia utente di Cloud Manager e come spostarsi per gestire i programmi e gli ambienti.
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b2950c62c55942614e23d08b3bb96864d4112e8c
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 80%

---


# Navigazione nell’interfaccia utente di Cloud Manager {#navigation}

Scopri come è organizzata l’interfaccia utente di Cloud Manager e come spostarsi per gestire i programmi e gli ambienti.

L’interfaccia utente di Cloud Manager è composta principalmente da due interfacce grafiche:

* [La console Programmi personali](#my-programs-console) in cui è possibile visualizzare e gestire tutti i programmi.
* [La finestra Panoramica del programma](#program-overview) dove puoi visualizzare i dettagli di e gestire un singolo programma.

>[!TIP]
>
>Consulta anche il [percorso di documentazione sull&#39;onboarding](/help/journey-onboarding/overview.md) per una panoramica completa su come iniziare a utilizzare AEM as a Cloud Service con Cloud Manager.

## Console Programmi personali {#my-programs-console}

Quando accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezioni l’organizzazione appropriata, vieni indirizzato alla console **Programmi personali**.

![Console Programmi personali](assets/my-programs-console.png)

La console Programmi personali fornisce una panoramica di tutti i programmi a cui hai accesso nell’organizzazione selezionata. È costituita da diverse elementi.

1. [Barre degli strumenti](#toolbars-my-programs-toolbars) per la selezione di organizzazioni, avvisi e impostazioni account
1. Schede che consentono di attivare/disattivare la visualizzazione corrente dei programmi.
   * Visualizzazione **Pagina principale** (predefinita) che seleziona la visualizzazione **Programmi personali** con una panoramica di tutti i programmi
   * **Licenza** che accede alla [Dashboard delle licenze.](/help/implementing/cloud-manager/license-dashboard.md)
   * Per impostazione predefinita, le schede sono chiuse e possono essere visualizzate utilizzando il menu hamburger nell’[intestazione Cloud Manager.](#cloud-manager-header)
1. [Statistiche e invito all’azione](#statistics) per una panoramica dell’attività recente
1. Sezione [**Programmi personali** ](#my-programs-section) con una panoramica di tutti i programmi
1. [Collegamenti rapidi](#quick-links-section) per accedere facilmente alle risorse correlate

>[!TIP]
>
>Per ulteriori informazioni sui programmi, consulta il documento [Programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

### Barre degli strumenti {#my-programs-toolbars}

Sono disponibili due barre degli strumenti una sopra l’altra.

#### Intestazione di Cloud Manager {#cloud-manager-header}

La prima è l’intestazione di Cloud Manager, che è persistente quando ti sposti in Cloud Manager. Si tratta di un ancoraggio che consente di accedere alle impostazioni e alle informazioni applicabili ai diversi programmi di Cloud Manager.

![Intestazione di Experience Cloud](assets/experience-cloud-header.png)

1. Il menu hamburger che fornisce l&#39;accesso alle schede che possono portare a parti specifiche di un singolo programma o passare dalla [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md) alla console **[Programmi](#my-programs-console)** a seconda del contesto.
1. Il pulsante Cloud Manager ti riporterà alla console Programmi personali di Cloud Manager, indipendentemente dalla tua posizione in Cloud Manager.
1. Tocca o fai clic sul pulsante Feedback per fornire un feedback ad Adobe su Cloud Manager.
1. Il selettore organizzazione visualizza l’organizzazione a cui sei attualmente connesso (in questo esempio, Foundation Internal). Tocca o fai clic per passare a un’altra organizzazione se il tuo Adobe ID è associato a più di una.
1. Tocca o fai clic sul selettore delle soluzioni per passare rapidamente ad altre soluzioni di Experience Cloud.
1. L’icona dell’aiuto fornisce un accesso rapido alle risorse di apprendimento e supporto.
1. Questa icona viene contrassegnata con il numero di [notifiche](/help/implementing/cloud-manager/notifications.md) incomplete attualmente assegnate.
1. Seleziona l’icona che rappresenta l’utente per accedere alle impostazioni utente. Se non hai configurato un’immagine utente, viene assegnata un’icona in modo casuale.

#### Barra degli strumenti del programma {#program-toolbar}

La barra degli strumenti del programma fornisce collegamenti per passare da programmi ad azioni di Cloud Manager e viceversa appropriati al contesto.

![Barra degli strumenti del programma](assets/program-toolbar.png)

1. Il selettore di programma si apre in un menu a discesa in cui puoi selezionare rapidamente altri programmi o intraprendere azioni appropriate al contesto, ad esempio la creazione di un nuovo programma
1. Il collegamento introduttivo consente di accedere al [percorso di documentazione sull’onboarding](/help/journey-onboarding/overview.md) per iniziare a utilizzare Cloud Manager.
1. Il pulsante di azione offre azioni appropriate al contesto, ad esempio la creazione di un nuovo programma.

### Statistiche e inviti all&#39;azione {#statistics}

La sezione Statistiche e invito all’azione fornisce dati aggregati per l’organizzazione. Ad esempio, se hai configurato correttamente i programmi, potrebbero essere visualizzate le statistiche delle attività degli ultimi 90 giorni, tra cui:

* Numero di [implementazioni](/help/implementing/cloud-manager/deploy-code.md)
* Numero di [problemi di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) identificati
* Numero di build

Oppure, se stai iniziando la configurazione dell’organizzazione, potrebbero essere disponibili suggerimenti sui passaggi successivi o sulle risorse della documentazione.

### Sezione Programmi personali {#my-programs-section}

Il contenuto principale della console **Programmi** è l&#39;elenco dei programmi nella sezione **Programmi**.

Nella sezione **I miei programmi** sono elencate le schede che rappresentano ogni programma. Tocca o fai clic su una scheda per accedere alla pagina **Panoramica del programma** per informazioni dettagliate sul programma.

>[!NOTE]
>
>A seconda dei privilegi di cui si dispone, potrebbe non essere possibile selezionare alcuni programmi.

Utilizza le opzioni di ordinamento per trovare meglio il programma necessario.

![Opzioni di ordinamento](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Ordina per
   * Data di creazione (impostazione predefinita)
   * Nome del programma
   * Stato
* Crescente (predefinito) / Decrescente
* Vista griglia (predefinito)
* Vista a elenco

#### Schede del programma {#program-cards}

Ogni programma è rappresentato da una scheda (o riga in una tabella) che fornisce una panoramica del programma e collegamenti rapidi per intervenire.

![Scheda Programma](assets/program-card.png)

* Immagine del programma (se configurata)
* Nome del programma
* Tipo di servizio:
   * **Experience Manager Cloud** per programmi AEM as a Cloud Service
   * **Experience Manager** per [programmi AMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [Tipo di programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md):
   * Sandbox
   * Produzione
* Stato
* Soluzioni configurate
* Data di creazione

A seconda delle opzioni scelte durante la creazione del programma, un programma di produzione potrebbe essere contrassegnato per mostrare funzioni aggiuntive.

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![Badge HIPAA](assets/hipaa.png)

* [Protezione WAF-DDOS](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![Badge WAF-DDOS](assets/waf-ddos-protection.png)

* [SLA 99,99%](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99,99% badge SLA](assets/9999-sla.png)

L’icona delle informazioni consente inoltre di accedere rapidamente a informazioni aggiuntive sul programma (utili nella vista a elenco).

![Informazioni](assets/information-list-view.png)

L’icona con i puntini di sospensione ti permette di accedere alle azioni aggiuntive che puoi intraprendere sul programma.

![Pulsante con i puntini di sospensione per i programmi](assets/program-ellipsis.png)

* Passare a un determinato [ambiente](/help/implementing/cloud-manager/manage-environments.md) del programma
* Apri la [Panoramica del programma](#program-overview)
* [Modifica il programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [Eliminare un programma sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Per ulteriori informazioni sui programmi e sulla creazione e gestione dei programmi, vedere i seguenti documenti.
>
>* [Programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Creazione di programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [Creazione di programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

### Sezione Collegamenti rapidi {#quick-links-section}

La sezione dei collegamenti rapidi consente di accedere alle risorse correlate di uso comune.

## Finestra Panoramica del programma {#program-overview}

Dopo aver selezionato un programma nella console **[Programmi personali](#my-programs-console)**, viene visualizzata la finestra **Panoramica programma**.

![Panoramica del programma](assets/program-overview.png)

La panoramica del programma consente di accedere a tutti i dettagli di un programma di Cloud Manager. Come la console **Programmi**, è composta da diverse parti.

1. [Barre degli strumenti](#program-overview-toolbar) per tornare rapidamente alla console Programmi personali e passare al programma
1. [Schede](#program-tabs) per passare da un aspetto all’altro del programma
1. Un [invito all’azione](#cta) basato sulle ultime azioni del programma
1. Una [panoramica degli ambienti](#environments) del programma
1. Una [panoramica delle pipeline](#pipelines) del programma
1. [panoramica delle prestazioni](#performance) del programma
1. Collegamenti a [risorse utili](#useful-resources)

### Barre degli strumenti {#program-overview-toolbar}

Le barre degli strumenti per la panoramica del programma sono molto simili a quelle della console [Programmi personali.](#my-programs-toolbars) Qui sono illustrate solo le differenze.

#### Intestazione di Cloud Manager {#cloud-manager-header-2}

L’intestazione di Cloud Manager dispone di un menu hamburger che si apre automaticamente per mostrare le schede navigabili della panoramica del programma.

![Menu hamburger di Cloud Manager](assets/cloud-manager-hamburger.png)

Tocca o fai clic sull’icona del menu hamburger per nascondere le schede.

#### Barra degli strumenti del programma {#program-toolbar-2}

La barra degli strumenti del programma consente comunque di passare rapidamente ad altri programmi, ma consente anche di accedere ad azioni appropriate al contesto, come l’aggiunta e la modifica del programma.

![Barra degli strumenti del programma](assets/cloud-manager-program-toolbar.png)

Inoltre, la barra degli strumenti fornisce sempre la scheda su cui ci si trova se si è scelto di nascondere le schede utilizzando il menu hamburger.

### Schede Programma {#program-tabs}

A ogni programma sono associate molte opzioni e molti dati. Questi dati vengono raccolti in schede per semplificare la navigazione nel programma. Le schede consentono di accedere a:

* Panoramica: la panoramica del programma come descritto nel documento corrente
* [Attività](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity): la cronologia delle esecuzioni delle pipeline del programma
* [Pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines): tutte le pipeline configurate per il programma
* [Archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md): tutti gli archivi configurati per il programma
* [Rapporti](/help/implementing/cloud-manager/sla-reporting.md): metriche quali i dati SLA
* [Ambienti](/help/implementing/cloud-manager/manage-environments.md): tutti gli ambienti configurati per il programma
* [Impostazioni dominio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Gestisci nomi di dominio personalizzati per il programma
* [Certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) - Gestisci i certificati SSL per il programma
* [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) - Definisci elenchi consentiti per determinati indirizzi IP
* [Set di contenuti](/help/implementing/developing/tools/content-copy.md): set di contenuti creati per scopi di copia
* [Attività copia contenuto](/help/implementing/developing/tools/content-copy.md): attività di copia dei contenuti
* [Infrastruttura di rete](/help/security/configuring-advanced-networking.md) - Gestisce le opzioni di rete avanzate per il programma
* Percorsi di apprendimento: risorse di apprendimento aggiuntive su Cloud Manager

Per impostazione predefinita, quando si apre un programma si accede alla scheda **Panoramica**. Viene evidenziata la scheda corrente. Seleziona un’altra scheda per visualizzarne i dettagli.

Utilizza il menu hamburger in [Intestazione di Cloud Manager](#cloud-manager-header-2) per nascondere le schede.

### Invito all’azione {#cta}

La sezione relativa agli inviti all’azione fornisce informazioni utili in base allo stato del programma. Per un nuovo programma puoi vedere i passaggi successivi offerti e un promemoria della data di pubblicazione, [impostato durante la creazione del programma.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![Invito all&#39;azione per un nuovo programma](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

Per un programma live, lo stato dell’ultima implementazione con collegamenti per i dettagli e l’avvio di una nuova implementazione.

![Invito all’azione](/help/implementing/cloud-manager/assets/info-banner.png)

### Scheda Ambienti {#environments}

La scheda **Ambienti** offre una panoramica degli ambienti e collegamenti per azioni rapide.

Nella scheda **Ambienti** sono elencati solo tre ambienti. Per visualizzare tutti gli ambienti del programma, fai clic su **Mostra tutto**.

Consulta il documento [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) per informazioni dettagliate su come gestire gli ambienti.

### Scheda Pipeline {#pipelines}

La scheda **Pipeline** offre una panoramica delle pipeline e dei collegamenti per azioni rapide.

Nella scheda **Pipeline** sono elencate solo tre pipeline. Per visualizzare tutte le pipeline del programma, fai clic su **Mostra tutto**.

Consulta il documento [Gestione delle pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) per informazioni dettagliate su come gestirle.

### Scheda Prestazioni {#performance}

La scheda **Prestazioni** offre una panoramica della **[dashboard CDN.](/help/implementing/cloud-manager/cdn-performance.md)**

![Scheda Prestazioni](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Risorse utili {#useful-resources}

La sezione **Risorse utili** fornisce collegamenti a risorse di apprendimento aggiuntive per Cloud Manager.
