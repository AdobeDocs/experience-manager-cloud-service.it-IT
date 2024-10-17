---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6fa6fc9015624bec9113a198285531a3bdd7e29c
workflow-type: ht
source-wordcount: '773'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 18175 {#release-18175}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 18175, rilasciata pubblicamente il 10 ottobre 2024. La versione di manutenzione precedente era la 17964. La versione 18099 è stata resa privata a causa di un problema.

Con la versione di attivazione funzioni 2024.10.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-18175}

* ASSETS-38322: abilitazione dell’evento di richiesta HTTP per AEM.
* ASSETS-41448: aggiornamento del bundle auth.ims per supportare FI per mappature gruppi.
* ASSETS-41684: aggiunta di configurazioni OSGI OOB per definire FI per mappatura gruppi per Assets, Foundation, Sites e Forms.
* ASSETS-43015: aggiornamento al bundle auth.ims più recente.
* CQ-4356633: aggiunta di un carattere extra nella descrizione “Solo contenuto”.
* GRANITE-50948: integrazione del servizio di archivio in AEM. Supporto per servizio di archivio.
* GRANITE-52454: aggiunta dell’helper di supporto versione 0.1.2.
* GRANITE-52454: aggiornamento dell’helper di supporto GRANITE-52454. Aggiornamento dell’helper di supporto per utilizzare la versione più recente di AEMaaCS.
* GRANITE-53287: aggiornamento della versione del test per l’integrazione di privilegi di sicurezza.
* GRANITE-53485: supporto per l’autenticazione dell’entità principale del servizio per la replica dell’archiviazione BLOB di Azure.
* GRANITE-53514: aggiornamento di Treeactivation alla versione 1.0.26.
* GRANITE-53870: creazione di un meccanismo interno per saltare il controllo della versione max di JVM per l’avvio rapido.
* GRANITE-53914: correzione degli errori di test Platform con Java 17, versione del modulo aggiornata.
* GRANITE-53966: utilizzo di un pool di thread a parte per la distribuzione dei contenuti.
* GRANITE-54006: aggiornamento di Jackson alla versione 2.17.2.
* GRANITE-54038: aggiunta del client IMS Creative Cloud Enterprise all’elenco Consentiti del client IMS di AEM.
* GRANITE-54054: variabile di ambiente per com.adobe.granite.repository.impl.SystemUserValidation warnOnly.
* GRANITE-54266: mancanza del servizio Search Suggestor nell’SDK di produzione.
* GRANITE-54274: accettazione del client IMS di Firefly.
* GRANITE-54300: aggiornamento di Oak all’ultima versione pubblica (1.70.0).
* GUIDES-19069: aggiunta di guidesPeerLinkIndex per il componente aggiuntivo AEM Guides.
* SITES-23584: correzione del test non riuscito per il componente Foundation in Java 17.
* SKYOPS-69768: i modelli Sling non deserializzano ResourceResolver.
* SKYOPS-76378: miglioramento della sicurezza dei thread per la registrazione e l’annullamento della registrazione di ResourceBundle in i18n.
* SKYOPS-79285: aggiornamento di Sling XSS alla versione 2.4.2.
* SKYOPS-82383: esposizione del risultato di conversione, unione e analisi “helm-values” nel descrittore di esecuzione del comando.
* SKYOPS-84810: omissione dell’esecuzione “40-initialize-publish.sh” all’avvio per RDE.
* SKYOPS-84951: correzione del codice di generazione del checksum per contenuti mutabili.
* SKYOPS-85335: aggiornamento di org.apache.sling.jcr.repoinit alla versione 1.1.52.
* SKYOPS-85366: aggiornamento di Sling Commons Threads alla versione 3.3.0.
* SKYOPS-86329: aggiornamento delle versioni dei moduli di test della piattaforma per il supporto dell’SDK Java 21.

### Problemi risolti {#fixed-issues-18175}

* CNTBF-298: rimozione jcr:uuid dai pacchetti esportati CC.
* SKYOPS-83910: correzione dei problemi di concorrenza rilevati in SKYOPS-82371.
* GRANITE-52876: aggiornamento a com.adobe.granite.ui.content 0.8.1448.
* GUIDES-14445: la generazione di PDF nativi non riesce e viene restituito un errore relativo all’ottenimento delle dipendenze per Node.js.
* GUIDES-16961: il titolo con `<conref>` non viene risolto nelle dashboard Linea di base e Traduzione dell’editor web.
* GUIDES-17283: quando si seleziona l’opzione **Usa metadati aggiunti nel meta-argomento**, le proprietà dei metadati non vengono propagate nelle proprietà del documento dell’output di PDF nativi.
* GUIDES-17793: il PDF di riferimento non viene attivato dalla **dashboard per la pubblicazione in blocco** durante l’attivazione in blocco del contenuto pubblicato.

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, consulta [Roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-18175}

* FORMS-15818: la voce del descrittore del componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` non ha trovato istruzioni nei registri del server. Queste sono innocue istruzioni di registro.

### Funzioni e API obsolete {#deprecated-18175}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

Di seguito è riportato un riepilogo delle funzioni dichiarate recentemente obsolete o in fase di rimozione.

#### API di utilizzo di JavaScript {#javascript-use-api}

[L&#39;API di utilizzo di JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) è stata ufficialmente dichiarata obsoleta per le difficoltà che gli utenti devono affrontare durante il debug e la manutenzione del codice che utilizza l’API, nonché per le prestazioni limitate rispetto all’alternativa Java.

È consigliabile passare [all’API di utilizzo di Java,](https://experienceleague.adobe.com/it/docs/experience-manager-htl/content/java-use-api) che offre prestazioni migliori, un debug più semplice e un supporto a lungo termine migliore.

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Adobe è in fase di aggiornamento `com.day.cq.wcm.api`. Parte dei metodi e delle classi sono stati contrassegnati come `@Deprecated` nella versione corrente e verranno rimossi nelle prossime versioni. Passa alle alternative suggerite relative.

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165: rimozione di org.apache.jackrabbit.oak.plugins.blob nell’API pubblica.

### Correzioni di sicurezza {#security-18175}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 2 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-18175}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
