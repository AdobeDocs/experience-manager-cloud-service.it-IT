---
title: Configurare la pipeline CI/CD - Cloud Services
description: Configurare la pipeline CI/CD - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: 03c058c17e8a9ff5a0be9203a65207bb367a02a6
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Configurazione della pipeline CI-CD {#configure-ci-cd-pipeline}

In Cloud Manager sono disponibili due tipi di pipeline:

* **Pipeline** di produzione:

   È possibile aggiungere una pipeline di produzione solo dopo la creazione di un set di ambienti di produzione e stage.

   Per ulteriori informazioni, consulta [Configurazione della pipeline di produzione](configure-pipeline.md#setting-up-the-pipeline) .

* **Pipeline** non di produzione:

   È possibile aggiungere una pipeline non di produzione dalla pagina **Panoramica** dall’interfaccia utente di Cloud Manager.

   Per ulteriori informazioni, consulta [Solo pipeline non di produzione e qualità del codice](configure-pipeline.md#non-production-pipelines) .

   >[!NOTE]
   >Per configurare la pipeline, devi:
   > * definisci il trigger che avvierà la pipeline.
   > * definire i parametri che controllano la distribuzione di produzione.
   > * configurare i parametri del test delle prestazioni.


## Impostazione della pipeline di produzione {#setting-up-production-pipeline}

Gestione distribuzione è responsabile della configurazione della pipeline di produzione.

>[!NOTE]
>Non è possibile impostare una pipeline di produzione finché non viene completata la creazione di un programma, l’archivio Git dispone di almeno un ramo e viene creato un set di ambiente Produzione e Stage.

Prima di iniziare a distribuire il codice, devi configurare le impostazioni della pipeline da [!UICONTROL Cloud Manager].

>[!NOTE]
>
>È possibile modificare le impostazioni della pipeline dopo la configurazione iniziale.

### Aggiunta di una nuova pipeline di produzione {#adding-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando l&#39;interfaccia utente di [!UICONTROL Cloud Manager], puoi aggiungere una pipeline di produzione.

Segui questi passaggi per configurare il comportamento e le preferenze per la pipeline di produzione:

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .
Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline di produzione**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **Viene visualizzata la finestra di dialogo Aggiungi** pipeline di produzione . Immettere il nome della pipeline.

   Inoltre, puoi anche impostare **Trigger distribuzione** e **Comportamento errori di metrica importanti** da **Opzioni di distribuzione**. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   Puoi definire gli attivatori di distribuzione per avviare la pipeline.

   * **Manuale** : utilizzando l’interfaccia utente si avvia manualmente la pipeline.
   * **In Modifiche Git** : avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Anche se selezioni questa opzione, puoi sempre avviare la pipeline manualmente.

      Durante la configurazione o la modifica della pipeline, Deployment Manager ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in uno qualsiasi dei gate di qualità.

      Questo è utile per i clienti che desiderano processi più automatizzati. Le opzioni disponibili sono:
   Puoi definire il comportamento delle metriche di errore importanti per avviare la pipeline.

   * **Chiedi ogni volta**  - Questa è l&#39;impostazione predefinita e richiede un intervento manuale su qualsiasi errore importante.
   * **Non riuscito Immediatamente**  - Se selezionato, la pipeline verrà annullata ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente** : se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che approva manualmente ogni errore.


1. La finestra di dialogo **Aggiungi pipeline di produzione** include una seconda scheda etichettata come **Codice sorgente**. **È selezionato il** codice Stack completo. È possibile scegliere il **Repository** e il **Ramo Git**. Selezionare Opzioni di distribuzione di produzione, come illustrato di seguito. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   Opzioni di distribuzione della produzione:

   * **Pausa prima della distribuzione in produzione**: Questa opzione consente la pausa della fase di distribuzione prima della produzione.
   * **Pianificato**: Questa opzione consente all&#39;utente di abilitare la distribuzione di produzione pianificata.

1. La finestra di dialogo **Aggiungi pipeline di produzione** include una terza scheda etichettata come **Audit esperienza**. Questa opzione fornisce una tabella per i percorsi URL che devono sempre essere inclusi nel controllo di esperienza.

   >[!NOTE]
   >Fai clic su **Aggiungi pagina** per definire un collegamento personalizzato.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   Fai clic su **Aggiungi nuova pagina** per fornire un percorso URL da includere nel controllo di esperienza.

   Ad esempio, se desideri includere `https://wknd.site/us/en/about-us.html` in Experience Audit, immetti il percorso `us/en/about-us.html` in questo campo e fai clic su **Salva**.

   ![](assets/exp-audit4.png)

   L’URL visualizzato nella tabella sarà:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   È possibile includere un massimo di 25 righe. Se in questa sezione non sono presenti pagine inviate dall’utente, per impostazione predefinita la home page del sito verrà inclusa in Experience Audit.

   Per ulteriori informazioni, consulta [Informazioni sui risultati di Experience Audit](/help/implementing/cloud-manager/experience-audit-testing.md) .

   >[!NOTE]
   > Le pagine configurate verranno inviate al servizio e valutate in base alle prestazioni, all’accessibilità, all’ottimizzazione SEO (Search Engine Optimization), alle best practice e ai test PWA (Progressive Web App).

1. Fai clic su **Salva**. La pipeline di produzione appena creata viene ora visualizzata nella scheda **Pipelines** .

   La pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   * **Aggiungi** : consente di aggiungere una nuova pipeline.
   * **Accesso a informazioni sul repository** : consente all’utente di ottenere le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
   * **Ulteriori informazioni** : descrive la risorsa della documentazione della pipeline CI/CD.

### Modifica di una pipeline di produzione {#editing-prod-pipeline}

Puoi modificare le configurazioni della pipeline dalla pagina **Panoramica del programma** .

Per modificare la pipeline configurata, effettua le seguenti operazioni:

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .

1. Fai clic su **..** dalla scheda **Pipelines** e fai clic su **Modifica**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. Viene visualizzata la finestra di dialogo **Modifica pipeline di produzione**.

   1. La scheda **Configurazione** ti consente di aggiornare il **Nome pipeline**, **Trigger distribuzione** e **Comportamento di errore delle metriche importanti**.

      >[!NOTE]
      >Per informazioni su come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) .

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. La scheda **Origine** offre un’opzione per selezionare o deselezionare le opzioni **Pausa prima della distribuzione in Produzione** e **Pianificata** da **Opzioni di distribuzione di produzione**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. L’opzione **Audit esperienze** consente di aggiornare o aggiungere nuove pagine.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. Una volta completata la modifica della pipeline, fai clic su **Aggiorna** .

### Azioni aggiuntive della pipeline di produzione {#additional-prod-actions}

#### Esecuzione di una pipeline di produzione {#run-prod}

Puoi eseguire la pipeline di produzione dalla scheda Pipelines :

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .

1. Fai clic su **..** dalla scheda **Pipelines** e fai clic su **Esegui**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### Eliminazione di una pipeline di produzione {#delete-prod}

Puoi eliminare la pipeline di produzione dalla scheda Pipelines :

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .

1. Fai clic su **..** dalla scheda **Pipelines** e fai clic su **Elimina**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >Un utente con il ruolo di Deployment Manager può ora eliminare la pipeline di produzione in modo self-service tramite l’opzione **Elimina** dalla scheda Pipeline.


## Solo pipeline non di produzione e di qualità del codice {#non-production-pipelines}

Oltre alla pipeline principale che viene implementata in fase e produzione, i clienti possono impostare pipeline aggiuntive, denominate **Non-Production Pipelines**. Queste pipeline eseguono sempre i passaggi di creazione e qualità del codice. Facoltativamente, possono anche distribuire AEM ambiente as a Cloud Service.

### Aggiunta di una nuova pipeline non di produzione {#adding-non-production-pipeline}

Nella schermata iniziale, queste pipeline sono elencate in una nuova scheda:

1. Accedi alla scheda **Pipelines** dalla schermata iniziale di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Viene visualizzata la finestra di dialogo Aggiungi**  pipeline non di produzione. Selezionare il tipo di pipeline che si desidera creare, ovvero **Pipeline di qualità del codice** o **Pipeline di distribuzione**.

   Inoltre, puoi anche impostare **Trigger distribuzione** e **Comportamento errori di metrica importanti** da **Opzioni di distribuzione**. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **È selezionato il** codice Stack completo. È possibile scegliere il **Repository** e il **Ramo Git**. Fai clic su **Salva**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. La pipeline non di produzione appena creata viene ora visualizzata nella scheda **Pipelines** .

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   La pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   * **Aggiungi** : consente di aggiungere una nuova pipeline.
   * **Accesso a informazioni sul repository** : consente all’utente di ottenere le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
   * **Ulteriori informazioni** : descrive la risorsa della documentazione della pipeline CI/CD.

### Modifica di una pipeline non di produzione {#editing-nonprod-pipeline}

Puoi modificare le configurazioni della pipeline dalla **scheda Pipelines** dalla pagina **Panoramica del programma** .

Per modificare la pipeline non di produzione configurata, effettua le seguenti operazioni:

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .

1. Seleziona la pipeline non di produzione e fai clic su **..**. Fai clic su **Modifica**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. Viene visualizzata la finestra di dialogo **Modifica pipeline di produzione**.

   1. La scheda **Configurazione** ti consente di aggiornare il **Nome pipeline**, **Trigger distribuzione** e **Comportamento errori di metrica importanti**.

      >[!NOTE]
      >Per informazioni su come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) .

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. La scheda **Codice sorgente** consente di aggiornare il **Repository** e il **Ramo Git**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. Fai clic su **Aggiorna** una volta completata la modifica della pipeline non di produzione.

### Azioni aggiuntive di pipeline non di produzione {#additional-nonprod-actions}

#### Esecuzione di una pipeline non di produzione {#run-nonprod}

Puoi eseguire la pipeline di produzione dalla scheda Pipelines :

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .

1. Fai clic su **..** dalla scheda **Pipelines** e fai clic su **Esegui**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### Eliminazione di una pipeline non di produzione {#delete-nonprod}

Puoi eliminare la pipeline di produzione dalla scheda Pipelines :

1. Passa alla scheda **Pipelines** dalla pagina **Panoramica del programma** .

1. Fai clic su **..** dalla scheda **Pipelines** e fai clic su **Elimina**, come illustrato nella figura seguente.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## Passaggi successivi {#the-next-steps}

Dopo aver configurato la pipeline, devi distribuire il codice.

Per ulteriori informazioni, consulta [Implementare il codice](deploy-code.md) .
