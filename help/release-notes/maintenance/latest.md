---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c1e175128ab6e4b483e3940d9bd86a06540ef40f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 27%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 24464 {#release-24464}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 24464, rilasciata pubblicamente il giovedì 18 febbraio 2026. La versione di manutenzione precedente era la 24288.

Con la versione di attivazione delle funzioni 2026.2.0 viene fornito il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-24464}

* AEMARCH-264: aggiunta del supporto per la convalida delle richieste condizionali basate su RequestEntity.
* AEMARCH-269: Esporre le API di convalida JavaEE per le implementazioni OpenAPI.
* AEMARCH-276: fornisce supporto per i18n tramite RequestEntity.
* ASSETS-10995: imposta il limite sul numero di risorse nello zip di download.
* ASSETS-50788: aggiorna l’API di ricerca per utilizzare l’API GET dei metadati delle risorse.
* ASSETS-50946: mappa il corpo della richiesta utilizzando l’API GET dei metadati con i metadati JCR.
* ASSETS-55866: evita di inviare una nuova richiesta per la stessa risorsa fino al completamento dell’elaborazione precedente.
* ASSETS-60300: fornisci API per recuperare contesto e risultato del processo asincrono.
* ASSETS-60574: è stato aggiunto il supporto per l’ultima versione del bundle Sling API.
* ASSETS-61049: continua lo sviluppo del bundle di gestione metadati.
* ASSETS-61692: esegui una ricerca semantica per impostazione predefinita nell’API Search Open.
* ASSETS-61696: route BAM e wrapper MFE nella visualizzazione delle risorse.
* ASSETS-61854: invia la soluzione GenStudio nel messaggio di attivazione/disattivazione.
* ASSETS-61973: crea un’API in AEM per la gestione dei prompt.
* ASSETS-62182: gestore eventi Asset Compute per la rappresentazione del manifesto c2pa.
* ASSETS-62311: cerca problemi di regressione.
* ASSETS-62413: aggiungi il supporto per il campo customModifier in ogni livello in JSON.
* ASSETS-62432: MERGE FOLDER delete API PR (Elimina API PR della cartella di unione).
* ASSETS-62540: aumenta la versione ui-touch ottimizzata in quickstart.
* ASSETS-62622: gestisce la modalità di ricerca in MatchQuery.
* ASSETS-62671: Correggi operatore MatchQuery startsWith.
* ASSETS-62780: attiva/disattiva la funzione per l’API delle cartelle.
* ASSETS-62988: nasconde la visualizzazione della rappresentazione del manifesto c2pa nella scheda delle rappresentazioni.
* ASSETS-63336: la sincronizzazione dei modelli da AEM a DM deve avvenire solo per i metadati con spazio dei nomi DAM.
* ASSETS-63375: attivazione/disattivazione della funzione per caricare le risorse in API sperimentali.
* ASSETS-63453: assicurati che tutti gli utenti possano leggere la configurazione di omnisearch.
* GRANITE-63744: consente la connessione dei processi asincroni ai processi sling.
* GRANITE-64567: disattiva automaticamente la ricerca semantica per le ricerche SKU.
* GUIDES-41187: aggiungi le intestazioni per l’utilizzo delle guide.
* SITES-30452: API di contenuto con ASO - suggerimenti per titolo e descrizione.
* SITES-33116: corregge la convalida del percorso.
* SITES-34234: Editor pagina: mantiene lo stato della struttura del contenuto.

### Problemi risolti {#fixed-issues-24464}

* ASSETS-43198: le e-mail di notifica della scadenza delle risorse non rispettano le preferenze della lingua utente.
* ASSETS-51840: miglioramenti nell’elaborazione delle risorse.
* ASSETS-52061: impossibile tornare indietro dopo aver selezionato la ricerca salvata.
* ASSETS-53155: miglioramenti al contenuto delle risorse.
* ASSETS-53745: il flusso di download di Dynamic Media richiede di deselezionare la risorsa originale prima di scegliere il predefinito web.
* ASSETS-54260: Correzioni ai contenuti delle risorse.
* ASSETS-54787: miglioramenti al contenuto delle risorse.
* ASSETS-57391: aggiornamenti del contenuto delle risorse.
* ASSETS-59213: cq-dynamicmedia-core dipende dalla libreria commons-lang obsoleta.
* ASSETS-59214: cq-scene7-imaging dipende dalla libreria commons-lang obsoleta.
* ASSETS-59546: cq-remotedam-client-core dipende dalla libreria commons-lang obsoleta.
* ASSETS-59703: cq-dam-core dipende dalla libreria commons-lang obsoleta.
* ASSETS-59705: cq-dam-handler dipende dalla libreria commons-lang obsoleta.
* ASSETS-59707: cq-dam-indesign dipende dalla libreria commons-lang obsoleta.
* ASSETS-59709: cq-scene7-core dipende dalla libreria commons-lang obsoleta.
* ASSETS-59929: il file CSV generato dall’esportazione dei metadati si interrompe quando il campo contiene il carattere di nuova riga.
* ASSETS-60241: il processo di spostamento asincrono non riesce quando si rinomina la cartella.
* ASSETS-61134: rimuovere i tag comparisonVersion dai file POM.
* ASSETS-61309: lo spostamento o la copia dei frammenti di contenuto non aggiorna più i riferimenti interni.
* ASSETS-61730: il reindirizzamento a Direct Binary Access deve rispettare la codifica delle risorse.
* ASSETS-62358: il file CSV dei rapporti di Assets mostra i valori danneggiati nel percorso del contenuto.
* ASSETS-62610: il pulsante di licenza di Adobe Stock è disabilitato nell’interfaccia utente di Assets.
* ASSETS-62613: NPE in `downloadasset`/`saveas`.
* ASSETS-62656: l’indicatore della Ricerca IA Omnisearch non veniva visualizzato correttamente per le ricerche non Assets.
* GRANITE-55387: se si corregge una parola racchiusa tra virgolette, verrà eliminata l&#39;intera parola.
* GRANITE-61240: RCE tramite XSS memorizzato in lazycontainer.js.
* GRANITE-64101: gli indici OOTB convertiti in ES sono tornati a Lucene al riavvio.
* SITES-24530: la destinazione touch dei pulsanti di chiusura/rimozione nella finestra modale di ricerca non è sufficientemente grande.
* SITES-31425: messaggio di errore non localizzato nel flusso di lavoro iniziale.

### Problemi noti {#known-issues-24464}

Nessuna.

### Funzioni e API obsolete {#deprecated-24464}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-24464}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 14 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-24464}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,90,0 | [API Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache HTTPD 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componenti core AEM | 2.30.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predefinito) | [Versioni Node.js supportate](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

