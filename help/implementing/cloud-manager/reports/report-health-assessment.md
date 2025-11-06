---
title: Valutazione dello stato per ambienti di produzione e stage
description: Scopri come utilizzare la valutazione dello stato di Cloud Manager. Puoi scansionare gli ambienti AEM, eseguire ed esaminare i rapporti, visualizzare i dettagli dei problemi, esportare PDF e gestire le esecuzioni passate.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 9%

---


# Valutazione stato {#about-health-assessment}

La valutazione dello stato è una scansione automatizzata e non intrusiva per gli ambienti di produzione e stage in Cloud Manager all’interno di AEM as a Cloud Service. Valuta contenuti, codice e configurazioni per trovare anti-pattern e deviazioni dalle best practice, migliorando sicurezza e prestazioni.

Il servizio di valutazione dello stato esegue le seguenti operazioni:

* Esegue la scansione degli ambienti ed espone colli di bottiglia delle prestazioni, inefficienze e rischi.
* Analizza le strutture dei contenuti, come blueprint, Live Copy e configurazioni dei clienti.
* Rileva le dipendenze obsolete, incluse AEM SDK e le librerie di terze parti.
* Segnala i problemi di qualità del codice, ad esempio annotazioni errate e modelli inefficienti.
* Fornisce indicazioni actionable nelle dashboard (ad esempio, Centro operativo).
* Gestisce la correzione proattiva per migliorare le prestazioni del sistema

Ogni esecuzione elenca i problemi in base alla gravità, fornisce collegamenti alle linee guida e alle correzioni consigliate e supporta un’esportazione PDF del rapporto. Puoi utilizzare la visualizzazione **Ultimo rapporto** per lo stato corrente e **Rapporti passati** per confrontare le esecuzioni.

