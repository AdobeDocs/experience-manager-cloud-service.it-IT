---
title: Aggiunta di pipeline di produzione
description: Aggiunta di pipeline di produzione
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---


# Creazione di una pipeline di produzione {#create-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando l&#39;interfaccia utente di [!UICONTROL Cloud Manager], puoi configurare la pipeline di distribuzione.

Per configurare il comportamento e le preferenze per la pipeline, effettua le seguenti operazioni:

1. Fai clic su **Imposta pipeline** per impostare e configurare la pipeline.

   ![](assets/set-up-pipeline1.png)

1. Viene visualizzata la schermata **Pipeline di installazione**. Seleziona il ramo e fai clic su **Avanti**.

   ![](assets/setup-1.png)

1. Configura le opzioni di distribuzione.

   ![](assets/setup-pipeline.png)

   Puoi definire il trigger per avviare la pipeline:

   * **Manuale** : utilizzando l’interfaccia utente si avvia manualmente la pipeline.
   * **In Modifiche Git** : avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Anche se selezioni questa opzione, puoi sempre avviare la pipeline manualmente.

   Durante la configurazione o la modifica della pipeline, Deployment Manager ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in uno qualsiasi dei gate di qualità.

   Questo è utile per i clienti che desiderano processi più automatizzati. Le opzioni disponibili sono:

   * **Chiedi ogni volta**  - Questa è l&#39;impostazione predefinita e richiede un intervento manuale su qualsiasi errore importante.
   * **Annulla immediatamente** : se selezionata, la pipeline verrà annullata ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che rifiuta manualmente ogni errore.
   * **Approva immediatamente** : se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che approva manualmente ogni errore.


1. Le impostazioni della pipeline di produzione includono una terza scheda etichettata come **Audit esperienze**. Questa opzione fornisce una tabella per i percorsi URL che devono sempre essere inclusi nel controllo di esperienza.

   >[!NOTE]
   >Fai clic su **Aggiungi nuova pagina** per definire il tuo collegamento personalizzato.

   ![](assets/setup-3.png)

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

1. Fai clic su **Salva** nella schermata **Modifica pipeline** . Nella pagina **Panoramica** viene ora visualizzata la scheda **Implementa il programma** . Fare clic sul pulsante **Distribuisci** per distribuire il programma.

   ![](assets/configure-pipeline5.png)

