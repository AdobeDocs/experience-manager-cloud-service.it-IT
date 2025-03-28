---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 32%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione X {#X}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione X, rilasciata pubblicamente il 1° aprile 2025. La versione di manutenzione precedente era la 19823.

Con la versione di attivazione funzioni 2025.4.0 verrà fornito il set di funzioni completo per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Miglioramenti {#enhancements-X}

FORMS-19068: è stato aggiunto il supporto per le azioni di invio del connettore AEP nelle API di Forms Manager per migliorare le funzionalità di integrazione dei dati dei moduli.

FORMS-18513: è stato implementato il supporto per la trasformazione della struttura dati nel connettore AEP per migliorare le funzionalità della procedura guidata e la gestione dei dati.

FORMS-18432: è stata implementata la configurazione della precompilazione lato client specifica per il modulo (basata su regex) per abilitare la funzionalità di precompilazione selettiva senza modifiche a livello OSGI.

FORMS-17551: aggiunto supporto per documenti di record (DoR) per le integrazioni di elenchi SharePoint.

### Problemi risolti {#fixed-issues-X}

FORMS-19028: la funzionalità di precompilazione lato client interrompe la gestione degli eventi dei moduli, impedendo la corretta attivazione degli eventi Value commit e DOMContentLoaded al caricamento del modulo.

FORMS-18360: gestione avanzata dell’ambito dell’elenco SharePoint per i team e i siti in Forms Document Management per migliorare l’organizzazione dei dati e il controllo degli accessi.

FORMS-18325: aggiunta configurazione cloud di Adobe Experience Platform (AEP) per migliorare l’integrazione e le funzionalità di elaborazione dei dati dei moduli.

FORMS-18213: è stata implementata la funzionalità di nascondere/escludere i campi disabilitati dal documento record (DoR) per migliorare la chiarezza del documento e l’esperienza utente.

FORMS-18189: è stata modificata la gestione delle funzioni personalizzate per impedire la registrazione degli errori per le librerie client vuote e migliorare la visualizzazione degli errori nell’interfaccia utente.

FORMS-18426: la funzionalità di ricerca elenco di SharePoint non riesce se i nomi degli elenchi contengono caratteri speciali (ad esempio, &quot;-&quot;), influendo sull’integrazione dei moduli con gli elenchi di SharePoint.

FORMS-18375: i moduli basati su Componenti Foundation selezionano erroneamente le configurazioni recaptcha dalla cartella `conf/global` quando non è selezionato alcun contenitore di configurazione specifico.

FORMS-18304: i documenti PDF/A-1b che passano la convalida in Acrobat e LiveCycle ES4 vengono erroneamente contrassegnati come non conformi in AEM 6.5 Forms a causa di errori di colore dipendenti dal dispositivo.

FORMS-18271: l’Editor tema di Forms visualizza messaggi di errore non localizzati che influiscono sull’esperienza utente nella configurazione dei moduli e nella personalizzazione del tema.

FORMS-18068: problemi di rendering del testo in grassetto nel documento record (DoR) per i gruppi di pulsanti di scelta e caselle di controllo che utilizzano campi in formato Rich Text.

FORMS-7016: l&#39;ordine di attivazione della tastiera nell&#39;editor moduli non segue la navigazione logica.

FORMS-6950: sono stati aggiunti i ruoli e gli attributi ARIA richiesti ai componenti treeview del navigatore del file system per migliorare l’accessibilità degli assistenti vocali e per conformarsi allo standard WCAG 4.1.2 per nome, ruolo e valore (livello A).

### Problemi noti {#known-issues-X}

Nessuna.

### Funzioni e API obsolete {#deprecated-X}

Le funzioni e le API obsolete e rimosse in AEM as a Cloud Service sono descritte nei dettagli nel documento [Funzioni e API obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

### Correzioni di sicurezza {#security-X}

AEM as a Cloud Service è dedicato all’ottimizzazione della sicurezza e delle prestazioni della piattaforma. Questa versione di manutenzione affronta le vulnerabilità identificate da X, rafforzando il nostro impegno per una solida protezione del sistema.

### Tecnologie incorporate {#embedded-tech-X}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak API 1.76.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API SLING AEM | 2.27.6 | [API Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | 2.27.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
