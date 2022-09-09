---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.6.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.5.0
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.6.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM 2021.6.0.

>[!NOTE]
>Per visualizzare le note sulla versione corrente per Adobe Experience Manager as a Cloud Service, fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.6.0 è il 10 giugno 2021.

### Novità {#what-is-new}

* Preview Service verrà distribuito su base continua a tutti i programmi. I clienti riceveranno una notifica interna al prodotto quando il loro programma è abilitato per Preview Service. Fai riferimento a [Accesso al servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) per ulteriori dettagli.

* Le dipendenze Maven scaricate durante il passaggio di creazione ora verranno memorizzate nella cache tra le esecuzioni della pipeline. Questa funzione verrà attivata per i clienti nelle prossime settimane.

* È ora possibile modificare il nome del programma tramite la finestra di dialogo modifica programma.

* Il nome del ramo predefinito utilizzato sia durante la creazione del progetto che nel comando push predefinito tramite gestione flussi di lavoro Git è stato modificato in `main`.

* L’esperienza di modifica del programma nell’interfaccia utente è stata aggiornata.

* Regola di qualità `ImmutableMutableMixCheck` è stato aggiornato per classificare `/oak:index` nodi immutabili.

* Le norme di qualità `CQBP-84` e `CQBP-84--dependencies` sono stati consolidati in un&#39;unica regola. Come parte di questo consolidamento, la scansione delle dipendenze identifica più accuratamente i problemi nelle dipendenze di terze parti che vengono distribuiti nel runtime di AEM.

* Per evitare confusione, le righe del segmento Pubblica AEM e Pubblica dispatcher nella pagina Dettagli ambiente sono state consolidate.

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* È stata aggiunta una nuova regola di qualità del codice per convalidare la struttura di `damAssetLucene` indici. Fai riferimento a [Indici Oak Lucene della risorsa DAM personalizzati](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) per ulteriori dettagli.

* Nella pagina dei dettagli dell’ambiente vengono ora visualizzati più nomi di dominio per i servizi di pubblicazione e anteprima (a seconda dei casi). Fai riferimento a [Dettagli dell&#39;ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#viewing-environment) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes}

* Le definizioni dei nodi JCR contenenti una nuova riga dopo che il nome dell&#39;elemento principale non è stato analizzato correttamente.

* L&#39;API degli archivi di elenco non filtrerebbe gli archivi eliminati.

* Veniva visualizzato un messaggio di errore non corretto quando veniva fornito un valore non valido per il passaggio di pianificazione.

* A volte l&#39;utente può vedere un verde *attivo* stato accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Alcune sequenze di modifica dei programmi potrebbero impedire la creazione o la modifica della pipeline di produzione.

* Alcune sequenze di modifica del programma potrebbero causare **Panoramica** visualizzazione di un messaggio fuorviante per eseguire nuovamente la configurazione del programma.
