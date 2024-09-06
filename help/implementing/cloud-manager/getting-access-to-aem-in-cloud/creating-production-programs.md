---
title: Creare programmi di produzione
description: Scopri come creare un programma di produzione per ospitare il traffico in tempo reale con Cloud Manager.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6a3d2d484bde20586b329010cdfe156570e736f5
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 12%

---


# Creare programmi di produzione {#create-production-program}

Un programma di produzione è per gli utenti che hanno familiarità con AEM e Cloud Manager, pronti per scrivere, generare e testare il codice, con l’obiettivo di distribuirlo per gestire il traffico in tempo reale.

Ulteriori informazioni sui tipi di programmi nel documento [Informazioni su programmi e tipi di programmi](program-types.md).

## Creare un programma di produzione {#create}

A seconda dei diritti dell&#39;organizzazione, è possibile che vengano visualizzate [opzioni aggiuntive](#options) durante l&#39;aggiunta del programma.

**Per creare un programma di produzione:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, nell&#39;angolo superiore destro, fare clic su **Aggiungi programma**.

   ![Pagina di destinazione di Cloud Manager](assets/log-in.png)

1. Nella procedura guidata *Crea il programma*, nel campo di testo **Nome programma**, digita il nome desiderato per il programma.

1. In **Obiettivo programma**, selezionare **`Set up for production`**.

   ![Procedura guidata per la creazione di un programma](assets/create-production-program.png)

1. (Facoltativo) Nell&#39;angolo inferiore destro della finestra di dialogo della procedura guidata, effettuate una delle seguenti operazioni:

   * Trascina e rilascia un file di immagine nella destinazione **Aggiungi un&#39;immagine del programma**.
   * Fai clic su **Aggiungi un&#39;immagine del programma**, quindi seleziona un&#39;immagine da un browser di file.
   * Fai clic sull’icona cestino per eliminare un’immagine aggiunta.

1. Fai clic su **Continua**.

