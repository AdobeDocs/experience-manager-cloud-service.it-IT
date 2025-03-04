---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 30b5d5838087a35a457939cdbaa13c5735df144e
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 53%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 19823 {#19823}

Di seguito sono riepilogati i miglioramenti continui per la versione di manutenzione 19823, rilasciata al pubblico il mercoledì 4 marzo 2025. La versione di manutenzione precedente era la 19687.

Con la versione di attivazione funzioni 2025.3.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-19823}

* ASSETS-46491: gestore eventi OSGI per la modifica dello stato di elaborazione delle risorse.
* ASSETS-45613: invia eventi di annullamento della pubblicazione quando le risorse vengono eliminate o spostate.
* ASSETS-45131: supporto delle proprietà tag personalizzate in Content Hub.

### Problemi risolti {#fixed-issues-19823}

* ASSETS-20433: problemi di acquisizione di Dynamic Media con PDF protetti da password.
* ASSETS-24675: opzioni di elaborazione delle immagini non visualizzate per il profilo immagine solo campione.
* ASSETS-41257: il confronto delle versioni delle risorse riproduce le risorse con proporzioni non corrette. Le versioni delle risorse visualizzate nella timeline sono in ordine errato.
* ASSETS-44894: i segnalibri di visualizzazione Assets potrebbero non essere selezionabili.
* ASSETS-45015: larghezza e altezza di ritaglio avanzate impostate su zero se l’handle della risorsa di ritaglio avanzato non viene trovato.
* ASSETS-45192: ridurre la frequenza delle richieste di impulsi.
* ASSETS-45724: se il processo di caricamento non è assegnato, assicurati che il caricamento DM venga ritentato.
* ASSETS-46425: problemi relativi alla ricerca dell’integrazione di Adobe Stock.
* ASSETS-27400: il generatore di anteprima delle cartelle potrebbe tentare di aprire l’originale.
* CQ-4358722: gestisce diversi codici locali in Java 11 e Java 17.
* SITES-29369: Eventi pagina pubblicata/non pubblicata attivati all’attivazione/disattivazione delle risorse.
* SITES-24074: Correggi l’accessibilità della tastiera in Unified Shell.
* SITES-28058: il titolo della cartella Assets non viene trasferito alla Live Copy.

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
