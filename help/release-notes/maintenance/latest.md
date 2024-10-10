---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ea7e027b5247b64e78da1d14e4e602f39a37e4bd
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 39%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18099 {#release-18099}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18099, rilasciata pubblicamente il giovedì 9 ottobre 2024. La precedente versione di manutenzione era la 17964.

Con la versione di attivazione funzioni 2024.10.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18099}

* ASSETS-43015: aggiornamento al bundle auth.ims più recente.
* ASSETS-41684: Aggiornamento src/main/features/docker/ethos/base-ims-oauth.json.
* ASSETS-38322: Abilitazione dell’evento di richiesta http per l’AEM.
* ASSETS-41684: aggiungi configurazioni OSGI OOB per definire la mappatura FI-gruppi per Assets, Foundation, Sites e Forms.
* ASSETS-41448: aggiorna il bundle auth.ims per supportare FI nelle mappature di gruppo.
* CQ-4356633: aggiungi un carattere aggiuntivo nella descrizione comando &quot;Solo contenuto&quot;.
* SITES-23584: i test dei componenti di Foundation non riescono in Java 17.
* GUIDES-19069: aggiungi guidesPeerLinkIndex per il componente aggiuntivo guide AEM.
* GRANITE-54300: aggiornamento di Oak all’ultima versione pubblica (1.70.0).
* GRANITE-54274: accetta client IMS di Firefly.
* GRANITE-36205: aggiorna la versione interna di oak all’ultima versione.
* GRANITE-45298: un utente con privilegi limitati può ottenere RCE creando un modulo dannoso senza JS ma alla maniera di XSS.
* GRANITE-54266: nell’SDK di produzione manca il servizio Search Suggestor.
* GRANITE-50948: integrazione del servizio repository in AEM Aggiunta di un servizio repository alternativo per lo sviluppo locale.
* GRANITE-53966: utilizza un pool di thread separato per la distribuzione dei contenuti.
* GRANITE-53514: Treeactivation 1.0.26.
* GRANITE-54054: variabile di ambiente per com.adobe.granite.repository.impl.SystemUserValidation warnOnly.
* GRANITE-50948: integrazione del servizio repository nel supporto AEM per il servizio repository.
* GRANITE-52454: aggiunta dell’helper di supporto 0.1.2.
* GRANITE-53514: Treeactivation 1.0.26.
* GRANITE-54038: aggiungere il client Creative Cloud Enterprise IMS al elenco Consentiti di del client AEM IMS.
* GRANITE-36205: aggiorna la versione interna di oak all’ultima versione.
* GRANITE-53485: supporta l’autenticazione dell’entità servizio per la replica dell’archiviazione BLOB di Azure.
* GRANITE-54006: aggiorna Jackson alla versione 2.17.2.
* GRANITE-53287: aggiornamento della versione del test per l’integrazione dei privilegi di sicurezza.
* GRANITE-53914: errori di test della piattaforma con Java 17 versione del modulo aggiornata.
* GRANITE-53870: crea un meccanismo interno per saltare il controllo della versione JVM massima per l’avvio rapido.
* GRANITE-52454: Aggiornamento dell’helper di supporto GRANITE-52454 aggiornamento dell’helper di supporto per utilizzare la versione più recente di AEMaaCS.
* SKYOPS-85335: aggiorna org.apache.sling.jcr.repoinit al 1.1.52.
* SKYOPS-85336: Aggiorna Sling Commons Threads alla versione 3.3.0.
* SKYOPS-76378: migliora la sicurezza dei thread per la registrazione/annullamento della registrazione ResourceBundle in i18n.
* SKYOPS-84951: il codice di generazione del checksum del contenuto mutabile non è corretto.
* SKYOPS-82383: espone il risultato &quot;helm-values&quot; convert-merge-analyze nel descrittore di esecuzione del comando.
* SKYOPS-86329: aggiornamento delle versioni dei moduli di test della piattaforma per il supporto dell’sdk Java 21.
* SKYOPS-69768: i modelli Sling non deserializzano ResourceResolver.
* SKYOPS-84810: salta l’esecuzione &quot;40-initialize-publish.sh&quot; all’avvio per RDE.
* SKYOPS-79285: Aggiornare Sling XSS alla versione 2.4.2

### Problemi risolti {#fixed-issues-18099}

* CNTBF-298: rimuovere jcr:uuid dai pacchetti esportati CC.
* SKYOPS-83910: sono stati risolti i problemi di concorrenza rilevati in SKYOPS-82371.
* GRANITE-52876: Aggiornamento a com.adobe.granite.ui.content 0.8.1448.
* GRANITE-53088: regressione introdotta dalla correzione di SITES-11992.
* GUIDES-14445: la generazione di PDF nativi non riesce e viene generato un errore relativo all’ottenimento delle dipendenze per Node.js.
* GUIDES-16961: il titolo con `<conref>` non viene risolto nelle dashboard Baseline e Traduzione dell&#39;editor Web.
* GUIDES-17283: quando si seleziona l&#39;opzione **Usa metadati aggiunti nell&#39;argomento meta**, le proprietà dei metadati non vengono propagate nelle proprietà del documento dell&#39;output di Native PDF.
* GUIDES-17793: il PDF di riferimento non viene attivato dal **dashboard Publish in blocco** durante l&#39;attivazione in blocco del contenuto pubblicato.

Per ulteriori informazioni sulle funzioni nuove e migliorate delle Guide e sui problemi risolti nella versione, vedi la [roadmap sulla versione di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-18099}

* FORMS - 15818: la voce descrittore componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` non ha trovato istruzioni nei registri del server. Queste sono innocue istruzioni di registro.

### Funzioni e API obsolete {#deprecated-18099}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

Di seguito è riportato un riepilogo delle funzioni dichiarate recentemente obsolete o in fase di rimozione.

#### API di utilizzo di JavaScript {#javascript-use-api}

[L&#39;API di utilizzo di JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) è stata ufficialmente dichiarata obsoleta per le difficoltà che gli utenti devono affrontare durante il debug e la manutenzione del codice che utilizza l’API, nonché per le prestazioni limitate rispetto all’alternativa Java.

È consigliabile passare [all’API di utilizzo di Java,](https://experienceleague.adobe.com/it/docs/experience-manager-htl/content/java-use-api) che offre prestazioni migliori, un debug più semplice e un supporto a lungo termine migliore.

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Adobe è in fase di aggiornamento `com.day.cq.wcm.api`. Parte dei metodi e delle classi sono stati contrassegnati come `@Deprecated` nella versione corrente e verranno rimossi nelle prossime versioni. Passa alle alternative suggerite relative.

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165: Depreca org.apache.jackrabbit.oak.plugins.blob nell’API pubblica.

### Correzioni di sicurezza {#security-18099}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 2 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-18099}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,70,0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
