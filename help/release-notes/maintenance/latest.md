---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 0dab7428d8ae5ec4c11a88ff310fad649a365868
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 22%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 13665 {#release-13665}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 13665, rilasciata pubblicamente il 27 settembre 2023. Questa versione di manutenzione sostituisce le 13420 sulla versione.

2023.10.0 Feature Activation fornisce il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-13665}

* Vari miglioramenti nelle API per frammenti di contenuto.
* ASSETS-26713: Assets Dashboard: la nuova dashboard dell’interfaccia utente dell’esperienza ora è raggiungibile dall’interfaccia utente touch.
* SITES-11206: Frammenti di contenuto: API di ricerca per frammenti di contenuto.
* SITES-11262: Frammenti di contenuto: pulsante per passare al nuovo editor di frammenti di contenuto.
* SITES-15447: Componenti core: versione 2.23.4.

### Problemi risolti {#fixed-issues-13665}

* Vari aggiornamenti relativi alla traduzione.
* CQ-4354428: Flussi di lavoro: impossibile completare un’attività nella casella in entrata.
* SITES-9733: Frammenti di contenuto: i riferimenti alle risorse nel pannello dei riferimenti ai frammenti di contenuto mostrano riferimenti 0 (zero).
* SITES-14561: Frammenti di contenuto: conversione da HTML a markup corretta e migliorata.
* SITES-14882: Frammenti di contenuto: dopo aver modificato Frammento di contenuto e chiuso la scheda senza fare clic sul pulsante Salva o chiudi, i valori vengono memorizzati.
* SITES-15167: Frammenti di contenuto: l’applicazione di patch a una variante con un payload non valido non restituisce 400 ma 500.
* SITES-15514: Frammenti di contenuto: output Markdown non valido per una tabella nell’editor Rich Text.
* SITES-15661: Frammenti di contenuto: non utilizzare vincoli univoci e riordinare gli elementi nei campi dei riferimenti nell’API Frammenti.
* SITES-15730: Screens: la funzionalità Anteprima canale Screens non funziona sul dashboard.
* SITES-15995: Frammenti di contenuto: i tipi MIME dei campi di testo del modello e del frammento lungo sono codificati.
* SITES-16074: Frammenti di contenuto: applica tag ai campi che non sono stringhe[] non può essere recuperato da JCR.
* SITES-16084: Frammenti di contenuto: CFHomeCardModelImpl non dispone del navigatore di destinazione.
* SITES-14773: Frammenti esperienza: il riferimento al collegamento non viene aggiornato all’interno del frammento esperienza.
* SITES-14899: Frammenti di esperienza: offerte multiple create per varianti XF in Target.
* SITES-8590: GraphQL: problemi di codifica con le variabili nelle query persistenti.
* SITES-9224: GraphQL: eccezione &quot;Writer has already been closed&quot; in GraphQLServlet.
* SITES-14800: GraphQL: eccezione nelle query GraphQL persistenti con variabili.
* SITES-15586: GraphQL: problema con il filtro delle query persistenti con valori nulli.
* SITES-15622: GraphQL: problema con le query persistenti con numeri e parametri booleani.
* SITES-15654: GraphQL: problema con unioni e proprietà con lo stesso nome.
* SITES-15267: Lanci: la promozione non riprende le pagine di lancio modificate prima del momento di modifica della configurazione del lancio.
* SITES-15406: Lanci: impossibile aggiungere una pagina di lancio.
* SITES-15427: Lanci: comportamento incoerente dell’ambito &quot;Promuovi pagina corrente e sottopagine&quot;.
* SITES-15429: Lanci: creazione di pagine eliminate durante la promozione dei lanci.
* SITES-15462: Lanci: il processo di promozione automatica pubblica le pagine al di fuori dell’ambito della promozione.
* SITES-15815: Lanci: la pagina eliminata dal lancio impedisce la corretta promozione di Launch.
* SITES-15223: Editor pagina: impossibile ridimensionare i componenti nell’emulatore delle dimensioni del tablet.
* SITES-15463: Modelli di pagina: impossibile pubblicare i modelli.

### Problemi noti {#known-issues-13665}

Nessuno

### Tecnologie incorporate {#embedded-tech-13665}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM Oak | 1,54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
