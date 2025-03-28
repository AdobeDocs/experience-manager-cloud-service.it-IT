---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 23ebeb259e5955bd51431844fd67db9b363034ea
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 100%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 19823 {#19823}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 19823, rilasciata al pubblico il 4 marzo 2025. La versione di manutenzione precedente era la 19687.

Con la versione di attivazione funzioni 2025.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-19823}

* ASSETS-46491: gestione eventi OSGI per il cambiamento dello stato di elaborazione delle risorse.
* ASSETS-45613: invio di eventi di annullamento della pubblicazione quando le risorse vengono eliminate o spostate.
* ASSETS-45131: supporto delle proprietà tag personalizzate in Content Hub.

### Problemi risolti {#fixed-issues-19823}

* ASSETS-20433: problemi di acquisizione Dynamic Media con PDF protetti da password.
* ASSETS-24675: opzioni di elaborazione delle immagini non visualizzate per il profilo immagine solo campione.
* ASSETS-41257: il confronto delle versioni di una risorsa riproduce la risorsa con proporzioni errate. Le versioni di una risorsa sono visualizzate nella timeline in ordine errato.
* ASSETS-44894: i segnalibri di visualizzazione delle risorse a volte non sono cliccabili.
* ASSETS-45015: la larghezza e l’altezza di ritaglio avanzato sono impostate su zero se non viene trovata l’handle della risorsa sottoposta a ritaglio avanzato.
* ASSETS-45192: riduzione della frequenza di richieste pulse.
* ASSETS-45724: se il processo di caricamento non viene assegnato, il caricamento DM verrà tentato di nuovo.
* ASSETS-46425: problemi relativi alla ricerca con l’integrazione Adobe Stock.
* ASSETS-27400: il generatore di anteprima delle cartelle potrebbe tentare di aprire l’originale.
* CQ-4358722: gestione di diversi codici di lingua in Java 11 e Java 17.
* SITES-29369: attivazione di eventi di pagina pubblicata/non pubblicata quando una risorsa viene attivata o disattivata.
* SITES-24074: correzione di accessibilità della tastiera in Unified Shell.
* SITES-28058: il titolo della cartella delle risorse non viene trasferito alla Live Copy.

### Problemi noti {#known-issues-19823}

Nessuna.

### Funzioni e API obsolete {#deprecated-19823}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-19823}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 6 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-19823}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak API 1.76.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
