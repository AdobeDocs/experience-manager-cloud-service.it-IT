---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cb963a233b5afd4497704233db7f51c37563d0f9
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 18%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 13099 {#release-13099}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 13099, rilasciata pubblicamente il 15 agosto 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 12874.

2023.8.0 Feature Activation fornirà il set completo di funzioni per questa versione di manutenzione. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-13099}

- SITES-13906: GraphQL - Aggiornamento a graphql-java 20.1.
- SITES-8972: GraphQL - Aggiungi l’etichetta dell’opzione in JSON per il tipo di dati Enumerazione.
- SITES-9689: GraphQL - Aggiungi titolo e descrizione in JSON per il tipo di dati Riferimento contenuto.
- SITES-13052: Frammenti di contenuto - Esportare frammenti di contenuto in Adobe Target

### Problemi risolti {#fixed-issues-13099}

- SITES-14937: MSM - Eredita configurazioni di rollout dal valore principale attivati quando premi Salva e chiudi su Live Copy.
- SITES-14847: Frammenti di contenuto - I collegamenti ai frammenti di contenuto non sono evidenziati.
- SITES-11620: Frammenti di contenuto - Il percorso dei riferimenti viene leggermente tagliato nell’interfaccia utente.
- SITES-14171: GraphQL - In alcuni casi, i riferimenti circolari non vengono interrotti per i dati memorizzati nella cache.
- SITES-14577: Frammenti esperienza - La pubblicazione in blocco non funziona per le Live Copy.
- SITES-14341: Interfaccia utente amministratore - Comportamento non coerente del pulsante &quot;Proprietà&quot; quando vengono rimosse le autorizzazioni di eliminazione.
- SITES-11000: Interfaccia utente amministratore - Riferimenti: collegamenti in ingresso mancanti in alcune pagine.
- SITES-11559: Interfaccia utente amministratore - Riferimenti: i collegamenti in entrata mostrano pagine errate.
- SITES-14337: Interfaccia utente amministratore - L’apertura della pagina dell’editor genera un errore in casi specifici.
- SITES-13425: ContextHub - La barra dei menu non viene visualizzata quando si fa clic sul pulsante ContextHub.
- FORMS-9971: quando si esegue il rendering di un modulo adattivo in una lingua diversa, la visibilità dei componenti viene interpretata e applicata in modo errato.
- FORMS-9888: quando un modulo adattivo è impostato per essere reindirizzato a un URL esterno (pagina di ringraziamento) all’invio del modulo, non riesce a essere reindirizzato all’URL esterno.
- FORMS-9845: dopo aver cancellato un menu a discesa utilizzando l’editor di regole, i valori forniti in precedenza persistono, nonostante la supposta autorizzazione.
- FORMS-9263: quando l’etichetta di una casella di controllo contiene caratteri speciali e un utente fa clic sulla casella di controllo, la relativa casella di controllo non è selezionata.
- FORMS-9254: Quando un utente scorre il testo del componente Termini e condizioni, la casella di controllo all’interno del componente viene abilitata automaticamente anche prima che l’utente abbia eseguito lo scorrimento dell’intero testo.
- FORMS-9045: il tag script non risolve i riferimenti a frammenti esterni nell’XDP di base.
- FORMS-9026: quando si tenta di creare un modulo adattivo utilizzando uno schema JSON con enumerazioni con stringhe vuote e la convalida senza errori, il processo si conclude con un errore. Successivamente, dopo l’aggiornamento della pagina, il modulo non viene caricato correttamente e viene visualizzato un modulo vuoto insieme a un errore nei registri.
- FORMS-8964: in Android™ Chrome/Firefox, il testo diventa non modificabile nel componente Casella di testo se viene raggiunto il limite massimo di caratteri.
- FORMS-8668: un numero eccessivo di immagini stack Java™ nei registri degli errori, nonostante il rendering funzionale dei moduli, causa un aumento di dimensioni del file di registro.
- FORMS-8554: il Forms adattivo con caricamento lazy abilitato non funziona in modalità anteprima dell’istanza di authoring.
- FORMS-8177: quando il servizio Forms è attivo, un’eccezione &quot;com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Non è riuscita a recuperare le dipendenze delle risorse.&quot; si verifica. L’errore scompare quando si disabilita il servizio modulo.
- FORMS-3691: ad alcuni oggetti manca l’ambito IIFE (Immediately Invoked Function Expression). Lo scopo principale dell’utilizzo di un IIFE è quello di creare un ambito per le variabili all’interno della funzione, impedendo a tali variabili di inquinare l’ambito globale.


### Problemi noti {#known-issues-13099}

- SITES-15359: il pattern del nome della variante non corrisponde correttamente alle varianti che presentano ```'_'``` nei nomi delle risorse.

### Tecnologie incorporate {#embedded-tech-13099}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
