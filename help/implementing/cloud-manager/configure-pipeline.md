---
title: Configurare la pipeline CI/CD - Cloud Services
description: Configurare la pipeline CI/CD - Cloud Services
translation-type: tm+mt
source-git-commit: 4d5ad99e44446ac40d9798df1c7fabb862065495
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Configurazione della pipeline CI-CD {#configure-ci-cd-pipeline}

In Cloud Manager, ci sono due tipi di pipeline:

* **Pipeline** di produzione:

   È possibile aggiungere una pipeline di produzione solo dopo la creazione di un set di ambienti di produzione e di fase.

   Per ulteriori informazioni, vedere [Impostazione della tubazione di produzione](configure-pipeline.md#setting-up-the-pipeline).

* **Pipeline** non di produzione:

   È possibile aggiungere una pipeline non di produzione dalla pagina **Panoramica** dall&#39;interfaccia utente di Cloud Manager.

   Per ulteriori informazioni, fare riferimento alla sezione [Pipeline non produzione e solo qualità del codice](configure-pipeline.md#non-production-pipelines).

>[!NOTE]
>Per configurare la pipeline, devi:
> * definire il trigger che avvierà la pipeline.
> * definire i parametri che controllano la distribuzione di produzione.
> * configurare i parametri del test delle prestazioni.


## Impostazione della tubazione di produzione {#setting-up-production-pipeline}

Gestione distribuzione è responsabile della configurazione della pipeline di produzione.

>[!NOTE]
>Non è possibile impostare una pipeline di produzione finché non viene completata la creazione di un programma, l&#39;archivio Git ha almeno un ramo e viene creato un ambiente di produzione e fase.

Prima di iniziare a distribuire il codice, devi configurare le impostazioni della pipeline dal [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile modificare le impostazioni della pipeline dopo la configurazione iniziale.

## Configurazione delle impostazioni della pipeline da [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando l&#39;interfaccia utente [!UICONTROL Cloud Manager], è possibile impostare la pipeline di distribuzione.

Per configurare il comportamento e le preferenze della pipeline, effettuate le seguenti operazioni:

1. Fare clic su **Imposta tubazione** per impostare e configurare la tubazione.

   ![](assets/set-up-pipeline1.png)

1. Viene visualizzata la schermata **Setup Pipeline**. Selezionare il ramo e fare clic su **Next**.

   ![](assets/setup-1.png)

1. Configurare le opzioni di distribuzione.

   ![](assets/setup-2.png)

   È possibile definire l&#39;attivatore per avviare la pipeline:

   * **Manuale** : l&#39;utilizzo dell&#39;interfaccia utente consente di avviare manualmente la pipeline.
   * **In Modifiche**  Git: avvia la pipeline CI/CD ogni volta che vengono aggiunti impegni al ramo git configurato. Anche se selezionate questa opzione, potete sempre avviare la pipeline manualmente.

   Durante la configurazione o la modifica della pipeline, Gestione distribuzione ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in una qualsiasi delle porte di qualità.

   Questo è utile per i clienti che desiderano un maggior numero di processi automatizzati. Le opzioni disponibili sono:

   * **Chiedi ogni volta**  - Questa è l&#39;impostazione predefinita e richiede l&#39;intervento manuale su qualsiasi errore importante.
   * **Errore immediato** : se selezionato, la pipeline verrà annullata ogni volta che si verifica un errore importante. In pratica, questo consente di emulare manualmente un utente che rifiuta ogni errore.
   * **Continua immediatamente** : se questa opzione è selezionata, la pipeline procederà automaticamente ogni volta che si verifica un errore importante. Si tratta essenzialmente di un&#39;emulazione manuale di un utente che approva ogni errore.


1. Le impostazioni della pipeline di produzione includono una terza scheda etichettata come **Experience Audit**. Questa opzione fornisce una tabella per i percorsi URL che devono sempre essere inclusi in Experience Audit.

   >[!NOTE]
   >È necessario fare clic su **Aggiungi nuova pagina** per definire il proprio collegamento personalizzato.

   ![](assets/setup-3.png)

   Fate clic su **Aggiungi nuova pagina** per specificare un percorso URL da includere nel controllo dell&#39;esperienza.

   Ad esempio, se desiderate includere `https://wknd.site/us/en/about-us.html` nel controllo dell&#39;esperienza, immettete il percorso `us/en/about-us.html` in questo campo e fate clic su **Salva**.

   ![](assets/exp-audit4.png)

   L’URL visualizzato nella tabella sarà:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   È possibile includere fino a 25 righe. Se non ci sono pagine inviate dall&#39;utente in questa sezione, per impostazione predefinita la pagina iniziale del sito verrà inclusa in Experience Audit.

   Per ulteriori informazioni, fare riferimento a [Informazioni sui risultati dell&#39;audit esperienza](/help/implementing/cloud-manager/experience-audit-testing.md).

   >[!NOTE]
   > Le pagine configurate verranno inviate al servizio e valutate in base alle prestazioni, all&#39;accessibilità, al SEO (ottimizzazione motore di ricerca), alle best practice e ai test PWA (app Web progressiva).

1. Fare clic su **Salva** nella schermata **Modifica tubazione**. La pagina **Panoramica** ora mostra la scheda **Implementa il programma**. Fare clic sul pulsante **Distribuisci** per distribuire il programma.

   ![](assets/configure-pipeline5.png)


## Pipeline di qualità non di produzione e solo codice {#non-production-pipelines}

Oltre alla pipeline principale che viene implementata per la fase e la produzione, i clienti possono impostare altri oleodotti, denominati **Non-Production Pipelines**. Tali pipeline eseguono sempre i passaggi di creazione e qualità del codice. Facoltativamente, possono anche essere distribuiti nell&#39;ambiente Adobe Managed Services.

Nella schermata iniziale, queste condotte sono elencate in una nuova scheda:

1. Accedete alla sezione **Pipeline non di produzione** dalla schermata principale di Cloud Manager.

   ![](assets/configure-pipeline6.png)

1. Fate clic sul pulsante **Aggiungi** per specificare il nome della tubazione, il tipo di tubazione e il ramo Git.

   Inoltre, puoi impostare l&#39;attivatore di distribuzione e un importante comportamento di errore dalle opzioni della pipeline.

   ![](assets/non-prod-pipe1.png)

1. Fate clic su **Salva** e la pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   ![](assets/configure-pipeline8.png)

   * **Modifica** : consente di modificare le impostazioni della pipeline
   * **Build** : passa alla pagina di esecuzione dalla quale è possibile eseguire la pipeline
   * **Manage Git**  - consente all&#39;utente di ottenere le informazioni necessarie per accedere all&#39;archivio Git di Cloud Manager

## Passaggi successivi {#the-next-steps}

Dopo aver configurato la pipeline, è necessario distribuire il codice.

Per ulteriori informazioni, vedere [Distribuzione del codice](deploy-code.md).