Vedere anche [Modelli di valutazione dell&#39;integrità](#ha-patterns) per le definizioni delle regole e i dettagli di correzione.

## Accedere alla pagina Valutazione stato {#access-health-assessment}

1. Accedi a Cloud Manager dall’indirizzo [experience.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
1. Selezionare un&#39;organizzazione desiderata. L&#39;immagine seguente è a scopo illustrativo. Seleziona il nome della tua organizzazione.

   ![Selezione di un&#39;organizzazione in Cloud Manager](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. Nella console **Programmi** fare clic sul programma per il quale si desidera visualizzare il report.

1. Effettua una delle operazioni seguenti:
   * Nella scheda **Ambienti**, a destra del nome di un ambiente, fai clic sull&#39;icona ![puntini di sospensione o sull&#39;icona Altro](https://spectrum.adobe.com/static/icons/ui_18/More.svg), quindi scegli **Valutazione integrità** dal menu.

     ![Selezione della valutazione dello stato dal menu con i puntini di sospensione nella scheda Ambienti](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * Dal menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**. Nella pagina Ambienti, a destra del nome di un ambiente, fai clic sull&#39;icona ![Puntini di sospensione o Altro](https://spectrum.adobe.com/static/icons/ui_18/More.svg), quindi scegli **Valutazione dell&#39;integrità** dal menu.

     ![Selezione della valutazione dello stato dal menu con i puntini di sospensione nella pagina Ambienti](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## Eseguire un nuovo rapporto per un ambiente selezionato {#run-report}

1. [Accedere alla pagina Valutazione stato](#access-health-assessment).
1. Nell&#39;angolo superiore destro della pagina **Valutazione integrità**, confermare l&#39;ambiente di destinazione che si sta per valutare.

   Se l&#39;ambiente non è corretto, fare clic sul menu a discesa o a discesa ![Chevron per selezionare un ambiente diverso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) per scegliere l&#39;ambiente corretto dall&#39;elenco.

1. Fai clic su **Esegui rapporto**.

   ![Fare clic sul pulsante Genera nuovo report nella pagina Valutazione stato](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   Durante l&#39;esecuzione di un report per l&#39;ambiente selezionato, **Esegui report** rimane disattivato fino al termine.

   ![Report in esecuzione](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   Al termine del report, il report verrà visualizzato nella pagina **Valutazione stato**, nella sezione **Report più recente**.

## Visualizza l’ultimo rapporto {#view-latest-report}

* Nella pagina **Valutazione integrità**, esaminare la sezione **Report più recente** per le informazioni seguenti:

   * Risultati dell’esecuzione più recente.
   * Data e ora di esecuzione.
   * Numero totale di problemi.
   * Punti salienti dei principali problemi critici.
   * Azioni: **[Visualizza dettagli](#view-report-details)** o **[Scarica PDF](#download-pdf-report)** di tutti i problemi.

  ![Pagina Valutazione più recente dopo la generazione di un nuovo report per un ambiente selezionato](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### Visualizzare i dettagli più recenti del rapporto {#view-report-details}

* Nella pagina **Valutazione stato**, a destra del titolo **Ultimo rapporto**, fai clic sull&#39;icona ![puntini di sospensione o altro](https://spectrum.adobe.com/static/icons/ui_18/More.svg), quindi fai clic su **Visualizza dettagli** o **Scarica**.

  L&#39;opzione **Visualizza dettagli** mostra quanto segue:

   * Un elenco completo dei problemi.
   * Possibilità di visualizzare i risultati e le descrizioni dei problemi.
   * Possibilità di visualizzare la documentazione con potenziali correzioni.

     ![Descrizioni problemi e risultati](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * L&#39;opzione **Scarica** consente di scaricare singoli report sui problemi in PDF.

     ![Scarica PDF dei singoli report sui problemi](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### Scarica PDF dell’intero rapporto {#download-pdf-report}

* Fai clic su **Scarica** nell&#39;angolo superiore destro della pagina del report.

  Viene generato un file ZIP contenente PDF per tutti i problemi rilevati in tale rapporto.

  ![Scarica PDF di tutti i problemi rilevati in un report](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## Rivedere i rapporti passati {#review-past-reports}

Nella pagina **Valutazione stato**, esaminare la sezione **Rapporti passati** per le informazioni seguenti:

* Visualizzare i dettagli di eventuali rapporti precedenti.
* Visualizza la data di ogni esecuzione.
* Scarica un PDF per qualsiasi rapporto.
* Ordina per data, numero di problemi o ambiente.

![Controlla i report passati](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* A destra dell&#39;intestazione **Rapporti passati**, fai clic sul menu a discesa ![freccia giù o a discesa per selezionare un ambiente diverso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) e ordinare i rapporti passati per data.
* All&#39;estrema destra di un report, fai clic sull&#39;icona ![Puntini di sospensione o Altro](https://spectrum.adobe.com/static/icons/ui_18/More.svg), quindi fai clic su **Visualizza dettagli** o **Scarica**.


## Modelli di valutazione dello stato {#ha-patterns}

Di seguito è riportato l’elenco completo degli anti-pattern e dei problemi rilevati dalla valutazione dello stato di salute in AEM as a Cloud Service. La tabella raggruppa gli elementi in tre tipi: analisi del contenuto, analisi del codice e anti-pattern di Cloud Service Optimizer, con una spiegazione per ciascuno di essi.

| Nome pattern | Categoria | Tipo | Descrizione | Impatto | Correzione automatica? |
| --- | --- | --- | --- | --- | --- |
| Gruppi AEM personalizzati con aggiunte dirette degli utenti | Protezione | Analisi dei contenuti | Gli utenti sono stati aggiunti direttamente ai gruppi di AEM invece di aggiungere gruppi IMS come membri. | La gestione delle autorizzazioni e la governance della sicurezza possono complicarsi. [Supporto IMS](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/ims-support) | No |
| Nodo di contenuto JCR mancante nelle pagine | Struttura di archivio | Analisi dei contenuti | Nodo `jcr:content` mancante nella pagina. | Limitazioni funzionali in Experience Manager as a Cloud Service. [Rilevamento pattern - ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | No |
| Tipo di risorsa Sling mancante nelle pagine | Struttura di archivio | Analisi dei contenuti | `sling:resourceType` mancante nella pagina. | Limitazioni funzionali in Experience Manager as a Cloud Service. [Rilevamento pattern - ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | No |
| Pagine con numero eccessivo di nodi | Prestazioni | Analisi dei contenuti | Le pagine contengono un numero elevato di nodi nella loro struttura. | Tempi di caricamento delle pagine lenti e scarsa esperienza utente. [Rilevamento pattern - PCX](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | No |
| Eccessive istanze di flussi di lavoro in esecuzione | Prestazioni | Analisi dei contenuti | Troppe istanze del flusso di lavoro in esecuzione. | Riduzione generale delle prestazioni del sistema. [Attività di manutenzione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/operations/maintenance) | No |
| Istanze flusso di lavoro completate non eliminate | Prestazioni | Analisi dei contenuti | Le istanze di flusso di lavoro completate precedenti non vengono eliminate. | Riduzione dell&#39;efficienza del sistema e aumento dei costi di storage. [Attività di manutenzione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/operations/maintenance) | No |
| Statistiche sull’utilizzo dei frammenti di contenuto | Statistiche | Analisi dei contenuti | Tiene traccia del numero di frammenti di contenuto in uso. | N/D | N/D |
| Statistiche sull’utilizzo del modello per frammenti di contenuto | Statistiche | Analisi dei contenuti | Tiene traccia del numero di modelli per frammenti di contenuto in uso. | N/D | N/D |
| Numero elevato di blueprint MSM | Statistiche | Analisi dei contenuti | Tiene traccia del numero di blueprint. | Può aumentare la complessità di gestione e rendere più difficile la governance dei contenuti. | N/D |
| Pagine MSM per blueprint | Statistiche | Analisi dei contenuti | Tiene traccia del numero di pagine per blueprint. | Può aumentare la complessità di gestione e rendere più difficile la governance dei contenuti. | N/D |
| Live Copy MSM eccessive | Statistiche | Analisi dei contenuti | Tiene traccia del numero di Live Copy. | Può causare problemi di prestazioni durante i rollout e complicare la sincronizzazione dei contenuti. | N/D |
| Live Copy MSM eccessive per blueprint | Statistiche | Analisi dei contenuti | Tiene traccia del numero di Live Copy per blueprint. | Può causare problemi di prestazioni durante i rollout e complicare la sincronizzazione dei contenuti. | N/D |
| Numero di Assets | Statistiche | Analisi dei contenuti | Tiene traccia del numero di risorse. | N/D | N/D |
| Numero di siti | Statistiche | Analisi dei contenuti | Tiene traccia del numero di siti. | N/D | N/D |
| Numero di Forms | Statistiche | Analisi dei contenuti | Tiene traccia del numero di moduli. | N/D | N/D |
| Frammenti di modulo | Statistiche | Analisi dei contenuti | Tiene traccia del numero di frammenti di modulo. | N/D | N/D |
| Comunicazioni di interazione | Statistiche | Analisi dei contenuti | Tiene traccia del numero di interazioni di comunicazione del modulo. | N/D | N/D |
| FDM | Statistiche | Analisi dei contenuti | Tiene traccia del numero di modelli di dati del modulo. | N/D | N/D |
| Dipendenze obsolete | Dipendenze | Analisi del codice | Evidenzia le dipendenze obsolete nell’archivio del cliente. | Incompatibilità con le versioni più recenti di AEM; potenziali vulnerabilità di sicurezza. | No |
| Versione di AEM SDK non corrispondente | Dipendenze | Analisi del codice | Versioni precedenti a (n-2) rispetto alla versione dell’ambiente Cloud Manager. | Può causare errori di build in Cloud Manager e problemi negli ambienti di sviluppo locali. | No |
| Dipendenza core Mockito obsoleta | Dipendenze | Analisi del codice | Le versioni precedenti alla versione 4.x.x sono considerate obsolete per AEM as a Cloud Service. | Può causare errori di build in Cloud Manager e problemi negli ambienti di sviluppo locali. | No |
| Annotazioni non supportate | Dipendenze | Analisi del codice | Annotazioni non supportate nell’archivio Cloud Manager del cliente. | Potenziali errori delle applicazioni e riduzione delle prestazioni. | No |
| Annotazione @Inject nei modelli Sling | Dipendenze | Analisi del codice | Annotazione `@Inject` obsoleta. | Riduzione delle prestazioni delle applicazioni a causa del sovraccarico della risoluzione di iniezione. | No |
| Richieste HTTP in uscita | Prestazioni | Anti-pattern di Cloud Service Optimizer | Utilizzo problematico nel contesto della richiesta, timeout elevati o mancata chiusura delle connessioni. | Degrado generale delle prestazioni del sistema e possibili interruzioni. | Sì |
| Query lente | Prestazioni | Anti-pattern di Cloud Service Optimizer | Query lente nel codice del cliente. | Prestazioni del sistema ridotte e timeout potenziali. | Sì |

### Categorie {#ha-patterns-categories}

| Categoria | Descrizione |
| --- | --- |
| Protezione | Modelli relativi a procedure di sicurezza, gestione degli utenti e controllo degli accessi. |
| Prestazioni | Modelli che influiscono sulle prestazioni di applicazioni e sistemi. |
| Struttura di archivio | Modelli relativi all’organizzazione e alla struttura dell’archivio JCR. |
| Dipendenze | Modelli relativi alle dipendenze del codice e alla gestione delle versioni. |
| Statistiche | Pattern che rappresentano le statistiche e le metriche di utilizzo. |



