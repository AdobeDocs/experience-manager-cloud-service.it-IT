---
title: Note sulla versione 2025.4.0 di Cloud Manager
description: Ulteriori informazioni sulla versione 2025.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 0712ba8918696f4300089be24cad3e4125416c02
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 100%

---

# Note sulla versione 2025.4.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Ulteriori informazioni sulla versione 2025.4.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.


Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.4.0 di Cloud Manager in AEM as a Cloud Service è il 10 aprile 2025.

La prossima versione è pianificata per l’8 maggio 2025.

## Novità {#what-is-new}

* **(Interfaccia utente) Visibilità della distribuzione migliorata**

  Nella pagina dei dettagli sull’esecuzione della pipeline in Cloud Manager quando una distribuzione è in attesa del completamento di un’altra distribuzione, ora viene visualizzato un messaggio di stato (“*In attesa: altro aggiornamento in corso*”). Questo flusso di lavoro semplifica la comprensione del sequenziamento durante la distribuzione dell’ambiente.  <!-- CMGR-66890 -->

  ![Finestra di dialogo Distribuzione dello sviluppo che mostra dettagli e raggruppamento](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **(Interfaccia utente) Miglioramento della convalida del dominio**

  Durante l’aggiunta di un dominio, se questo è già installato in un account Fastly, Cloud Manager mostra ora un errore: “*Il dominio è già installato in un account Fastly. Rimuovilo prima di aggiungerlo a Cloud Service.*”

## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma per i primi utilizzatori di Cloud Manager per ottenere un accesso esclusivo alle prossime funzioni prima del rilascio generale.

Le seguenti opportunità sono attualmente disponibili per i primi utilizzatori:

### Bring Your Own Git: ora con supporto per GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La funzione **Bring Your Own Git** è stata estesa in modo da includere il supporto per archivi esterni come GitLab e Bitbucket. Questo nuovo supporto si aggiunge a quello già esistente per archivi GitHub privati ed aziendali. Quando aggiungi questi nuovi archivi, puoi anche collegarli direttamente alle pipeline. Puoi inoltre ospitare questi archivi sia su piattaforme cloud pubbliche sia all’interno della tua infrastruttura o del tuo cloud privato. Questa integrazione elimina anche la necessità di sincronizzare continuamente il codice con l’archivio Adobe e offre la possibilità di convalidare le richieste pull prima di unirle in un ramo principale.

Le pipeline che utilizzano archivi esterni (esclusi quelli ospitati da GitHub) e il **Trigger di implementazione** impostato su **Cambiamenti su Git** ora vengono avviate automaticamente.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Attualmente, i controlli di qualità predefiniti per il codice di richiesta pull sono esclusivi degli archivi ospitati in GitHub, ma è in preparazione un aggiornamento per estendere questa funzionalità anche ad altri fornitori Git.

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Se ti trovi in una struttura di archivio privata/pubblica o aziendale, assicurati di specificare la piattaforma Git che desideri utilizzare.

### Pagina Home di AEM {#aem-home}

La pagina Home di AEM rappresenta un punto di partenza centralizzato per la gestione di contenuti, risorse e siti in Adobe Experience Manager. Progettata per offrire un’esperienza personalizzata, la pagina Home di AEM consente di navigare nell’ecosistema di AEM in modo semplice in base ai ruoli e agli obiettivi. Funge da guida e fornisce informazioni chiave e azioni consigliate per aiutare a raggiungere gli obiettivi in modo efficiente. Con un layout chiaro e personalizzato, la pagina Home di AEM assicura un accesso rapido a strumenti essenziali, supportando un’esperienza semplificata ed efficace in tutte le funzioni di AEM.

Disponibile per i primi utilizzatori, la pagina Home di AEM offre un’esperienza ottimizzata incentrata sul miglioramento dei flussi di lavoro, sulla definizione delle priorità degli obiettivi e sulla distribuzione dei risultati. Consentendone l’utilizzo permette di influenzare lo sviluppo della pagina Home di AEM fornendo un feedback che aiuta a modellarne il futuro e ne aumenta il valore per l’intera comunità di AEM.

Se ti interessa testare questa nuova funzionalità e condividere il tuo feedback, invia un’e-mail a [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Accertati di includere le seguenti informazioni:

* Il ruolo più adatto al tuo profilo: autore del contenuto, sviluppatore, Proprietario business, amministratore o altro (fornisci una descrizione).
* Superficie di accesso AEM principale: AEM Sites, AEM Assets, AEM Forms, Cloud Manager o altro (fornisci una descrizione).

## Correzioni di bug

* **Problema relativo ai certificati in cui manca il campo Nome comune (NC)**

  Cloud Manager non genera più una risposta NullPointerException (NPE) e HTTP 500 durante l’elaborazione di certificati OV/EV che non includono un Nome comune (NC) nel campo Oggetto. I certificati moderni spesso omettono NC e utilizzano invece Nome alternativo soggetto (NAS). Questa correzione assicura che l’assenza del NC non causi più un errore durante il processo di creazione della configurazione quando è presente il NAS. <!-- CMGR-67548 -->

* **Problema di verifica del dominio relativo alla corrispondenza del certificato errata**

  Cloud Manager non verifica più in modo non corretto i domini utilizzando certificati errati. In precedenza, la logica di convalida utilizzava la corrispondenza basata su pattern invece della corrispondenza esatta, causando la visualizzazione di domini, ad esempio `should-not-be-verified.example.com`, come verificati a seguito della sovrapposizione con certificati validi per `example.com`. Questa correzione assicura che la convalida del dominio ora verifichi la corrispondenze esatta, evitando associazioni di certificati errate. <!-- CMGR-67225 -->

* **Univocità applicata ai nomi di inoltro delle porte di rete avanzata**

  Cloud Manager ora applica una denominazione univoca per gli inoltri delle porte di rete avanzate. In precedenza, erano consentiti nomi duplicati, che potevano causare conflitti. Questa correzione assicura che ogni voce di inoltro delle porte abbia un nome distinto, in linea con le best practice per l’integrità della configurazione di rete. <!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

