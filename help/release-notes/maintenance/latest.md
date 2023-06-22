---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 46f0f8ba51b328bef1061d574b0d378a510fcf38
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 31%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 12255 {#release-12255}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 12255, rilasciata pubblicamente il 13 giugno 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 12142.

L’abilitazione delle funzioni per questa versione di manutenzione fornirà il set completo di funzioni con attivazione della funzione 2023.6.0. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-12255}

Nessuno.

### Problemi risolti {#fixed-issues-12255}

- Vari aggiornamenti relativi all’accessibilità
- ASSETS-15116 - Opzione &quot;Vai alla posizione&quot; disponibile nella vista di ricerca di Assets
- ASSETS-17453 - (Dynamic Media) Impossibile selezionare una miniatura personalizzata per i video
- ASSETS-19279 - Archivio di download delle risorse per file di grandi dimensioni
- ASSETS-19544 - Ultima modifica apportata dall’utente per gli aggiornamenti delle risorse
- ASSETS-20146 - (Interfaccia touch) Rapporto Segnalazioni di download di risorse non riuscite a causa di errori di convalida vengono visualizzate sempre nella parte superiore della pagina dell’elenco per i rapporti
- ASSETS-21056: ottimizzazione delle prestazioni di riferimento delle risorse per ridurre al minimo le operazioni di scrittura
- ASSETS-21909 - Impossibile visualizzare il ritaglio video automatico quando il download della vtt non riesce
- ASSETS-22261 - La struttura delle cartelle per il download da Linkshare non è coerente con i download dell’interfaccia utente di Assets
- ASSETS-22550 - Il pannello dei filtri di ricerca è ora aperto per impostazione predefinita
- ASSETS-22920 - L’annullamento della pubblicazione della cartella da Brand Portal non contrassegna le risorse in come non pubblicate
- ASSETS-22922 - I predefiniti visualizzatore disattivati vengono visualizzati nel componente Dynamic Media
- ASSETS-23461 - Pubblicazione rapida Brand Portal dalla vista di ricerca di Assets
- ASSETS-23466 - La gestione dei collegamenti non accessibili InDesign Server non risolve i collegamenti AAL contenenti spazi
- ASSETS-23469 - I filtri risorse predefiniti si scontrano con i filtri personalizzati
- ASSETS-23981 - Funzione di ordinamento per i titoli che non funzionano nei collegamenti della raccolta
- ASSETS-24723 - Le risorse pubblicate sono state rielaborate senza l’intervento dell’utente
- GRANITE-45385 - Migra attivazione struttura per utilizzare il processo sling invece del flusso di lavoro

### Problemi noti {#known-issues-12255}

- ASSETS-25729 - Il menu dello switcher di visualizzazione è disattivato
- ASSETS-25728 - Opzione Rielabora risorsa non disponibile nella vista di ricerca
- ASSETS-22603 - Alcune colonne del rapporto Asset di tipo Download visualizzano valori &quot;null&quot; nell’interfaccia utente. Il file CSV scaricabile non subisce modifiche.

### Tecnologie incorporate {#embedded-tech-12255}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak API 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
