---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.5.0
feature: Informazioni sulla versione
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 3%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.6.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.6.0.

>[!NOTE]
>Per visualizzare il Cloud Service delle note sulla versione corrente per Adobe Experience Manager, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.6.0 è il 10 giugno 2021.
La prossima versione è prevista per il 15 luglio 2021.

### Novità {#what-is-new}

* Preview Service verrà distribuito su base continua a tutti i programmi. I clienti riceveranno una notifica interna al prodotto quando il loro programma è abilitato per Preview Service. Per ulteriori informazioni, consulta [Accesso al servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) .

* Le dipendenze Maven scaricate durante il passaggio di creazione ora verranno memorizzate nella cache tra le esecuzioni della pipeline. Questa funzione verrà attivata per i clienti nelle prossime settimane.

* È ora possibile modificare il nome del programma tramite la finestra di dialogo modifica programma.

* Il nome del ramo predefinito utilizzato sia durante la creazione del progetto che nel comando push predefinito tramite gestione flussi di lavoro Git è stato modificato in `main`.

* L’esperienza di modifica del programma nell’interfaccia utente è stata aggiornata.

* La regola di qualità `ImmutableMutableMixCheck` è stata aggiornata per classificare i nodi `/oak:index` come immutabili.

* Le regole di qualità `CQBP-84` e `CQBP-84--dependencies` sono state consolidate in un’unica regola. Come parte di questo consolidamento, la scansione delle dipendenze identifica più accuratamente i problemi nelle dipendenze di terze parti che vengono distribuiti nel runtime di AEM.

* Per evitare confusione, le righe del segmento Pubblica AEM e Pubblica dispatcher nella pagina Dettagli ambiente sono state consolidate.

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* È stata aggiunta una nuova regola di qualità del codice per convalidare la struttura degli indici `damAssetLucene`. Per ulteriori informazioni, consulta [Indici Oak di risorsa Lucene personalizzati DAM](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) .

* Nella pagina dei dettagli dell’ambiente vengono ora visualizzati più nomi di dominio per i servizi di pubblicazione e anteprima (a seconda dei casi). Per ulteriori informazioni, consulta [Dettagli ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) .

### Correzioni di bug {#bug-fixes}

* Le definizioni dei nodi JCR contenenti una nuova riga dopo che il nome dell&#39;elemento principale non è stato analizzato correttamente.

* L&#39;API degli archivi di elenchi non filtrerebbe gli archivi eliminati.

* Veniva visualizzato un messaggio di errore non corretto quando veniva fornito un valore non valido per il passaggio di pianificazione.

* A volte, l&#39;utente può visualizzare uno stato verde *attivo* accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Alcune sequenze di modifica dei programmi potrebbero impedire la creazione o la modifica della pipeline di produzione.

* Alcune sequenze di modifica del programma potrebbero causare la visualizzazione di un messaggio fuorviante della pagina **Panoramica** per la riesecuzione della configurazione del programma.
