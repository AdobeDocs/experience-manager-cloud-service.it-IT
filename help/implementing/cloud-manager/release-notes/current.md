---
title: Note sulla versione 2024.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Scopri le note sulla versione 2024.10.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: b90ace2250277005d8ac250c841104c93298a605
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 15%

---

# Note sulla versione 2024.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2024.10.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager versione 2024.10.0 in AEM as a Cloud Service è il 3 ottobre 2024.

La prossima versione è prevista per il venerdì 14 novembre 2024.

## Novità {#what-is-new}

* <!-- BOTH CS & AMS --> La versione dell’Archetipo AEM utilizzato in Cloud Manager è ora aggiornata alla versione 26. Vedi [https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> Quando aggiungi o modifichi un’infrastruttura di rete, i valori nei campi Indirizzo IP e Maschera di rete vengono convalidati in base alle regole seguenti:

   * Lo spazio degli indirizzi non deve sovrapporsi agli indirizzi definiti nello spazio degli indirizzi di connessione.
   * Gli indirizzi DNS devono appartenere alla maschera di rete definita nello spazio degli indirizzi di connessione o essere pubblici.

  ![Finestra di dialogo Aggiungi infrastruttura di rete](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> Sono state apportate modifiche al formato dei registri di distribuzione dell’ambiente per l’indicizzazione, l’installazione di contenuto mutabile e i processi di trasformazione.

  >[!NOTE]
  >
  >Questa modifica è pianificata per l’implementazione in modo graduale con una data di completamento prevista a dicembre 2024.

  ![Distribuisci sulla scheda di produzione](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  Il formato del registro cambierà da una semplice voce visualizzata nei seguenti elementi:

  ![Il file di registro mostra voci semplici](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  A una voce JSON visualizzata nei seguenti elementi:

  ![File di registro con voci JSON](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma di adozione anticipata di Cloud Manager e prova le prossime funzionalità.

### Porta il tuo Git - ora con supporto per GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La funzionalità **Porta il tuo Git** è stata espansa per includere il supporto per archivi esterni come GitLab e Bitbucket. Questo nuovo supporto si aggiunge a quello già esistente per gli archivi GitHub privati ed aziendali. Quando aggiungi questi nuovi repository, puoi anche collegarli direttamente alle pipeline. Puoi ospitare questi archivi su piattaforme cloud pubbliche o all’interno del cloud o dell’infrastruttura privata. Questa integrazione elimina anche la necessità di una sincronizzazione costante del codice con l’archivio Adobe e consente di convalidare le richieste pull prima di unirle in un ramo principale.

Vedi [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Attualmente, i controlli predefiniti per la qualità del codice di richiesta di pull sono esclusivi per gli archivi ospitati da GitHub, ma è in corso un aggiornamento per estendere questa funzionalità ad altri fornitori Git.

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID. Assicurati di includere la piattaforma Git da utilizzare e se ti trovi in una struttura di archivio privata/pubblica o aziendale.


<!-- ## Bug fixes




## Known Issues {#known-issues} -->
