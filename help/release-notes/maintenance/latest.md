---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3686697c85273ccc13e80b8d7f4ad1ff3c79845d
workflow-type: ht
source-wordcount: '632'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 21706 {#21706}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 21706, rilasciata pubblicamente il 24 luglio 2025. La versione di manutenzione precedente era la 21570.

>[!NOTE]
>
>La versione 21644 è stata resa privata e sostituita dalla versione 21706.

Con la versione di attivazione funzioni 2025.7.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-21706}

* ASSETS-39377: migliora la gestione dei 429 provenienti da archiviazione remota in Importazione in blocco delle risorse.
* ASSETS-46026: profondità massima configurabile per l’esportazione dei metadati.
* ASSETS-49172: le risorse modello Dynamic Media devono ereditare i metadati dalla cartella.
* ASSETS-50209: supporto per la sottostringa nei modelli DM.
* ASSETS-52326: pagina di configurazione di AEM Assets per impostare le preferenze di visualizzazione del titolo delle risorse.
* ASSETS-52805: è stato aggiunto il supporto per output/download CSV per il processo di operazione in blocco.
* ASSETS-52873: è stata aggiunta una nuova configurazione nelle proprietà della cartella per disabilitare l’elaborazione IA per tale cartella.
* ASSETS-53535: prestazioni migliorate per il caricamento video di YouTube.
* ASSETS-53612: controllo per la ricerca ibrida in Assets Omnisearch.
* GRANITE-60183: è stata aggiornata la dipendenza commons-fileupload a 1.6.0.
* GRANITE-60287: è stato aggiornato QS a Jackrabbit 2.22.1.
* SITES-30452: API di contenuto con ASO - Suggerimenti per titolo e descrizione.
* SITES-31677: l’area di lavoro personalizzata supporta l’esportazione dei frammenti di contenuto di AEM in Target.
* SKYOPS-112741: rimuove il bundle `com.adobe.granite.product.support` da AEM-CS SDK.

### Problemi risolti {#fixed-issues-21706}

* ASSETS-12882: problemi di allineamento dell’interfaccia utente dopo l’apertura dei predefiniti visualizzatore.
* ASSETS-48958: problema con la sincronizzazione risorse che modifica lo stato di pubblicazione in AEM Sites locale.
* ASSETS-50856: `dam:processingAttempts` non viene reimpostato durante completeUpload.
* ASSETS-51604: il CSV del report di condivisione dei collegamenti non contiene i dati relativi al campo “condivisi con”.
* ASSETS-51783: fallback alla configurazione DM in `/conf/global` se non viene trovata alcuna configurazione utilizzando la query di ricerca.
* ASSETS-51857: elementi tabella delle risorse non riordinabili.
* ASSETS-52169: rendering della nuova macchina BAT erroneamente incluso nei download delle risorse.
* ASSETS-52229: notifiche casella in entrata mancanti per i rapporti sulle risorse in AEM as a Cloud Service.
* ASSETS-52399: il bug della versione in com.day.cq.dam.api potrebbe interrompere il codice cliente.
* ASSETS-52780: la risorsa può essere contrassegnata per l’anteprima anche senza l’attivazione.
* ASSETS-52866: i video DM di cui è stata eseguita la migrazione rimangono nello stato di elaborazione nella cartella con sincronizzazione DM disabilitata.
* ASSETS-53237: elenco a discesa Profilo colore vuoto nell’editor dei predefiniti per immagini.
* ASSETS-53240: report sulle risorse - l’utilizzo del disco non riesce quando si ottengono le dimensioni del rendering delle risorse provenienti da Dynamic Media.
* ASSETS-53446: errori intermittenti nell’aggiornamento del token di autenticazione di YouTube dovuti a NPE.
* ASSETS-53827: la convalida ACL blocca il salvataggio di set di file multimediali diversi.
* ASSETS-5403: le librerie client Dynamicmedia utilizzate nell’istanza di pubblicazione devono avere `allowProxy=true`.
* ASSETS-54261: l’importazione dei metadati causa la perdita di connessioni e viene bloccata se il download del file non riesce.
* CQ-4359863: la ricerca di parole chiave nei tag è stata interrotta per ordine errato nell’Editor frammenti di contenuto/editor risorse.
* CQ-4359958: rende il supporto openapi compatibile con AEM 6.5.22.0 e versioni successive.
* CQ-4360256: include il percorso del contesto del servlet nel percorso della richiesta per le richieste HTTP gestite tramite il contesto del servlet `/adobe`.
* CQ-4360317: è stato aggiunto il metodo per impostare l’intestazione della data di scadenza durante la creazione delle risposte.
* GRANITE-60311: AEM SDK Quickstart - NPE su “Stampante di configurazione del programma di installazione OSGi”.
* GS-15285: gli utenti vengono visualizzati come disattivati.

### Problemi noti {#known-issues-21706}

Nessuna.

### Funzioni e API obsolete {#deprecated-21706}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-21706}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 4 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-21706}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak API 1.80.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componenti core AEM | 2.29.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
