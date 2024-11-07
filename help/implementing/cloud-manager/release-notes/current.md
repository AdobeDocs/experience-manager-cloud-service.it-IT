---
title: Note sulla versione 2024.11.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Scopri la versione di Cloud Manager 2024.11.0 in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 87293526ca9c10a142bc1d1d3a35562b171da385
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 30%

---

# Note sulla versione 2024.11.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Scopri la versione 2024.11.0 di Cloud Manager nell’as a Cloud Service AEM (Adobe Experience Manager).

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di rilascio {#release-date}

La data di pubblicazione di Cloud Manager 2024.11.0 in AEM as a Cloud Service è il 7 novembre 2024.

La prossima versione pianificata è il 5 dicembre 2024.

## Novità {#what-is-new}

* Scopri le ultime innovazioni nei Edge Delivery Services con AEM Cloud Service, ora disponibile per l’esplorazione nel tuo programma Sandbox. [Ulteriori informazioni](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* La pagina Impostazioni dominio in AEM Cloud Manager ora include una funzione di ricerca che consente di individuare rapidamente i domini per nome. Puoi immettere parole chiave nel campo di ricerca per filtrare e visualizzare i domini corrispondenti, semplificando così la gestione efficiente di più domini. Inoltre, la pagina offre filtri di stato, ad esempio **Verificato** e **Non verificato**, per perfezionare ulteriormente i risultati della ricerca. <!-- (CMGR-62615) -->

![Campo di ricerca nelle impostazioni del dominio](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma per i primi utilizzatori di Cloud Manger e concediti la possibilità di testare le prossime funzionalità.

### Home page AEM {#aem-home}

La Home di AEM introduce un punto di partenza centralizzato per la gestione di contenuti, risorse e siti in Adobe Experience Manager. Progettata per offrire un’esperienza personalizzata, la Home dell’AEM ti consente di navigare nell’ecosistema dell’AEM senza problemi in base ai tuoi ruoli e obiettivi. Funge da guida e fornisce informazioni chiave e azioni consigliate per aiutarti a raggiungere gli obiettivi in modo efficiente. Con un layout chiaro e personalizzato, la Home dell’AEM assicura un accesso rapido a strumenti essenziali, supportando un’esperienza semplificata ed efficace in tutte le funzioni dell’AEM.

Disponibile per i primi utenti, AEM Home offre un’esperienza ottimizzata incentrata sul miglioramento dei flussi di lavoro, sulla definizione delle priorità degli obiettivi e sulla distribuzione dei risultati. Opt in consente di influenzare lo sviluppo della Home dell&#39;AEM fornendo un feedback che aiuta a modellarne il futuro e ne aumenta il valore per l&#39;intera comunità dell&#39;AEM.

Se ti interessa testare questa nuova funzionalità e condividere i tuoi commenti, invia un&#39;e-mail a [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID. Accertati di includere le seguenti informazioni:

* Il ruolo più adatto al tuo profilo: Autore di contenuti, Sviluppatore, Proprietario business, Amministratore o Altro (fornisci una descrizione).
* Superficie di accesso AEM principale: AEM Sites, AEM Assets, AEM Forms, Cloud Manager o altro (fornisci una descrizione).

### Bring Your Own Git: ora con supporto per GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La funzionalità **Bring Your Own Git** è stata estesa in modo da includere il supporto per archivi esterni come GitLab e Bitbucket. Questo nuovo supporto si aggiunge a quello già esistente per archivi GitHub privati ed aziendali. Quando aggiungi questi nuovi archivi, puoi anche collegarli direttamente alle pipeline. Puoi inoltre ospitare questi archivi sia su piattaforme cloud pubbliche sia all’interno della tua infrastruttura o del tuo cloud privato. Questa integrazione elimina anche la necessità di sincronizzare continuamente il codice con l’archivio Adobe e offre la possibilità di convalidare le richieste pull prima di unirle in un ramo principale.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Attualmente, i controlli di qualità predefiniti per il codice di richiesta pull sono esclusivi degli archivi ospitati in GitHub, ma è in preparazione un aggiornamento per estendere questa funzionalità anche ad altri fornitori Git.

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Assicurati di includere la piattaforma Git da utilizzare e se ti trovi in una struttura di archivio privata/pubblica o aziendale. —>


## Correzioni di bug

* Un aggiornamento recente ha risolto un problema in SonarQube a causa del quale in alcuni casi non venivano rilevate password hardcoded. La correzione ora include un controllo pattern espanso e si allinea agli standard di rilevamento predefiniti in SonarQube. <!-- CMGR-62682 -->
* Quando si tenta di aggiornare un certificato SSL in Cloud Manager, viene visualizzato un errore sconosciuto dopo aver fatto clic su **[!UICONTROL Aggiorna]** nella finestra di dialogo **[!UICONTROL Visualizza e aggiorna certificato SSL]**. <!-- CMGR-62848 -->
* In Cloud Manager, gli aggiornamenti del certificato SSL non riuscivano e veniva visualizzato l’errore &quot;Il nuovo certificato non corrisponde ai domini esistenti&quot;, anche quando i domini erano identici ma presentavano differenze in lettere maiuscole o minuscole. L&#39;aggiornamento ora riconosce i domini senza distinzione tra maiuscole e minuscole, allineandoli agli standard RFC. <!-- CMGR-62844 -->
* In Cloud Manager, le associazioni dei Elenchi Consentiti di indirizzi IP sono rimaste bloccate in uno stato di esecuzione perché mancavano collegamenti chiave esterni alle configurazioni del dominio. La correzione ora garantisce che i binding del Inserisco nell&#39;elenco Consentiti di IP siano collegati correttamente alle configurazioni di dominio associate. <!-- CMGR-62838 -->
* Cloud Manager convalida lo stato OCSP (Online Certificate Status Protocol) di un certificato SSL. Adobe consiglia inoltre di convalidare l&#39;integrità del certificato localmente utilizzando uno strumento come `openssl verify -untrusted intermediate.pem certificate.pem` prima di installarlo tramite Cloud Manager. Per ulteriori dettagli, consulta la [documentazione sui requisiti del certificato SSL](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements). <!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->