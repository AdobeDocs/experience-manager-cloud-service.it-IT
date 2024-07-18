---
title: Creazione di programmi di produzione
description: Scopri come creare un programma di produzione per ospitare il traffico in tempo reale con Cloud Manager.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 88b0479c44f6431a9f254551e51b1ce86af91d0f
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 34%

---


# Creazione di programmi di produzione {#create-production-program}

Un programma di produzione è destinato agli utenti che hanno familiarità con AEM e Cloud Manager e sono pronti per iniziare a scrivere, creare e testare il codice allo scopo di distribuirlo per ospitare il traffico in tempo reale.

Per ulteriori informazioni sui tipi di programmi, consulta il documento [Informazioni su programmi e tipi di programmi.](program-types.md)

## Creazione di un programma di produzione {#create}

Per creare un programma di produzione, segui la procedura riportata di seguito. Tieni presente che, a seconda dei diritti della tua organizzazione, potresti visualizzare [opzioni aggiuntive](#options) durante l&#39;aggiunta del programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, tocca o fai clic su **Aggiungi programma** nell&#39;angolo in alto a destra dello schermo.

   ![Pagina di destinazione di Cloud Manager](assets/log-in.png)

1. Per creare un programma di produzione, seleziona **Configura per produzione** nella procedura guidata Crea programma nome e specifica un nome.

   ![Procedura guidata per la creazione di un programma](assets/create-production-program.png)

1. Se lo desideri, puoi anche aggiungere un’immagine al programma trascinando un file immagine nell’area **Aggiungi un’immagine del programma** oppure fai clic per selezionare un’immagine da un browser di file. Seleziona **Continua**.

1. Dalla scheda **Soluzioni e componenti aggiuntivi**, seleziona le soluzioni da includere nel programma.

   * Se non sai per certo se ti servono uno o più programmi per le varie soluzioni disponibili, seleziona quella che più ti interessa. Potrai attivare altre soluzioni in un secondo tempo [modificando il programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md). Per ulteriori consigli sulla configurazione del programma, consulta [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).
   * Per la creazione del programma è necessaria almeno una soluzione.
   * Se è stata selezionata l&#39;opzione **[Abilita sicurezza avanzata](#security)**, è possibile selezionare solo tutte le soluzioni per le quali sono disponibili i diritti HIPAA.

   ![Selezione delle soluzioni](assets/setup-prod-select.png)

1. Fare clic sulla freccia che precede il nome della soluzione per visualizzare i componenti aggiuntivi facoltativi, ad esempio selezionando l&#39;opzione del componente aggiuntivo **Commerce** in **Sites**.

   ![Selezione dei componenti aggiuntivi](assets/setup-prod-commerce.png)

1. Dopo aver selezionato le soluzioni e i componenti aggiuntivi, fai clic su **Continua**.

1. Nella scheda **Data di pubblicazione**, inserisci la data di pubblicazione pianificata per il programma di produzione.

   ![Definizione della data di pubblicazione pianificata](assets/set-up-go-live.png)

   * Questa data può essere modificata in qualsiasi momento.
   * Questa data è solo per uso informativo e attiva il widget di pubblicazione sulla pagina [**Panoramica del programma**](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) per fornire collegamenti rapidi alla documentazione sulle best practice di AEM as a Cloud Service, in modo da allinearsi al percorso e garantire un&#39;esperienza di pubblicazione fluida e di successo.

1. Fai clic su **Crea**.

Il programma viene creato da Cloud Manager e visualizzato nella pagina di destinazione, disponibile per la selezione.

![Panoramica di Cloud Manager](assets/navigate-cm.png)

## Opzioni aggiuntive del programma di produzione {#options}

A seconda dei diritti disponibili per l’organizzazione, è possibile che siano disponibili opzioni aggiuntive al momento della creazione di un programma di produzione.

### Sicurezza {#security}

Se disponi dei diritti necessari, la scheda **Sicurezza** verrà visualizzata come prima scheda nella finestra di dialogo **Imposta per produzione**.

La scheda **Sicurezza** fornisce le opzioni per attivare **HIPAA** e/o **Protezione WAF-DDOS** per il programma di produzione.

Adobe Conformità HIPAA e Web Application Firewall (WAF) facilitano la sicurezza basata sul cloud come parte di un approccio multilivello per la protezione contro le vulnerabilità.

* **HIPAA** - Questa opzione abilita l&#39;implementazione della soluzione compatibile con HIPPA di Adobe.
   * [Ulteriori informazioni](https://www.adobe.com/go/hipaa-ready_it) sull’implementazione della soluzione compatibile HIPAA di Adobe.
   * Impossibile abilitare o disabilitare HIPAA dopo la creazione del programma.
* **Protezione WAF-DDOS** - Questa opzione abilita il firewall dell&#39;applicazione Web tramite regole per proteggere l&#39;applicazione.
   * Una volta attivata, è possibile configurare la protezione WAF-DDOS configurando una [pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * Per informazioni su come gestire le regole del filtro del traffico nell&#39;archivio in modo che vengano distribuite correttamente, consulta il documento [Regole del filtro del traffico, incluse le regole WAF](/help/security/traffic-filter-rules-including-waf.md).

![Opzioni di protezione](assets/create-production-program-security.png)

### SLA {#sla}

Se si dispone dei diritti necessari, la scheda **SLA** verrà visualizzata come seconda o terza scheda nella finestra di dialogo **Imposta per la produzione**.

AEM Sites e Forms offrono un contratto di servizio (SLA) standard del 99,9%. L&#39;opzione del **99,99% del contratto del livello di servizio** consente un tempo di attività minimo del 99,99% per gli ambienti di produzione per Sites e/o Forms.

Il 99,99% del contratto di servizio offre vantaggi quali maggiore disponibilità e latenza inferiore e richiede l&#39;applicazione di un&#39;area di pubblicazione aggiuntiva [](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) all&#39;ambiente di produzione nel programma.

![Opzioni SLA](assets/create-production-program-sla.png)

Una volta soddisfatti i [requisiti](#sla-requirements) per abilitare il 99,99% SLA, è necessario eseguire una [pipeline full stack](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per attivarla.

#### Requisiti per il 99,99% SLA {#sla-requirements}

Oltre alle adesioni richieste, il 99,99% degli SLA prevede requisiti aggiuntivi per l&#39;utilizzo.

* Al momento dell’applicazione del 99,99% del contratto di servizio (SLA) al programma, l’organizzazione deve avere a disposizione sia il 99,99% che i diritti aggiuntivi per regione di pubblicazione.
* Per applicare lo SLA del 99,99% al programma, Cloud Manager verificherà che sia disponibile anche un diritto di [ulteriore area di pubblicazione](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) non utilizzato e che possa essere applicato al programma.
* Durante la modifica di un programma, se contiene già un ambiente di produzione con almeno un’area di pubblicazione aggiuntiva, Cloud Manager controlla solo la disponibilità di un diritto SLA del 99,99%.
* Per attivare il 99,99% SLA e il reporting, è necessario che sia stato creato l&#39;[ambiente di produzione/staging](/help/implementing/cloud-manager/manage-environments.md#adding-environments) e che sia stata applicata almeno un&#39;area di pubblicazione aggiuntiva all&#39;ambiente di produzione/staging.
   * Se utilizzi la [rete avanzata,](/help/security/configuring-advanced-networking.md) assicurati di controllare nel documento [Aggiunta di più aree di Publish a un nuovo ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-regions) che non siano presenti consigli in modo da mantenere la connettività in caso di errore regionale.
* Almeno un&#39;area geografica di pubblicazione aggiuntiva deve rimanere nel programma SLA al 99,99%. Gli utenti non possono eliminare l’ultima area di pubblicazione aggiuntiva dal programma SLA al 99,99%.
* Il 99,99% di SLA è supportato per i programmi di produzione in cui è abilitata la soluzione Sites o Forms.
* È necessario eseguire una [pipeline full stack](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per attivare (o disattivare, quando si modifica un programma) lo SLA del 99,99%.

## Accesso al programma {#accessing}

1. Quando visualizzi la scheda del programma nella pagina di destinazione, seleziona il pulsante con i puntini di sospensione per visualizzare le opzioni di menu disponibili.

   ![Panoramica del programma](assets/program-overview.png)

1. Per accedere alla pagina **Panoramica** di Cloud Manager, seleziona **Panoramica del programma**.

1. La principale scheda di invito all’azione nella pagina della panoramica ti guiderà attraverso la creazione di un ambiente, una pipeline non di produzione e infine una pipeline di produzione.

   ![Panoramica del programma](assets/set-up-prod5.png)

>[!TIP]
>
>Per informazioni dettagliate su come esplorare Cloud Manager e la console **I miei programmi**, vedere il documento [Navigazione nell&#39;interfaccia utente di Cloud Manager](/help/implementing/cloud-manager/navigation.md).

>[!NOTE]
>
>A differenza di un [programma sandbox](introduction-sandbox-programs.md#auto-creation), un programma di produzione richiede che l’utente con il ruolo di Cloud Manager appropriato crei il progetto e aggiunga un ambiente tramite l’interfaccia utente self-service.
