---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 8a1ed1e44db0154854af73a96339d8e416afd3b4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 43%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 13420 {#release-13420}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 13420, rilasciata pubblicamente il 12 settembre 2023. Questa versione di manutenzione sostituisce le 13323 sulla versione.

L’attivazione delle funzioni 2023.9.0 fornirà il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-13420}

- ASSETS-19544: Assets last modified by property (Ultima modifica delle risorse da parte della proprietà) ora è impostato sull’utente che richiede l’elaborazione.

### Problemi risolti {#fixed-issues-13420}

- ASSETS-27628: Creazione errata del nodo &quot;canali&quot; durante la personalizzazione del pannello di ricerca di Assets
- ASSETS-27539: restrizioni di caricamento corrispondenti alle espressioni regolari.
- ASSETS-26530: Unified Shell non riporta gli utenti alla pagina originale.
- ASSETS-22719: le parentesi nella denominazione dei punti di interruzione del ritaglio avanzato interrompono la funzione di modifica del ritaglio avanzato.
- ASSETS-27726: linkshare.html non deve essere indicizzato da Google.
- ASSETS-27791: la convalida dello schema metadati viene eseguita solo per il primo campo.
- ASSETS-25544: è stato corretto il pulsante di annullamento della validità della cache CDN disabilitata.
- ASSETS-26575: troncamento del nome fisso durante la creazione di set di immagini.
- ASSETS-26705: è stata corretta un’elaborazione non necessaria di risorse di cartelle e frammenti di contenuto non DM.
- ASSETS-25740: i lettori a schermo fisso non narrano il nome e il ruolo dei controlli di modifica/ritaglio nella pagina &quot;Modifica ritagli avanzati&quot; utilizzando i tasti freccia giù.
- CQ-4354266: impossibile aprire gli elementi della casella in entrata.
- CQ-4354347: Traduzioni AEM aggiornate.
- DISP-1009: User-Agent come non prima intestazione taglia X-Forwarded-Host.
- Varie correzioni relative a accessibilità e sicurezza.

### Problemi noti {#known-issues-13420}

Nessuno.

### Tecnologie incorporate {#embedded-tech-13420}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
