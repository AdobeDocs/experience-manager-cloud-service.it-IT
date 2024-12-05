---
title: Note sulla versione 2024.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2024.12.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: ea1aa471a4fcb2ace6e4079715ac88af2d296e18
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 37%

---

# Note sulla versione 2024.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Ulteriori informazioni sulla versione 2024.12.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di rilascio per Cloud Manager 2024.12.0 in AEM as a Cloud Service è giovedì 5 dicembre 2024.

La prossima versione pianificata è gennaio 2024.

## Novità {#what-is-new}

* Supporto di **Java 21:** I clienti possono ora scegliere di creare con Java 17 o Java 21, beneficiando di miglioramenti delle prestazioni e di nuove funzioni del linguaggio. Consulta [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) per i passaggi di configurazione, incluso l&#39;aggiornamento della descrizione del progetto Maven e di alcune versioni della libreria. Quando la versione della build è impostata su Java 17 o Java 21, il runtime utilizza per impostazione predefinita Java 21.

  A partire da febbraio 2025, le sandbox e gli ambienti di sviluppo vengono aggiornati al runtime Java 21, indipendentemente dalla versione di build (Java 8, 11, 17 o 21). Gli ambienti di produzione verranno aggiornati ad aprile 2025.

* **Tipi di record:** è stato aggiunto il supporto per i tipi di record A per migliorare la preparazione Go Live per i domini che utilizzano le configurazioni CDN in AEM Cloud Manager. Ora puoi andare &quot;live&quot; aggiungendo un tipo di record CNAME o un tipo di record A che rappresenta gli IP di Fastly, semplificando il routing del dominio. Questo miglioramento elimina la restrizione di affidarsi esclusivamente ai record CNAME per la configurazione del dominio con Fastly.

  Vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). <!-- CMGR-63076 -->

* **Aggiungere più domini a un sito Edge Delivery:** È ora possibile aggiungere più domini, inclusi i domini APEX e non APEX, a un sito Edge Delivery (EDS) in AEM Cloud Manager. Questo miglioramento risolve le limitazioni precedenti che limitavano la possibilità di associare più domini a un’origine EDS. L’aggiornamento garantisce una maggiore flessibilità per la gestione delle configurazioni dei domini e semplifica i processi di pubblicazione per i siti con configurazioni di dominio complesse. <!-- CMGR-63007 -->

* **Opzioni di filtro avanzate:** Sono state introdotte opzioni di filtro avanzate nelle pagine di esecuzione della pipeline e nelle pagine del certificato SSL in AEM Cloud Manager. Ora è possibile filtrare in base a più criteri, consentendo un accesso più rapido ai dati rilevanti e migliorando l’efficienza della distribuzione. <!-- CMGR-26263 -->

   * **Filtro attività pipeline:** include il filtro attività pipeline, che consente di perfezionare i risultati della ricerca per attività pipeline specifiche. I filtri disponibili includono pipeline, azione e stato.
     ![Filtro attività pipeline](/help/implementing/cloud-manager/assets/filters-pipeline.png)


   * **Filtro dei certificati SSL:** include il filtro dei certificati SSL, che consente di perfezionare i risultati della ricerca per certificati specifici. I filtri disponibili includono il nome del certificato SSL, la proprietà e lo stato.
     ![Filtro certificato SSL](/help/implementing/cloud-manager/assets/filters-ssl-certificates.png)

## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma per i primi utilizzatori di Cloud Manger e concediti la possibilità di testare le prossime funzionalità.

### Bring Your Own Git: ora con supporto per GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La funzionalità **Porta il tuo Git** è stata espansa per includere il supporto per archivi esterni, come GitLab e Bitbucket. Questo nuovo supporto si aggiunge a quello già esistente per archivi GitHub privati ed aziendali. Quando aggiungi questi nuovi archivi, puoi anche collegarli direttamente alle pipeline. Puoi inoltre ospitare questi archivi sia su piattaforme cloud pubbliche sia all’interno della tua infrastruttura o del tuo cloud privato. Questa integrazione elimina anche la necessità di sincronizzare continuamente il codice con l’archivio Adobe e offre la possibilità di convalidare le richieste pull prima di unirle in un ramo principale.

Le pipeline che utilizzano archivi esterni (esclusi quelli ospitati da GitHub) e il **Trigger di distribuzione** impostato su **Su modifiche Git** ora vengono avviate automaticamente.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Attualmente, i controlli di qualità predefiniti per il codice di richiesta pull sono esclusivi degli archivi ospitati in GitHub, ma è in preparazione un aggiornamento per estendere questa funzionalità anche ad altri fornitori Git.

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Se ti trovi in una struttura di archivio privata/pubblica o aziendale, assicurati di specificare la piattaforma Git che desideri utilizzare.

## Correzioni di bug

* È stata aggiunta una protezione per impedire l’eliminazione di domini con mappature di dominio attive in AEM Cloud Manager. Gli utenti che tentano di eliminare tali domini ricevono ora un messaggio di errore in cui viene richiesto di eliminare prima la mappatura del dominio prima di procedere con l’eliminazione. Questo flusso di lavoro garantisce l’integrità del dominio ed evita errori di configurazione accidentali. <!-- CMGR-63033 -->
* Di rado, gli utenti non potevano aggiungere un nome di dominio o aggiornare un certificato SSL a causa di uno stato non corretto associato nei rispettivi casi. <!-- CMGR-62816 -->


<!-- ## Known issues {#known-issues} -->