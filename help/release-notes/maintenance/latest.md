---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 36fefbf74a288d60a9529f0c7273dd6b0557177b
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 39%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 15939 {#release-15939}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 15939, rilasciata al pubblico il giovedì 17 aprile 2024. La versione di manutenzione precedente era 15860.

Con l’attivazione delle funzioni 2024.4.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-15939}

* GRANITE-39892: aggiorna la distribuzione in base al limite di dimensioni della coda e la pubblicazione è pronta.
* GRANITE-48777: aggiornamento di QS in com.adobe.granite.security.user-0.4.84 completato.
* GRANITE-49421: sono state aggiunte proprietà per l’entità del servizio segmenti.
* GRANITE-49855: in caso di utilizzo di commons.json, scrivi un analizzatore del modello di feature che non supera la build Quickstart.
* GRANITE-47995: consente di passare alla scrittura di cq:isDelivered.
* GRANITE-36205: aggiorna la versione oak interna all’ultima versione.
* GRANITE-50156 Associa l’affinità AEMCS all’ID utente IMS per l’editor universale.
* GRANITE-50556: aggiorna il bundle crosswalk alla versione v0.1.18.
* GRANITE-50728: Aggiornare FileVault a 3.7.3-T20240308111857-81fa88f1.
* GRANITE-50957: Aggiornare QS a com.adobe.granite.repository a 1.8.114.
* GRANITE-50158: aggiunta del supporto per il flusso da server OAuth a credenziali server nel caricatore YAML.
* GRANITE-51327: Aggiornare Oak all’ultima versione pubblica (1.62.0).
* SKYOPS-68091 Aggiornamento delle immagini runtime di Java 11 alla versione 3.0.0.
* SKYOPS-70421: aggiorna il bundle org.apache.sling.servlet-helpers
* SKYOPS-73483: consenti token di registrazione su AEM.

### Problemi risolti {#fixed-issues-15939}

* GRANITE-46901: aggiungi metriche al client di messaggistica.
* GRANITE-48793: Aggiornare QS a com.adobe.granite.crx-explorer-1.1.28.
* GRANITE-48937: Omniseaarch non funziona sulla pagina aem/start.html.
* GRANITE-49638: Correggi la configurazione errata del tipo di contenuto per la fabbrica di trasformatori RUM.
* GRANITE-50141: IMSProviderImpl sta inviando spam al registro.
* SITES-20949: Errore di ComponentsIT.testEmbed dopo l’aggiunta di referrerpolicy=&quot;strict-origin-when-cross-origin&quot; da parte di Youtube.
* SITES-21233: Aggiornamento dei Componenti core - Correggi pannello a soffietto dopo l’aggiornamento a 15860.
* SKYOPS-74819: compatibilità con le versioni precedenti interrotta per le chiavi duplicate in Apache Commons.
* SKYOPS-67087: in alcuni casi l’aggregazione Clientlib non funziona.
* CQ-4355415: i collegamenti per le notifiche AEM non funzionano in 6.5 SP18.

### Problemi noti {#known-issues-15939}

Nessuno.

### Funzioni e API obsolete {#deprecated-15939}

* [Credenziali JWT nella console Adobe Developer obsolete](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Dai un&#39;occhiata a [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per sapere cosa è stato dichiarato obsoleto o rimosso in AEM as a Cloud Service.

### Tecnologie incorporate {#embedded-tech-15939}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,62,0 | [API Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API SLING AEM | 2.27.2. | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.24.6 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
