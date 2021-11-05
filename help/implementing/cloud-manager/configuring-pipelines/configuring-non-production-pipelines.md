---
title: Configurazione di una pipeline non di produzione
description: Segui questa pagina per informazioni sulla configurazione di una pipeline non di produzione in Cloud Manager
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# Configurazione di una pipeline non di produzione {#configure-non-production-pipeline}

Oltre alla pipeline principale che viene implementata in fase e produzione, i clienti possono impostare pipeline aggiuntive, denominate pipeline non di produzione .

Esistono due tipi di gasdotti non di produzione:

1. Qualità del codice: Esegue la scansione della qualità del codice sul codice nel ramo git. Questa pipeline esegue i passaggi di creazione e qualità del codice.
1. Distribuzione: Oltre a eseguire i passaggi di build e qualità del codice, questa pipeline distribuisce il codice alla non produzione selezionata per AEM l’ambiente as a Cloud Service.

## Aggiunta di una nuova pipeline non di produzione {#adding-non-production-pipeline}

Nella schermata iniziale, queste pipeline sono elencate in una nuova scheda:

1. Accedere al **Tubi** scheda dalla schermata principale di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Aggiungi pipeline non di produzione**  viene visualizzata la finestra di dialogo. Seleziona il tipo di pipeline che desideri creare, oppure **Pipeline di qualità del codice** o **Pipeline di distribuzione**.

   >[!NOTE]
   >Per le pipeline di distribuzione, è necessario selezionare l&#39;ambiente di distribuzione.

   Inoltre, puoi anche configurare **Trigger distribuzione** e **Comportamento di errori di metrica importanti** da **Opzioni di distribuzione**. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

   Puoi definire i seguenti trigger di distribuzione per avviare la pipeline.

   * **Manuale** - l’utilizzo dell’interfaccia utente consente di avviare manualmente la pipeline.
   * **Su modifiche Git** - avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo git configurato. Anche se selezioni questa opzione, puoi sempre avviare la pipeline manualmente.

      Durante la configurazione o la modifica della pipeline, Deployment Manager ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in uno qualsiasi dei gate di qualità.

      Questo è utile per i clienti che desiderano processi più automatizzati. Le opzioni disponibili sono:
   Puoi definire il comportamento delle metriche di errore importanti per avviare la pipeline.

   * **Chiedi sempre** - Questa è l&#39;impostazione predefinita e richiede l&#39;intervento manuale su qualsiasi errore importante.
   * **Non riuscito immediatamente** - Se selezionata, la pipeline verrà annullata ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente** - Se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che approva manualmente ogni errore.


1. Seleziona **[Codice Stack Completo](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** o **[Codice front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   Se hai selezionato **Codice front-end**, devi selezionare la **Archivio**, **Ramo Git** e **Posizione codice**, come illustrato nella figura seguente:

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   Se hai selezionato **Codice Stack Completo**, devi selezionare la **Archivio** e **Ramo Git**, come illustrato nella figura:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >Se per l’ambiente selezionato esiste già una pipeline del codice di stack completo, questa selezione verrà disabilitata.

   >[!NOTE]
   >Prima di iniziare a configurare le pipeline Front End, consulta [AEM Percorso di creazione di siti rapidi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) per un flusso di lavoro end-to-end tramite lo strumento di creazione rapida AEM facile da usare. Questo sito di documentazione ti aiuterà a semplificare lo sviluppo front-end del tuo sito AEM e a personalizzare rapidamente il tuo sito senza AEM conoscenza back-end.

1. La nuova pipeline non di produzione creata viene ora visualizzata nella **Tubi** il Card.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   La pipeline viene visualizzata sulla scheda nella schermata iniziale con quattro azioni, come illustrato di seguito:

   * **Aggiungi** - consente di aggiungere una nuova pipeline.
   * **Mostra tutto** - consente all&#39;utente di visualizzare tutte le pipeline.
   * **Accesso alle informazioni sul repository** - consente all’utente di ottenere le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
   * **Ulteriori informazioni** - Informazioni sulla risorsa della documentazione della pipeline CI/CD.