1. Nella casella di riepilogo **Soluzioni e componenti aggiuntivi** selezionare una o più soluzioni da includere nel programma.

   * Se non sai per certo se ti servono uno o più programmi per le varie soluzioni disponibili, seleziona quella che più ti interessa. Potrai attivare altre soluzioni in un secondo tempo [modificando il programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md). Per ulteriori consigli sulla configurazione del programma, consulta [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).
   * Per la creazione del programma è necessaria almeno una soluzione.
   * Seleziona **Edge Deliver Services** per una soluzione CDN completamente gestita che ottimizza le esperienze digitali. Consulta [Informazioni sull&#39;utilizzo dei Edge Delivery Services per consegnare il tuo progetto Cloud Manager](#edge-overview)
   * Se è stata selezionata l&#39;opzione **[Abilita sicurezza avanzata](#security)**, è possibile selezionare solo tutte le soluzioni per le quali sono disponibili i diritti HIPAA.

   ![Selezione delle soluzioni](/help/implementing/cloud-manager/assets/add-production-program-with-edge.png)

1. Fai clic sulla freccia a sinistra del nome di una soluzione per visualizzare eventuali componenti aggiuntivi facoltativi, ad esempio il componente aggiuntivo **Commerce** in **Sites**.

   ![Selezione dei componenti aggiuntivi](assets/setup-prod-commerce.png)

1. Dopo aver selezionato le soluzioni e i componenti aggiuntivi, fai clic su **Continua**.

1. Nella scheda **Data di pubblicazione**, inserisci la data in cui intendi avviare il programma di produzione.

   ![Definizione della data di pubblicazione pianificata](assets/set-up-go-live.png)

   * Puoi modificare questa data in qualsiasi momento.
   * La data ha scopo informativo e attiva il widget di pubblicazione nella pagina [**Panoramica del programma**](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview). Questa funzionalità fornisce collegamenti tempestivi alle best practice di AEM as a Cloud Service per supportare un’esperienza di pubblicazione fluida.

1. Fai clic su **Crea**. Cloud Manager crea il programma e lo visualizza nella pagina di destinazione per la selezione.

![Panoramica di Cloud Manager](assets/navigate-cm.png)

## Opzioni aggiuntive del programma di produzione {#options}

A seconda dei diritti disponibili per l’organizzazione, è possibile che siano disponibili opzioni aggiuntive al momento della creazione di un programma di produzione.

### Sicurezza {#security}

Se si dispone dei diritti necessari, la scheda **Protezione** verrà visualizzata come prima scheda nella finestra di dialogo **`Set up for production`**.

![Opzioni di protezione](assets/create-production-program-security.png)

La scheda **Sicurezza** fornisce le opzioni per attivare **HIPAA** o **Protezione WAF-DDOS** o entrambi per il programma di produzione.

Adobe Conformità HIPAA e WAF-DDOS (Web Application Firewall - Distributed Denial of Service) facilitano la sicurezza basata sul cloud come parte di un approccio multilivello per la protezione contro le vulnerabilità.

* **HIPAA** - Questa opzione abilita l&#39;implementazione della soluzione compatibile con HIPPA di Adobe.
   * [Ulteriori informazioni](https://www.adobe.com/trust/compliance/hipaa-ready.html) sull’implementazione della soluzione compatibile HIPAA di Adobe.
   * Impossibile abilitare o disabilitare HIPAA dopo la creazione del programma.
* **Protezione WAF-DDOS** - Questa opzione abilita il firewall dell&#39;applicazione Web tramite regole per la protezione dell&#39;applicazione.
   * Una volta attivata, la protezione WAF-DDOS può quindi essere configurata impostando una [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).
   * Consulta [Regole filtro traffico, incluse le regole di WAF](/help/security/traffic-filter-rules-including-waf.md) per scoprire come gestire le regole filtro traffico nel tuo archivio in modo che vengano distribuite correttamente.

### SLA {#sla}

Se si dispone dei diritti necessari, la scheda **SLA** verrà visualizzata come seconda o terza scheda nella finestra di dialogo **`Set up for production`**.

![Opzioni SLA](assets/create-production-program-sla.png)

AEM Sites e Forms offrono un contratto di servizio (Service Level Agreement, SLA) standard al 99,9%. L&#39;opzione del **99,99% del contratto del livello di servizio** consente un tempo di attività minimo del 99,99% per gli ambienti di produzione per Sites e/o Forms.

Il 99,99% di SLA offre vantaggi quali maggiore disponibilità e minore latenza e richiede l&#39;applicazione di un&#39;ulteriore area di pubblicazione [](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) all&#39;ambiente di produzione nel programma.

Quando sono soddisfatti i [requisiti](#sla-requirements) per abilitare SLA al 99,99%, è necessario eseguire una [pipeline full stack](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per attivarla.

#### Requisiti per SLA al 99,99% {#sla-requirements}

Oltre alle adesioni richieste, il 99,99% di SLA ha requisiti aggiuntivi per l’utilizzo.

* Quando applichi al programma il 99,99% di SLA, l’organizzazione deve disporre del 99,99% di SLA e di altre autorizzazioni per area geografica di pubblicazione.
* Cloud Manager verifica che sia disponibile un diritto di [area di pubblicazione aggiuntiva](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) inutilizzato prima di applicare SLA al programma al 99,99%.
* Durante la modifica di un programma, se contiene già un ambiente di produzione con almeno un’area di pubblicazione aggiuntiva, Cloud Manager controlla solo la disponibilità di un diritto SLA del 99,99%.
* Per attivare il 99,99% di SLA e il reporting, è necessario che sia stato creato l&#39;[ambiente di produzione/staging](/help/implementing/cloud-manager/manage-environments.md#adding-environments) e che sia stata applicata almeno un&#39;area di pubblicazione aggiuntiva all&#39;ambiente di produzione/staging.
   * Se utilizzi la [rete avanzata](/help/security/configuring-advanced-networking.md), assicurati di controllare nel documento [Aggiunta di più aree di Publish a un nuovo ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-regions) che non siano presenti consigli in modo da mantenere la connettività in caso di errore regionale.
* Almeno un&#39;area geografica di pubblicazione aggiuntiva deve rimanere nel programma SLA al 99,99%. Gli utenti non possono eliminare l’ultima area di pubblicazione aggiuntiva dal programma SLA al 99,99%.
* Il 99,99% di SLA è supportato per i programmi di produzione in cui è abilitata la soluzione Sites o Forms.
* Esegui una [pipeline full stack](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per attivare o, quando modifichi un programma, disattivare il SLA al 99,99%.

## Accedere al programma {#accessing}

1. Quando visualizzi la scheda del programma nella pagina di destinazione, seleziona il pulsante con i puntini di sospensione per visualizzare le opzioni di menu disponibili.

   ![Panoramica del programma](assets/program-overview.png)

1. Per accedere alla pagina **Panoramica** di Cloud Manager, seleziona **Panoramica del programma**.

1. La principale scheda di invito all’azione nella pagina della panoramica ti guida attraverso la creazione di un ambiente, una pipeline non di produzione e infine una pipeline di produzione.

   ![Panoramica del programma](assets/set-up-prod5.png)

>[!TIP]
>
>Consulta [Navigare nell&#39;interfaccia utente di Cloud Manager](/help/implementing/cloud-manager/navigation.md) per informazioni su come esplorare Cloud Manager e comprendere la console **Programmi**.

>[!NOTE]
>
>A differenza di un [programma sandbox](introduction-sandbox-programs.md#auto-creation), un programma di produzione richiede che l&#39;utente con il ruolo Cloud Manager appropriato crei il progetto e aggiunga un ambiente tramite l&#39;interfaccia utente self-service.


