---
title: Note sulla versione 2024.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2024.12.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8e89adcaadbc53c3d525d57ef452f671137a619f
workflow-type: ht
source-wordcount: '645'
ht-degree: 100%

---

# Note sulla versione 2024.12.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Ulteriori informazioni sulla versione 2024.12.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2024.12.0 di Cloud Manager in AEM as a Cloud Service è il 5 dicembre 2024.

La prossima versione è pianificata per il 23 gennaio 2025.


## Novità {#what-is-new}

<!-- * **Java 21 support:** Customers can now optionally build with Java 17 or Java 21, benefiting from performance improvements and new language features. See [Build environment](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) for configuration steps, including updating your Maven project description, and certain library versions. When the build version is set to Java 17 or Java 21, the runtime defaults to Java 21.

    Starting February 2025, sandboxes and dev environments upgrade to the Java 21 runtime, regardless of the build version (Java 8, 11, 17, or 21). Production environments follow with an upgrade in April 2025. -->

* **Tipi di record A:** è stato aggiunto il supporto per i tipi di record A per migliorare la preparazione al Go-Live per i domini che utilizzano le configurazioni CDN in AEM Cloud Manager. Ora è disponibile l’opzione Go-live aggiungendo un tipo di record CNAME o un tipo di record A che rappresenta gli IP di Fastly, semplificando il routing del dominio. Questo miglioramento elimina la restrizione di affidarsi esclusivamente ai record CNAME per la configurazione del dominio con Fastly.

  Consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). <!-- CMGR-63076 -->

<!-- * The AEM Code Quality step now uses SonarQube 9.9 Server, replacing the older 7.4 version. This upgrade brings additional security, performance, and code quality checks, offering more comprehensive analysis and coverage for your projects. -->

* **Aggiungere più domini a un sito Edge Delivery:** ora è possibile aggiungere più domini, inclusi i domini APEX e non APEX, a un sito di Edge Delivery (EDS) in AEM Cloud Manager. Questo miglioramento risolve le restrizioni precedenti che limitavano la possibilità di associare più domini a un’origine EDS. L’aggiornamento garantisce una maggiore flessibilità per la gestione delle configurazioni dei domini e semplifica i processi Go-live per i siti con configurazioni di dominio complesse. <!-- CMGR-63007 -->

* **Opzioni di filtro avanzate:** sono state introdotte opzioni di filtro avanzate nelle pagine di esecuzione della pipeline e nelle pagine del certificato SSL in AEM Cloud Manager. Ora è possibile filtrare in base a più criteri, consentendo un accesso più rapido ai dati rilevanti e migliorando l’efficienza della distribuzione. <!-- CMGR-26263 -->

   * **Filtro attività pipeline:** include il filtro attività della pipeline, che consente di perfezionare i risultati della ricerca per attività pipeline specifiche. I filtri disponibili includono pipeline, azione e stato.
     ![Filtro attività pipeline](/help/implementing/cloud-manager/assets/filters-pipeline.png)


   * **Filtro dei certificati SSL:** include il filtro dei certificati SSL, che consente di perfezionare i risultati di ricerca per certificati specifici. I filtri disponibili includono il nome del certificato SSL, la proprietà e lo stato.
     ![Filtro certificato SSL](/help/implementing/cloud-manager/assets/filters-ssl-certificates.png)

## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma per i primi utilizzatori di Cloud Manger e concediti la possibilità di testare le prossime funzionalità.

### Bring Your Own Git: ora con supporto per GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La funzione **Bring Your Own Git** è stata estesa in modo da includere il supporto per archivi esterni come GitLab e Bitbucket. Questo nuovo supporto si aggiunge a quello già esistente per archivi GitHub privati ed aziendali. Quando aggiungi questi nuovi archivi, puoi anche collegarli direttamente alle pipeline. Puoi inoltre ospitare questi archivi sia su piattaforme cloud pubbliche sia all’interno della tua infrastruttura o del tuo cloud privato. Questa integrazione elimina anche la necessità di sincronizzare continuamente il codice con l’archivio Adobe e offre la possibilità di convalidare le richieste pull prima di unirle in un ramo principale.

Le pipeline che utilizzano archivi esterni (esclusi quelli ospitati da GitHub) e il **Trigger di implementazione** impostato su **Cambiamenti su Git** ora vengono avviate automaticamente.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Attualmente, i controlli di qualità predefiniti per il codice di richiesta pull sono esclusivi degli archivi ospitati in GitHub, ma è in preparazione un aggiornamento per estendere questa funzionalità anche ad altri fornitori Git.

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Se ti trovi in una struttura di archivio privata/pubblica o aziendale, assicurati di specificare la piattaforma Git che desideri utilizzare.

## Correzioni di bug

* È stata aggiunta una protezione per impedire l’eliminazione di domini con mappature di dominio attive in AEM Cloud Manager. Gli utenti che tentano di eliminare tali domini ricevono ora un messaggio di errore in cui viene richiesto di eliminare inizialmente la mappatura prima di procedere con l’eliminazione del dominio. Questo flusso di lavoro garantisce l’integrità del dominio ed evita errori di configurazione accidentali. <!-- CMGR-63033 -->
* Di rado, gli utenti non potevano aggiungere un nome di dominio o aggiornare un certificato SSL a causa di uno stato non corretto associato nei rispettivi casi. <!-- CMGR-62816 -->


<!-- ## Known issues {#known-issues} -->
