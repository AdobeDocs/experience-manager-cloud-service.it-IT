---
title: Note sulla versione 2025.7.0 di Cloud Manager
description: Scopri la versione 2025.7.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 3e7ce0c7f330ba92b57e36ea8fe5bb17b5998cb1
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 99%

---

# Note sulla versione 2025.7.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Scopri la versione 2025.7.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La versione 2025.7.0 di Cloud Manager in AEM as a Cloud Service è stata rilasciata il 10 luglio 2025.

La prossima versione è pianificata per il 7 agosto 2025.

## Novità {#what-is-new}

* **In Cloud Manager è stato aggiunto il supporto per i certificati SSL con ECDSA (Elliptic Curve Digital Signature Algorithm)**

  Cloud Manager ora supporta i certificati ECDSA. Questa funzione garantisce un livello di sicurezza elevato con chiavi di dimensioni più piccole e consente di applicare una crittografia moderna e leggera alle configurazioni CDN. <!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **Scarica il report sull’utilizzo della licenza del sito**

  Nella pagina **Dettagli sull’utilizzo di Sites** (in Cloud Manager, fai clic su **Licenza**. nella tabella Soluzioni, nella riga **Sites**, fai clic su **Visualizza dettagli sull’utilizzo**), la clientela può ora fare clic su **Scarica report** per esportare i dati come file CSV. Questo scaricamento semplifica l’analisi e la condivisione delle tendenze di utilizzo. <!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![Dettagli sull’utilizzo di Sites](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

  Consulta [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

## Programma per primi utilizzatori {#private-beta-program}

Partecipa ai programmi Beta e Alpha di Cloud Manager per ottenere un accesso esclusivo alle prossime funzioni prima della versione generale.

Sono attualmente disponibili le seguenti opportunità:

### Rollback con un solo clic per le implementazioni di pipeline {#one-click-rollback}

Ripristino rapido a un’implementazione precedente se il codice di origine più recente del cliente non funziona come previsto: non è necessario eseguire nuovamente la pipeline completa o ripristinare manualmente i commit.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Ripristina il codice di origine del cliente dalla scheda Ambienti](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *Nella scheda Ambienti precedente è visualizzata l’opzione **Ripristina**>**Codice precedente implementato**&#x200B;per un ambiente selezionato.*


![Finestra di dialogo Ripristina codice precedente implementato](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*Nella finestra di dialogo **Ripristina codice precedente implementato**, controlla la versione attualmente implementata e quella che desideri ripristinare, quindi fai clic su **Conferma***.


![Ripristino dell’attivazione](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager ripristina l’ambiente alla versione precedente, mantiene intatti il contenuto e la configurazione e contrassegna l’ambiente **Ripristino**&#x200B;fino al completamento dell’implementazione.*


![Versione del codice di origine in uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *La visualizzazione dei dettagli dell’ambiente, come illustrato in precedenza, mostra ora anche la versione del codice di origine attiva in uso.*

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [restorecode@adobe.com](mailto:restorecode@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.

Vedi [Ripristinare il codice precedente distribuito in AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulta anche [Ripristino dei contenuti in AEM as a Cloud Service](/help/operations/restore.md).


### Ambiente di test specializzato {#specialized-test-environment}

Cloud Manager ora supporta l’aggiunta di un nuovo tipo di ambiente denominato **Ambiente di test specializzato**. L’ambiente è progettato per aiutare i team a convalidare le funzioni in condizioni prossime alla produzione prima della pubblicazione. Questo tipo di ambiente è diverso dagli ambienti *Produzione + Fase*, *Sviluppo* o *Sviluppo rapido* e offre uno spazio mirato per l’esecuzione di scenari di convalida avanzati.

Miglioramento recente: ora puoi configurare ambienti di test specializzati su una pipeline non di produzione tramite un flusso di lavoro più semplice e intuitivo. La configurazione semplificata accelera il completamento e riduce gli errori di configurazione.

Consulta [Aggiungere un ambiente di test specializzato](/help/implementing/cloud-manager/specialized-test-environment.md).

![Finestra di dialogo Aggiungi ambiente con il pulsante di scelta Ambiente di test specializzato selezionato](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.


### BYOG (Bring Your Own Git): ora con supporto per Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Ora è possibile portare in Cloud Manager i propri archivi Git Azure DevOps, con supporto per i nuovi archivi Azure DevOps e gli archivi legacy VSTS (Visual Studio Team Services).

* Per chi usa Edge Delivery Services, l’archivio di cui è stato eseguito l’onboarding può essere utilizzato per sincronizzare e distribuire il codice del sito.
* Per chi usa AEM as a Cloud Service e Adobe Managed Services (AMS), l’archivio può essere collegato sia a pipeline full stack che front-end.

Verranno presto introdotti anche il supporto di ulteriori tipi di pipeline e la convalida di richieste pull tramite pipeline per la qualità del codice.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Se ti trovi in una struttura di archivio privata/pubblica o aziendale, assicurati di specificare la piattaforma Git che desideri utilizzare.


**Domande frequenti su BYOG**

| Domanda | Risposta |
|---|---|
| *Come può un progetto tornare all’archivio Git gestito da Adobe, se necessario?* | Tornare indietro è semplice. [Aggiorna le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) in modo che puntino all’archivio Adobe e rimuovi l’archivio esterno se non è più necessario. |
| *È possibile configurare archivi diversi per ambienti diversi (ad esempio, non di produzione o di produzione) per consentire prima il test in ambienti non di produzione?* | Sì, è possibile configurare archivi diversi per ambienti separati. Ad esempio, la pipeline di sviluppo o di qualità del codice può puntare a un archivio esterno mentre la pipeline di produzione rimane connessa all’archivio Adobe. Assicurati che il processo di sincronizzazione tra i due archivi rimanga attivo durante questa configurazione. |
| *Le impostazioni esistenti come gli elenchi IP consentiti continuano a funzionare?* | Sì, gli elenchi IP consentiti esistenti continuano a funzionare come al solito. Tuttavia, se l’archivio Git esterno è protetto da un firewall, gli [Indirizzi IP Adobe necessari devono essere aggiunti all’elenco consentiti](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Funzionano tutti gli URL dell’archivio GitLab? L’URL dell’archivio in uso segue il formato `https://gitlab_dedicated_url.com/path/repo-name.git`, che differisce dall’esempio riportato nella documentazione.* | Sì, è supportato qualsiasi archivio GitLab che supporta API V3 o V4, inclusi gli URL GitLab con hosting autonomo come quelli descritto in [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gestisci token di accesso{#manage-access-tokens}

Utilizza **Gestisci token di accesso** in Cloud Manager per visualizzare, rinominare ed eliminare i token di accesso associati agli archivi BYOG esterni, ad esempio GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulta [Gestisci token di accesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.


### Aggiungere una pipeline di configurazione Edge Delivery {#add-eds-pipeline}

Le pipeline di configurazione sono ora supportate per i siti creati con Edge Delivery Services, espandendo questa funzionalità oltre i singoli ambienti di Cloud Service. È possibile utilizzare le **pipeline di configurazione** per gestire impostazioni quali le regole di filtro del traffico e le configurazioni del firewall per applicazioni web (WAF), se applicabile. Consulta le [configurazioni supportate](/help/operations/config-pipeline.md#configurations).

![Aggiungi pipeline Edge Delivery nell’elenco a discesa Aggiungi pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Aggiunta di una pipeline Edge Delivery dalla pagina **Panoramica del programma**, scheda **Pipeline**.*

![Finestra di dialogo Aggiungi pipeline di Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Finestra di dialogo Aggiungi pipeline di Edge Delivery.*

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.


## Correzioni di bug

* Cloud Manager ora aggiorna la versione di tutte le pipeline durante gli aggiornamenti dell’ambiente, garantendo un tracciamento coerente delle versioni per tutti i tipi di pipeline. <!-- CMGR-69043 -->
* Ora l’interfaccia utente visualizza messaggi di stato e messaggi di errore dettagliati quando un certificato SSL di convalida del dominio (DV) non riesce, utili per comprendere e risolvere i problemi relativi ai certificati. <!-- CMGR-68872 -->
* Durante la modifica di una mappatura di dominio, l’interfaccia utente ora impedisce la selezione di certificati SSL che non corrispondono al dominio scelto, riducendo gli errori di configurazione e migliorando l’affidabilità durante la configurazione. <!-- CMGR-64307 -->
* In alcune situazioni, i certificati non venivano eliminati correttamente, mantenendo il dominio ancora attivo. <!-- CMGR-69867 -->
* È stato risolto un problema che in alcuni casi poteva bloccare gli aggiornamenti da *Adobe Assets* a *Adobe Assets Ultimate*. Le transizioni sono ora più fluide e affidabili. <!-- CMGR-69506 -->
* È stato risolto un problema che causava l’impostazione automatica dei campi delle aree chiave durante la creazione di ambienti con più aree geografiche, al fine di supportare servizi e implementazioni a valle fluidamente. <!-- CMGR-69471 -->
* È stato risolto un problema che impediva la corretta interruzione di alcune pipeline di configurazione dopo l’esecuzione. Ora le pipeline vengono completate correttamente e chiuse come previsto, migliorando l’affidabilità. <!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->

