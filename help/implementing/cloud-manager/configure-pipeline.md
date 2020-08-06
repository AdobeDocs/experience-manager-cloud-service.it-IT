---
title: Configurare la pipeline CI/CD - Cloud Services
description: Configurare la pipeline CI/CD - Cloud Services
translation-type: tm+mt
source-git-commit: cd307cb8806f30892b40b20974e19d4a0a34f8dc
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 2%

---


# Configurazione della pipeline CI-CD {#configure-ci-cd-pipeline}

In Cloud Manager, ci sono due tipi di pipeline:

* **Tubi** di produzione:

   È possibile aggiungere una pipeline di produzione solo dopo la creazione di un ambiente di produzione e di fase.

   Per ulteriori informazioni, vedere [Impostazione della tubazione](configure-pipeline.md#setting-up-the-pipeline) .

* **Tubi** non di produzione:

   È possibile aggiungere una pipeline non di produzione dalla pagina **Panoramica** dall&#39;interfaccia utente di Cloud Manager.

   Per ulteriori informazioni, fare riferimento alle tubazioni [](configure-pipeline.md#non-production-pipelines) non di produzione e di qualità del codice.

## Informazioni sul flusso {#understanding-the-flow}

Puoi configurare la pipeline dalla sezione **Pipeline Settings (Impostazioni pipeline)** dell’interfaccia utente di [!UICONTROL Cloud Manager].

Gestione distribuzione è responsabile della configurazione della pipeline. In questo caso, selezionate prima un ramo dall&#39;archivio **Git**.

Per configurare la pipeline, l&#39;utente deve:

* definire il trigger che avvierà la pipeline.
* definire i parametri che controllano la distribuzione di produzione.
* configurare i parametri del test delle prestazioni.

## Impostazione della tubazione {#setting-up-the-pipeline}

>[!CAUTION]
>
>La pipeline non può essere impostata finché non viene completata la creazione di un programma e l&#39;archivio Git ha almeno un ramo.

Prima di iniziare a distribuire il codice, devi configurare le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile modificare le impostazioni della pipeline dopo la configurazione iniziale.

## Configurazione delle impostazioni della pipeline da [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando l&#39;interfaccia utente di [!UICONTROL Cloud Manager] , potete configurare la pipeline di distribuzione.

Per configurare il comportamento e le preferenze della pipeline, effettuate le seguenti operazioni:

1. Fate clic su **Imposta tubazione** per impostare e configurare la tubazione.

   ![](assets/set-up-pipeline1.png)

1. Viene visualizzata la schermata **Configurazione tubazione** . Select the branch and click **Next**.

   ![](assets/setup-pipeline-1.png)

1. Configurare le opzioni di distribuzione.

   ![](assets/setup-pipeline-2.png)

   È possibile definire l&#39;attivatore per avviare la pipeline:

   * **Manuale** : l&#39;utilizzo dell&#39;interfaccia utente consente di avviare manualmente la pipeline.
   * **Su modifiche** Git - avvia la pipeline CI/CD ogni volta che vengono aggiunti impegni al ramo git configurato. Anche se selezionate questa opzione, potete sempre avviare la pipeline manualmente.

   Durante la configurazione o la modifica della pipeline, Gestione distribuzione ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in una qualsiasi delle porte di qualità.

   Questo è utile per i clienti che desiderano un maggior numero di processi automatizzati. Le opzioni disponibili sono:

   * **Chiedi ogni volta** - Questa è l&#39;impostazione predefinita e richiede l&#39;intervento manuale su qualsiasi errore importante.
   * **Errore immediato** - Se selezionato, la pipeline verrà annullata ogni volta che si verifica un errore importante. In pratica, questo consente di emulare manualmente un utente che rifiuta ogni errore.
   * **Continua immediatamente** : se questa opzione è selezionata, la pipeline procederà automaticamente ogni volta che si verifica un errore importante. Si tratta essenzialmente di un&#39;emulazione manuale di un utente che approva ogni errore.


1. Le impostazioni della pipeline di produzione includono una terza scheda etichettata come **Content Audit**.

   ![](assets/content-audit-1.png)

   Questa opzione fornisce una tabella per i percorsi URL che devono sempre essere inclusi nella revisione dei contenuti. L&#39;utente può inserire manualmente un percorso URL da includere. È possibile includere fino a 25 righe. Se non ci sono pagine inviate dall&#39;utente in questa sezione, la pagina iniziale del sito verrà inclusa nel controllo del contenuto come impostazione predefinita.

   >[!NOTE]
   > Le pagine configurate verranno inviate al servizio e valutate in base alle prestazioni, all&#39;accessibilità, al SEO (ottimizzazione motore di ricerca), alle best practice e ai test PWA (app Web progressiva).

   Per ulteriori informazioni, consultate [Informazioni sui risultati](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) dell&#39;audit dei contenuti.

   Fate clic su **Aggiungi nuova esclusione** pagina per specificare un percorso URL da includere nel controllo dei contenuti. Dopo aver aggiunto il percorso, fate clic su **Salva**.

   >[!NOTE]
   >Per attivare il passaggio Controllo contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Per ulteriori informazioni, consulta [Problemi](/help/release-notes/release-notes-cloud/release-notes-current.md#known-issues-cm) noti.

   ![](assets/content-audit2.png)

1. Fate clic su **Salva** nella schermata **Modifica tubazione** . Nella pagina **Panoramica** è ora visualizzata la scheda **Implementa il programma** . Fate clic sul pulsante **Distribuisci** per distribuire il programma.

   ![](assets/configure-pipeline5.png)


## Tubazioni non di produzione e di qualità del codice {#non-production-pipelines}

Oltre alla pipeline principale che viene implementata per fasi e produzione, i clienti sono in grado di impostare altri oleodotti, denominati **Non-Production Pipelines**. Tali pipeline eseguono sempre i passaggi di creazione e qualità del codice. Facoltativamente, possono anche essere distribuiti nell&#39;ambiente Adobe Managed Services.

Nella schermata iniziale, queste condotte sono elencate in una nuova scheda:

1. Accedete alla sezione **Tubi** non di produzione dalla schermata iniziale di Cloud Manager.

   ![](assets/configure-pipeline6.png)

1. Fate clic sul pulsante **Aggiungi** per specificare il nome della tubazione, il tipo di tubazione e il ramo Git.

   Inoltre, puoi impostare l&#39;attivatore di distribuzione e un importante comportamento di errore dalle opzioni della pipeline.

   ![](assets/non-prod-pipe1.png)

1. Fate clic su **Salva** e la pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   ![](assets/configure-pipeline8.png)

   * **Modifica** : consente di modificare le impostazioni della pipeline
   * **Genera** : consente di passare alla pagina di esecuzione dalla quale è possibile eseguire la pipeline
   * **Gestione Git** : consente all&#39;utente di ottenere le informazioni necessarie per accedere all&#39;archivio Git di Cloud Manager

## Passaggi successivi {#the-next-steps}

Dopo aver configurato la pipeline, è necessario distribuire il codice.

Per ulteriori informazioni, consulta [Distribuzione del codice](deploy-code.md) .
