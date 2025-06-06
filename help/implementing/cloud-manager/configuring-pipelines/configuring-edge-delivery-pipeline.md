---
title: Aggiungere una pipeline di Edge Delivery
description: Scopri come aggiungere una pipeline Edge Delivery per generare e distribuire il codice negli ambienti di produzione.
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Adottatore anticipato" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: acb919474bfe4285c889b8646f731285f5b759ba
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 38%

---



# Aggiungere una pipeline di Edge Delivery {#configure-production-pipeline}

Scopri come configurare le pipeline di Edge Delivery per generare e distribuire il codice negli ambienti di produzione. Una pipeline di produzione distribuisce prima il codice nell’ambiente di staging. Dopo l’approvazione, distribuisce lo stesso codice nell’ambiente di produzione.

Per configurare le pipeline di produzione, l’utente deve avere il ruolo **[Responsabile dell’implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

>[!NOTE]
>
>Non è possibile impostare una pipeline di produzione finché non si verifica quanto segue:
>
>* Il programma viene creato.
>* L’archivio Git dispone di almeno un ramo.
>* Vengono creati gli ambienti di produzione e di staging.

Prima di iniziare la distribuzione del codice, configura le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiungere una nuova pipeline di Edge Delivery {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente che utilizza l’interfaccia utente di [!UICONTROL Cloud Manager], puoi aggiungere una pipeline di produzione seguendo la procedura riportata di seguito.

>[!TIP]
>
>Prima di configurare una pipeline front-end, consulta [Percorso per la creazione rapida dei siti di AEM](/help/journey-sites/quick-site/overview.md) per una guida end-to-end all’intuitivo strumento AEM per la creazione rapida dei siti. Questo percorso può aiutarti a semplificare lo sviluppo front-end del tuo sito AEM, consentendoti di personalizzare rapidamente il tuo sito senza alcuna conoscenza del back-end di AEM.

**Per aggiungere una nuova pipeline Edge Delivery:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma** e fai clic su **Aggiungi** per selezionare **Aggiungi pipeline di produzione**.

   ![Scheda Pipeline nella panoramica del responsabile del programma](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Viene visualizzata la finestra di dialogo **Aggiungi pipeline di produzione**. Per identificare la pipeline, fornisci un **nome della pipeline** con le seguenti opzioni. Fai clic su **Continua**.

   **Trigger distribuzione**: quando si definiscono i trigger della distribuzione per avviare la pipeline, le opzioni disponibili sono le seguenti.

   * **Manuale** - Avvia la pipeline manualmente.
   * **Su modifiche Git** - Avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Con questa opzione è comunque possibile avviare la pipeline manualmente secondo necessità.

   **Comportamento in caso di errori relativi a metriche importanti**: durante la configurazione o la modifica della pipeline, l’utente con il ruolo **Responsabile dell’implementazione** può definire il comportamento della pipeline in caso di errore importante rilevato da un gate di qualità. Opzioni disponibili:

   * **Chiedi ogni volta** - Impostazione predefinita. Richiede l&#39;intervento manuale in caso di errori importanti.
   * **Interrompi subito**: selezionando questa opzione, la pipeline viene annullata ogni volta che si verifica un errore importante. In sostanza, questo processo simula un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente** - Se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo processo simula un utente che approva manualmente ogni errore.

   ![Configurazione della pipeline di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Nella scheda **Codice Source**, seleziona il tipo di codice da elaborare con la pipeline.

   * **[Configurare una pipeline del codice full stack](#full-stack-code)**
   * **[Configurare una pipeline di distribuzione di destinazione](#targeted-deployment)**

Per ulteriori informazioni sui tipi di pipeline, consulta [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

I passaggi per completare la creazione della pipeline di produzione variano a seconda del tipo di codice sorgente selezionato. Accedi ai collegamenti riportati qui sopra per passare alla sezione successiva del documento e completare la configurazione della pipeline.

