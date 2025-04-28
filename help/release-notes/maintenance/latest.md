---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 20476 {#20476}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 20476, rilasciata pubblicamente il 15 aprile 2025. La versione di manutenzione precedente era la 20133.

Con la versione di attivazione funzioni 2025.4.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-20476}

* CNTBF-411: è stata aggiunta la possibilità di eliminazione del processo sling nel caso in cui venga rilasciato da JCR.
* CQ-4359813: kit di traduzione AEM: 20 marzo.
* CQ-4359811: Kit di traduzione Granite: 20 marzo.
* GRANITE-57863: aggiornamento di Filevault alla versione 3.8.4.
* GRANITE-56154: configurazione di nuovi tentativi esponenziali in oak-segment-azure.
* GRANITE-55999: miglioramento delle prestazioni di UserPropertiesService.
* GRANITE-55781: è stata eliminata la riconfigurazione ridondante dell’iscrizione degli utenti.
* GRANITE-53956: aggiornamento di Azure SDK V8 a V12 per oak-segment-azure.
* GRANITE-50654: nella scheda Autorizzazioni principali, è stato rimosso il caricamento di “tutti” per impostazione predefinita sul front-end.
* SKYOPS-103444: aggiornamento a Sling ResourceResolver 1.12.6.
* SKYOPS-101147: aggiornamento caconfig impl.
* SKYOPS-97124: sono stati aggiunti avvisi dell’Analyser per le versioni obsolete del bundle SPIFly.
* SKYOPS-95826: aggiornamento delle versioni runtime di Java a 11.0.26 e 21.0.6.
* SKYOPS-53671: utilizzo degli artefatti installati della clientela dai modelli di funzioni durante i riavvi di AEM (RDE).

### Problemi risolti {#fixed-issues-20476}

* ASSETS-49027: [Regressione] AemRequestEventFilter interrompe le richieste POST alla console web OSGI.
* ASSETS-44956: non è possibile selezionare una rappresentazione Dynamic Media: i tag script devono essere caricati nel componente di livello principale.
* CNTBF-410: puntatore null getId CheckJob nel bundle ContentCopy.
* CNTBF-341: indice di esportazione ContentCopy al di fuori dei limiti.
* CQ-4355411: le descrizioni comandi rimangono visualizzate nella finestra di dialogo “Preferenze utente”.
* GRANITE-57265: i valori della selezione a discesa non vengono selezionati.
* GRANITE-57067: criteri effettivi mancanti nell’interfaccia utente.
* SITES-30727: il trascinamento potrebbe non riuscire per i componenti secondari nell’editor di AEM.
* SKYOPS-90607: i processi Sling vengono eseguiti in una distribuzione inattiva/contenuti mutabili.
* SKYOPS-95722: è stata rimossa la dimensione `MaxPermSize` dai flag quickstart in AEM-SDK.
* SKYOPS-103569: non è possibile caricare alcune immagini con Java 21: `javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`.

### Problemi noti {#known-issues-20476}

Nessuna.

### Funzioni e API obsolete {#deprecated-20476}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-20476}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 5 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-20476}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.78.0 | [API Oak API 1.78.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.28.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
