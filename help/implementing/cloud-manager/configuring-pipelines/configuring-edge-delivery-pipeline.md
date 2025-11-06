---
title: Aggiungere una pipeline di Edge Delivery
description: Scopri come aggiungere una pipeline Edge Delivery per generare e distribuire il codice negli ambienti di produzione.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 10%

---

# Aggiungere una pipeline di Edge Delivery {#configure-production-pipeline}

<!--badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

Scopri come configurare le pipeline di Edge Delivery per generare e distribuire il codice negli ambienti di produzione. Le pipeline di Edge Delivery consentono di configurare le funzioni, tra cui l’inoltro dei registri e la rete CDN gestita da Adobe.

Per un elenco delle configurazioni supportate, vedere [Utilizzare le pipeline di configurazione - configurazioni supportate](/help/operations/config-pipeline.md#configurations).

Per configurare le pipeline di produzione, l’utente deve avere il ruolo **[Responsabile dell’implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

>[!IMPORTANT]
>
>Non è possibile configurare una pipeline di Edge Delivery finché non si verifica quanto segue:
>
>* Viene creato un programma che contiene un sito Edge Delivery Services e un dominio mappato. In caso contrario, l&#39;opzione denominata **Aggiungi pipeline Edge Delivery** risulta disabilitata nell&#39;interfaccia utente e una descrizione comandi spiega i requisiti mancanti. Vedi [Creare un sito Edge Delivery in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)
>* L’archivio Git dispone di almeno un ramo. Vedi [Gestione archivi in Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).
>* Vengono creati gli ambienti di produzione e di staging. Consulta [Introduzione alle pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

<!-- CMGR‑69680 -->

Prima di iniziare la distribuzione del codice, configura le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

**Per aggiungere una pipeline Edge Delivery:**

1. Accedi a Cloud Manager all&#39;indirizzo [experience.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
1. Selezionare un&#39;organizzazione desiderata.
1. Nella console **Programmi** fare clic su un programma.

   ![Pagina Programmi in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. Effettua una delle seguenti operazioni:

   * **Aggiungi una pipeline di Edge Delivery dalla scheda Pipeline**

      1. Nella barra a sinistra, sotto **Programma**, fai clic sull&#39;icona **![Panoramica](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [Panoramica](/help/implementing/cloud-manager/navigation.md#my-programs)**.
      1. Nella pagina **Panoramica programma**, nella scheda **Pipeline**, fai clic su **![Segno più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)Aggiungi**, quindi seleziona **Aggiungi pipeline Edge Delivery**.

         ![Scheda Pipeline nella pagina Panoramica del programma](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

         >[!TIP]
         >
         >Oltre a utilizzare la scheda **Pipeline** come illustrato nella schermata precedente, puoi anche gestire la pipeline dalla pagina **Pipeline**.
         >
         >![Widget pipeline Edge Delivery con nome pipeline, stato, repository e ramo](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

   * **Aggiungi una pipeline di Edge Delivery dalla pagina Pipeline**

      1. Nella barra a sinistra, sotto **Programma**, fai clic sull&#39;icona **![Flusso di lavoro o Pipeline](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) Pipeline**.
      1. Nella pagina Pipeline, nell&#39;angolo superiore destro, fai clic su **Aggiungi pipeline** > **Aggiungi pipeline Edge Delivery**.

         ![Pagina Pipeline con il pulsante Aggiungi pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

         >[!TIP]
         >
         >Nell&#39;angolo in alto a sinistra, fai clic su **Filtri**, quindi seleziona la casella di controllo **Consegna Edge** nella sezione **Tipo di consegna** per filtrare l&#39;elenco solo per le pipeline di Edge Delivery (ovvero per le pipeline che utilizzano Edge Delivery Services). <!-- (CMGR-69682) -->
         >
         >![Pannello dei filtri che mostra il nuovo tipo di distribuzione Edge Delivery e Pubblica consegna](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

1. Nella finestra di dialogo **Aggiungi pipeline di Edge Delivery**, digita un&#39;etichetta descrittiva della pipeline nel campo di testo **Nome pipeline**.

   ![Finestra di dialogo Aggiungi pipeline di Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. Selezionare l&#39;opzione **Trigger distribuzione** della pipeline desiderata.

   * **Manuale** - Avvio della distribuzione.
   * **Su modifiche Git** - Il commit Git avvia automaticamente la distribuzione. Se necessario, è comunque possibile avviare la pipeline manualmente.

1. Fai clic su **Continua**.

1. In **Codice Source**, impostare le opzioni seguenti:

   * **Ambiente di distribuzione** - Visualizza il campo dell&#39;ambiente di destinazione. Rimane di sola lettura.

   * **Archivio**: utilizza l&#39;elenco a discesa per puntare la pipeline esattamente all&#39;archivio Git che memorizza la configurazione di Edge Delivery.

     Consulta anche [Aggiungere e gestire archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git**: utilizza l&#39;elenco a discesa per selezionare un ramo specifico all&#39;interno dell&#39;archivio scelto. Se necessario, fai clic sull&#39;icona ![Ricicla o Aggiorna](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) per ricaricare l&#39;elenco a discesa del ramo Git dopo i push recenti.
   * **Posizione codice** - Definisce il percorso della cartella all&#39;interno dell&#39;archivio in cui inizia il codice pronto per la pipeline ( `/` è uguale alla directory principale dell&#39;archivio).

   ![Pipeline di configurazione](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. Fai clic su **Salva**.

Ora puoi [gestire la pipeline](managing-pipelines.md) dalla scheda **Pipeline** nella pagina **Panoramica del programma** o dalla pagina **Pipeline**.


![Widget pipeline Edge Delivery con nome pipeline, stato, repository e ramo](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)



