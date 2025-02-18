---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 49%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 19567 {#19567}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 19567, rilasciata pubblicamente il mercoledì 18 febbraio 2025. La versione di manutenzione precedente era la 19352.

Con la versione di attivazione funzioni 2025.2.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-19567}

* GRANITE-56650: la distribuzione del contenuto deve segnalare solo la coda bloccata dopo alcuni tentativi
* SKYOPS-89616: consente di creare fino a 40 account tecnici in Adobe Developer Console

### Problemi risolti {#fixed-issues-19567}

* CNTBF-232: pacchetti profondi nt:file nodi da includere jcr:content figlio obbligatorio
* CQ-4358930: Problema di prestazioni durante il caricamento delle proprietà della pagina con molti campi multipli
* GRANITE-55960: Problema di prestazioni con il campo Coral Select in AEM as Cloud Service
* GRANITE-56197: il nuovo passaggio del flusso di lavoro TreeActivation non raggruppa le risorse in una struttura di cartelle piatta di grandi dimensioni

#### Guide AEM {#guides}

* GUIDE-23526: quando si aggiornano le condizioni dal profilo di cartella, tutti i gruppi di condizioni vengono persi e le condizioni vengono appiattite.
* GUIDES-22574: se un collegamento esterno contiene un UUID, viene sottoposto a post-elaborazione e converte il collegamento esterno in UUID, interrompendo in tal modo il collegamento nell’editor e anche nei siti di pubblicazione.
* GUIDES-24983: quando si copia un’immagine da un prodotto esterno (ad esempio, MS PowerPoint) e la si incolla nelle guide, si verifica un’interruzione della funzionalità di caricamento rapido della risorsa da utilizzare nel file.
* GUIDES-21772: la generazione nativa di PDF non riesce per il contenuto con **attributo chunk** impostato su **to-content**.
* GUIDES-23964: quando si sceglie **Modifica proprietà**, nella finestra di dialogo della baseline non vengono visualizzati i criteri salvati in precedenza per la baseline dinamica.
* GUIDES-19067: quando si duplica un profilo di cartella, anche il relativo elenco di utenti amministratori viene copiato dal profilo di cartella originale

Per ulteriori informazioni sulle funzioni nuove e migliorate e sui problemi risolti in questa versione, vedi [Roadmap delle versioni di Experience Manager Guides](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemi noti {#known-issues-19567}

Nessuno.

### Funzioni e API obsolete {#deprecated-19567}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-19567}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione riguarda 21 vulnerabilità identificate, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-19567}

| Tecnologia | Versione | Collegamento |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1,76,0 | [API Oak API 1.76.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
