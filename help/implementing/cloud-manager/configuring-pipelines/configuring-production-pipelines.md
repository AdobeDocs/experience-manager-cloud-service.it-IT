---
title: Configurazione delle pipeline di produzione
description: Configurazione delle pipeline di produzione
index: false
source-git-commit: 84d04d8399668b8b1051d4edf9de851bca271071
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Configurazione di una pipeline di produzione {#configure-production-pipeline}

Gestione distribuzione è responsabile della configurazione della pipeline di produzione.

>[!NOTE]
>Non è possibile impostare una pipeline di produzione finché non viene completata la creazione di un programma, l’archivio Git dispone di almeno un ramo e viene creato un set di ambiente Produzione e Stage.

Prima di iniziare a distribuire il codice, devi configurare le impostazioni della pipeline dal [!UICONTROL Cloud Manager].

>[!NOTE]
>È possibile modificare le impostazioni della pipeline dopo la configurazione iniziale.

## Aggiunta di una nuova pipeline di produzione {#adding-production-pipeline}

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


1. La **Aggiungi pipeline di produzione** una seconda scheda etichettata come **Codice sorgente**. Puoi selezionare **Codice Stack Completo** e **Codice front-end**. Puoi scegliere la **Archivio** e **Ramo Git**. Selezionare Opzioni di distribuzione di produzione, come illustrato di seguito. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   >[!NOTE]
   >Prima di iniziare a configurare le pipeline front-end, vedere AEM Percorso di creazione rapida di siti per un flusso di lavoro end-to-end tramite lo strumento di creazione rapida AEM facile da utilizzare. Questo sito di documentazione ti aiuterà a semplificare lo sviluppo front-end del tuo sito AEM e a personalizzare rapidamente il tuo sito senza AEM conoscenza back-end.

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


