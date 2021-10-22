---
title: Configurare la pipeline CI/CD - Cloud Services
description: Configurare la pipeline CI/CD - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: f3743451f7aeadae26e8a6814cfbed9667c4a242
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# Configurazione della pipeline CI-CD {#configure-ci-cd-pipeline}

In Cloud Manager sono disponibili due tipi di pipeline:

* **Pipeline di produzione**:

   È possibile aggiungere una pipeline di produzione solo dopo la creazione di un set di ambienti di produzione e stage.

   Fai riferimento a [Impostazione della pipeline di produzione](configure-pipeline.md#setting-up-the-pipeline) per ulteriori dettagli.

* **Pipeline non di produzione**:

   È possibile aggiungere una pipeline non di produzione dalla **Panoramica** dall’interfaccia utente di Cloud Manager.

   Fai riferimento a [Solo pipeline non di produzione e di qualità del codice](configure-pipeline.md#non-production-pipelines) per ulteriori dettagli.

   >[!NOTE]
   >Per configurare la pipeline, devi:
   > * definisci il trigger che avvierà la pipeline.
   > * definire i parametri che controllano la distribuzione di produzione.
   > * configurare i parametri del test delle prestazioni.


## Impostazione della pipeline di produzione {#setting-up-production-pipeline}

Gestione distribuzione è responsabile della configurazione della pipeline di produzione.

>[!NOTE]
>Non è possibile impostare una pipeline di produzione finché non viene completata la creazione di un programma, l’archivio Git dispone di almeno un ramo e viene creato un set di ambiente Produzione e Stage.

Prima di iniziare a distribuire il codice, devi configurare le impostazioni della pipeline dal [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile modificare le impostazioni della pipeline dopo la configurazione iniziale.

### Aggiunta di una nuova pipeline di produzione {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando [!UICONTROL Cloud Manager] Interfaccia utente, puoi aggiungere una pipeline di produzione.

Segui questi passaggi per configurare il comportamento e le preferenze per la pipeline di produzione:

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.
Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline di produzione**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Aggiungi pipeline di produzione** viene visualizzata la finestra di dialogo. Immettere il nome della pipeline.

   Inoltre, puoi anche configurare **Trigger distribuzione** e **Comportamento di errori di metrica importanti** da **Opzioni di distribuzione**. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Puoi definire gli attivatori di distribuzione per avviare la pipeline.

   * **Manuale** - l’utilizzo dell’interfaccia utente consente di avviare manualmente la pipeline.
   * **Su modifiche Git** - avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo git configurato. Anche se selezioni questa opzione, puoi sempre avviare la pipeline manualmente.

      Durante la configurazione o la modifica della pipeline, Deployment Manager ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in uno qualsiasi dei gate di qualità.

      Questo è utile per i clienti che desiderano processi più automatizzati. Le opzioni disponibili sono:
   Puoi definire il comportamento delle metriche di errore importanti per avviare la pipeline.

   * **Chiedi sempre** - Questa è l&#39;impostazione predefinita e richiede l&#39;intervento manuale su qualsiasi errore importante.
   * **Non riuscito immediatamente** - Se selezionata, la pipeline verrà annullata ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente** - Se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che approva manualmente ogni errore.


1. La **Aggiungi pipeline di produzione** una seconda scheda etichettata come **Codice sorgente**. **Codice Stack Completo** è selezionato. Puoi scegliere la **Archivio** e **Ramo Git**. Selezionare Opzioni di distribuzione di produzione, come illustrato di seguito. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Opzioni di distribuzione della produzione:

   * **Sospendi prima della distribuzione in produzione**: Questa opzione consente la pausa della fase di distribuzione prima della produzione.
   * **Pianificato**: Questa opzione consente all&#39;utente di abilitare la distribuzione di produzione pianificata.

1. La **Aggiungi pipeline di produzione** una terza scheda etichettata come **Audit delle esperienze**. Questa opzione fornisce una tabella per i percorsi URL che devono sempre essere inclusi nel controllo di esperienza.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >È necessario fare clic su **Aggiungi pagina** per definire un collegamento personalizzato. Il percorso della pagina deve iniziare con `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   Fai clic su **Aggiungi nuova pagina** per fornire un percorso URL da includere nel controllo di audit esperienza.

   Ad esempio, se desideri includere `https://wknd.site/us/en/about-us.html` in Audit esperienze, immetti il percorso `/us/en/about-us.html` in questo campo e fai clic su **Salva**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   L’URL visualizzato nella tabella sarà:

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   È possibile includere un massimo di 25 righe. Se in questa sezione non sono presenti pagine inviate dall’utente, per impostazione predefinita la home page del sito verrà inclusa in Experience Audit.

   Fai riferimento a [Risultati di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) per ulteriori dettagli.

   >[!NOTE]
   > Le pagine configurate verranno inviate al servizio e valutate in base alle prestazioni, all’accessibilità, all’ottimizzazione SEO (Search Engine Optimization), alle best practice e ai test PWA (Progressive Web App).

1. Fai clic su **Salva**. La nuova pipeline di produzione creata viene ora visualizzata in **Tubi** il Card.

   La pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   * **Aggiungi** - consente di aggiungere una nuova pipeline.
   * **Accesso alle informazioni sul repository** - consente all’utente di ottenere le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
   * **Ulteriori informazioni** - Informazioni sulla risorsa della documentazione della pipeline CI/CD.

### Modifica di una pipeline di produzione {#editing-prod-pipeline}

Puoi modificare le configurazioni della pipeline dalla sezione **Panoramica del programma** pagina.

Per modificare la pipeline configurata, effettua le seguenti operazioni:

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Modifica**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. La **Modifica pipeline di produzione** viene visualizzata la finestra di dialogo.

   1. La **Configurazione** consente di aggiornare **Nome della pipeline**, **Trigger distribuzione** e **Comportamento di errore delle metriche importanti**.

      >[!NOTE]
      >Vedi [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. La **Origine** scheda ti offre un’opzione per selezionare o deselezionare **Sospendi prima dell’implementazione in produzione** e **Pianificato** opzioni da **Opzioni di distribuzione della produzione**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. La **Audit delle esperienze** consente di aggiornare o aggiungere nuove pagine.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Fai clic su **Aggiorna** una volta completata la modifica della pipeline.

### Azioni aggiuntive della pipeline di produzione {#additional-prod-actions}

#### Esecuzione di una pipeline di produzione {#run-prod}

Puoi eseguire la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Esegui**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### Eliminazione di una pipeline di produzione {#delete-prod}

Puoi eliminare la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Elimina**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Un utente con il ruolo di Deployment Manager ora può eliminare la pipeline di produzione in modo self-service tramite il **Elimina** dalla scheda Pipeline.


## Solo pipeline non di produzione e di qualità del codice {#non-production-pipelines}

Oltre alla pipeline principale che viene implementata in fase e produzione, i clienti possono impostare pipeline aggiuntive, denominate pipeline non di produzione .
Esistono due tipi di gasdotti non di produzione:

1. Qualità del codice: Esegue la scansione della qualità del codice sul codice nel ramo git. Questa pipeline esegue i passaggi di creazione e qualità del codice.
1. Distribuzione: Oltre a eseguire i passaggi di build e qualità del codice, questa pipeline distribuisce il codice alla non produzione selezionata per AEM l’ambiente as a Cloud Service.

### Aggiunta di una nuova pipeline non di produzione {#adding-non-production-pipeline}

Nella schermata iniziale, queste pipeline sono elencate in una nuova scheda:

1. Accedere al **Tubi** scheda dalla schermata principale di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Aggiungi pipeline non di produzione**  viene visualizzata la finestra di dialogo. Seleziona il tipo di pipeline che desideri creare, oppure **Pipeline di qualità del codice** o **Pipeline di distribuzione**.

   >[!NOTE]
   >Per le pipeline di distribuzione, è necessario selezionare l&#39;ambiente di distribuzione.

   Inoltre, puoi anche configurare **Trigger distribuzione** e **Comportamento di errori di metrica importanti** da **Opzioni di distribuzione**. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **Codice Stack Completo** è selezionato. Puoi scegliere la **Archivio** e **Ramo Git**. Fai clic su **Salva**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. La nuova pipeline non di produzione creata viene ora visualizzata nella **Tubi** il Card.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   La pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   * **Aggiungi** - consente di aggiungere una nuova pipeline.
   * **Accesso alle informazioni sul repository** - consente all’utente di ottenere le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
   * **Ulteriori informazioni** - Informazioni sulla risorsa della documentazione della pipeline CI/CD.

### Modifica di una pipeline non di produzione {#editing-nonprod-pipeline}

Puoi modificare le configurazioni della pipeline dalla sezione **Scheda pipeline** da **Panoramica del programma** pagina.

Per modificare la pipeline non di produzione configurata, effettua le seguenti operazioni:

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Seleziona la pipeline non di produzione e fai clic su **...**. Fai clic su **Modifica**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. La **Modifica pipeline di produzione** viene visualizzata la finestra di dialogo.

   1. La **Configurazione** consente di aggiornare **Nome della pipeline**, **Trigger distribuzione** e **Comportamento di errori di metrica importanti**.

      >[!NOTE]
      >Vedi [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. La **Codice sorgente** consente di aggiornare **Archivio** e **Ramo Git**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Fai clic su **Aggiorna** una volta completata la modifica della pipeline non di produzione.

### Azioni aggiuntive di pipeline non di produzione {#additional-nonprod-actions}

#### Esecuzione di una pipeline non di produzione {#run-nonprod}

Puoi eseguire la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Esegui**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Eliminazione di una pipeline non di produzione {#delete-nonprod}

Puoi eliminare la pipeline di produzione dalla scheda Pipelines :

1. Passa a **Tubi** scheda da **Panoramica del programma** pagina.

1. Fai clic su **...** dal **Tubi** scheda e fai clic su **Elimina**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## Passaggi successivi {#the-next-steps}

Dopo aver configurato la pipeline, devi distribuire il codice.

Vedi [Distribuisci il codice](deploy-code.md) per ulteriori dettagli.
