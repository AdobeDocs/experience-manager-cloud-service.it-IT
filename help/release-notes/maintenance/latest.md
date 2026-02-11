---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e58e1355b923e1da447e3dbcfd0a81086aee3e66
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 23%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 24288 {#24288}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 24288, rilasciata pubblicamente il giovedì 4 febbraio 2026. La versione di manutenzione precedente era la 23963.

Con la versione di attivazione delle funzioni 2026.2.0 viene fornito il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

>[!NOTE]
>
>Il 24222 sulla versione è stato reso privato.

### Miglioramenti {#enhancements-24288}

* CNTBF-604: crea una nuova versione del bundle contentbackflow.
* CQ-4361592: aggiunta del supporto TypeHint per la creazione e l’aggiornamento del progetto.
* CQ-4362198: traduzioni più recenti dei pacchetti AEM e GRANITE.
* GRANITE-36205: aggiorna la versione interna di Oak all’ultima versione.
* GRANITE-59211: OPTEL: aggiunto supporto nonce e configurazione self-service.
* GRANITE-62166: aggiorna il bundle di migrazione per riutilizzare gli stati di migrazione dallo strumento di migrazione.
* GRANITE-62598: rimuovi la proprietà ridondante escludi dal filtro del pacchetto di contenuti.
* GRANITE-62684: rendi configurabile il timeout del socket client tramite skyline-ops.
* GRANITE-62702: sostituisci l’individuazione sling con l’implementazione autonoma per la migrazione online.
* GRANITE-62763: aggiorna l’elenco di eccezioni di obsolescenza di Guava in base alla funzione rotativa di ASSETS.
* GRANITE-62771: non è possibile creare le build Quickstart quando vengono introdotte nuove dipendenze Commons-Lang obsolete.
* GRANITE-62987: Aggiorna la console web Felix alla versione 5.0.18.
* GRANITE-63339: migliora il meccanismo di lease per il BLOB dello stato di migrazione di Azure.
* GRANITE-63343: aggiungi il supporto per la versione più recente del bundle API Sling in workflow.core.
* GRANITE-63799: versione Bump del bundle di autenticazione OIDC.
* GRANITE-63821: Aggiornamento da Quickstart a filevault per la correzione di JCRVLT-831/JCRVLT-839.
* GRANITE-63827: Aggiornare Quickstart all’ultima versione pubblica di Oak (1.90.0).
* GRANITE-63888: Aggiornare Quickstart a Jackrabbit 2.22.3.
* GRANITE-64030: aggiungi parole chiave e pattern all’elenco Consentiti per la convalida del linguaggio di espressione.
* GRANITE-64050: consente alle cartelle conf nascoste di nascondere la funzionalità esterna del prodotto.
* SITES-30452: API di contenuto con ASO - Suggerimenti su titolo e descrizione.
* SITES-38099: Aggiornare `testing-model.txt` per utilizzare una versione successiva dei controlli di integrità.
* SKYOPS-43616: esegui la migrazione delle credenziali Jenkins in Vault negli archivi del dispatcher.
* SKYOPS-108584: strumento Bump FACT da 0.6.0 a 0.6.10.
* SKYOPS-115691: aggiorna il bundle di filtri CORS per aggiungere l’intestazione Vary Origin alle richieste di verifica preliminare.
* SKYOPS-123094: aggiorna i componenti HTTP Apache in Quickstart.
* SKYOPS-123236: includere `rep:cugPolicy` nel pacchetto di replica.
* SKYOPS-123240: aggiorna le dipendenze CRXDE in Quickstart.
* SKYOPS-123247: aggiorna il bundle Sling XSS in Quickstart.
* SKYOPS-123250: aggiorna il bundle di sicurezza Sling in Quickstart.
* SKYOPS-123327: è necessario Java 21 per il SDK AEM-CS.
* SKYOPS-125574: aggiornare i bundle dello strumento AC netcentric in Quickstart.
* SKYOPS-126150: migliora il comando superiore per lo script del generatore di immagini thread.

### Problemi risolti {#fixed-issues-24288}

* FORMS-23687: correggi l’errore di convalida SSV quando la regola contains viene utilizzata senza valore predefinito.
* GRANITE-48472: Errore di localizzazione durante la modifica della password nella scheda Modifica impostazioni utente.
* GRANITE-50286: risolto un problema di layout nella colonna di stato della finestra modale Gestione utente.
* GRANITE-52301: Localize Impossibile eseguire il commit delle modifiche alla stringa di sessione nei gruppi di sicurezza.
* GRANITE-52920: errore di localizzazione durante la creazione dell’utente in Sicurezza Crea nuovo utente.
* GRANITE-54654: localizza una stringa nella finestra di dialogo Security Adobe IMS Configurations Check (Verifica configurazioni Adobe IMS per la sicurezza).
* GRANITE-56371: correggere il formato dati errato nell’archivio fonti attendibili per la sicurezza.
* GRANITE-62717: aggiorna il keystore di crittografia per la gestione delle password JSafe con caratteri non ASCII.
* GRANITE-62789: aggiorna messaging-client per supportare la modalità nessun nuovo tentativo nella distribuzione dei contenuti.
* GRANITE-62824: correggere `NullPointerException` quando si accede alla scheda Gruppi nell&#39;Editor utente.
* GRANITE-63080: rendere l&#39;importazione di `org.slf4j.spi` compatibile con `slf4j 2.x`.
* GRANITE-63210: aggiorna il nucleo di distribuzione per correggere l’invalidazione del dispatcher all’avvio della pubblicazione.
* GRANITE-63293: correggi il percorso obbligatorio perdendo l’asterisco richiesto dopo la prima creazione.
* GRANITE-63360: correggi le informazioni errate visualizzate quando sono selezionati più percorsi.
* SITES-36242: restringi GraphQL esegui regex per correggere il bypass del filtro del dispatcher.
* SITES-40122: Correzione dell’integrazione di Edge Delivery con ImsService per la distribuzione dei contenuti.
* SKYOPS-84379: utilizza l’ultimo strumento FACT per una corretta raccolta e/o selezione delle funzioni da parte degli RDE.
* SKYOPS-121216: ripristina l’aggiornamento alle librerie di Jackson 2.20.0.

#### AEM Guides {#guides-24288}

* GUIDES-38198 : Quando si aggiorna un’equazione in linea di MathML utilizzando l’opzione Modifica MathML dal menu di scelta rapida, il valore aggiornato viene visualizzato solo dopo l’aggiornamento della pagina.
* GUIDES-38276: impossibile rimuovere le etichette di versione dal pannello Cronologia versioni nell’interfaccia utente di Assets.
* GUIDES-36641: durante la generazione dell&#39;output di AEM Sites, i titoli delle mappe contenenti parole chiave e titoli di argomenti con l&#39;elemento `<ph>` non vengono inclusi nell&#39;output pubblicato.
* GUIDES-37837: quando si tenta di salvare un argomento o una mappa, l’operazione potrebbe non riuscire a intermittenza con un errore Impossibile salvare il file, in particolare durante attività di elaborazione intensiva delle risorse o flussi di lavoro di traduzione in esecuzione in background.
* GUIDES-27774: il report Elenco interrotto include erroneamente collegamenti esterni, `keyrefs` validi e parole chiave risolte correttamente nell&#39;ambito della mappa corrente.

>[!NOTE]
>
> In AEM Guides è stata introdotta una modifica importante di cui tenere conto: [Gestione migliorata per i file di sola lettura](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2026-releases/2601-release/whats-new-2026-01-0#improved-handling-for-read-only-files).

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta la [roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-24288}

* SITES-40408: l’endpoint GraphQL restituisce 404 a causa delle regole di riscrittura del dispatcher personalizzate.

### Funzioni e API obsolete {#deprecated-24288}

* AEMSRE-2896: correzione della gestione della configurazione di logmanager personalizzata.
* GRANITE-62802: rimuovere la dipendenza `commons-lang` obsoleta da `granite.auth.saml`.
* GRANITE-62805: rimuovere la dipendenza `commons-lang` obsoleta da `granite.httpcache.core`.
* GRANITE-62864: rimuovere la dipendenza `commons-lang` obsoleta da `granite.jobs.async`.
* GRANITE-62865: rimuovere la dipendenza `commons-lang` obsoleta da `granite.replication.core`.
* GRANITE-62868: rimuovere la dipendenza `commons-lang` obsoleta da `granite.rest.api`.
* GRANITE-62895: rimuovere la dipendenza `commons-lang` obsoleta da `translation.connector.msft.core`.
* GRANITE-63069: Obsoleto `com.adobe.granite.httpcache.core`.
* GRANITE-63179: rimuovere la dipendenza `commons-lang` obsoleta da `cq-workflow-impl`.
* GRANITE-63180: rimuovere l&#39;esportazione `commons.lang` obsoleta dal bundle `cq-mailer`.
* SKYOPS-123329: elimina il supporto Java 11 per le distribuzioni AEM Ethos e aggiorna `commons-lang3`.
* SKYOPS-124983: rimuovere `nashorn.args` obsoleto dagli script di avvio di AEM.

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-24288}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 10 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-24288}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,90,0 | [API Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.2. | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
