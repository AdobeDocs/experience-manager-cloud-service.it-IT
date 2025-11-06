---
title: Normative sulla protezione dei dati e la privacy dei dati - Compatibilità di AEM Sites
description: Informazioni sul supporto di Adobe Experience Manager as a Cloud Service Sites per le varie normative su privacy e protezione dei dati, incluso il Regolamento generale sulla protezione dei dati (GDPR) dell’UE, il California Consumer Privacy Act e le modalità per conformarsi quando si implementa un nuovo progetto AEM as a Cloud Service.
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
feature: Compliance
role: Admin, Developer, Leader
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 100%

---

# Compatibilità di Experience Manager Sites per le normative su privacy e protezione dei dati {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende esserne una sostituzione.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative su privacy e protezione dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta di Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta [Centro privacy di Adobe](https://www.adobe.com/it/privacy.html).

Adobe Experience Manager as a Cloud Service Sites è pronto ad aiutare i clienti a rispettare gli obblighi in materia di privacy e protezione dei dati. Questa pagina guida i clienti attraverso le procedure per gestire tali richieste in AEM Sites. Descrive la posizione dei dati privati memorizzati e come rimuoverli manualmente o con codice.

Per ulteriori informazioni, visita il [Centro per la privacy Adobe](https://www.adobe.com/it/privacy.html).

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Preparazione di Adobe Experience Manager as a Cloud Service per le normative su privacy e protezione dei dati](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

## Livello di authoring AEM {#aem-author-tier}

Gli account utente e i contenuti UGC sul server di authoring sono trattati nella [documentazione di AEM Foundation](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Livello di pubblicazione AEM {#aem-publish-tier}

Gli account utente utilizzati per autenticare i visitatori sul sito e i contenuti UGC sul server di pubblicazione sono trattati nella [documentazione di AEM Foundation](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

Per impostazione predefinita, i componenti AEM Sites non memorizzano i dati dei moduli immessi dai visitatori sul server di pubblicazione. Si consiglia di inoltrare i dati a un sistema di terzi o ad Adobe Campaign per un’ulteriore elaborazione.

## Consenso/rinuncia {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager è soggetto a un servizio di rinuncia ai cookie utilizzato per gestire il consenso/rifiuto esplicito per gli utenti.

Per rinunciare:

1. Accedi a:
   [Centro per la privacy di Adobe - Rinuncia](https://www.adobe.com/it/privacy/opt-out.html)

1. Scorri verso il basso fino a **Servizi** - **Dati sull’utilizzo del servizio Experience Cloud**.

1. Seleziona il collegamento a cui si fa riferimento, attualmente con titolo **qui**.

1. Ti vengono presentati i seguenti dettagli, insieme alle opzioni di rinuncia o consenso:

   * Per rinunciare all’aggregazione e all’analisi dei dati relativi alla visita a questo sito, è necessario installare un cookie sul browser. Questo cookie indica che hai rinunciato.

     Se elimini il cookie di rinuncia o cambi computer o browser web, devi ripetere la rinuncia.

     Rinuncia: escludimi dall’aggregazione e dall’analisi della sessione del visitatore (installa il cookie di rinuncia `amcglobal.sc.omtrdc.net`) - Fai clic qui.

     Consenso: includimi nell’aggregazione e nell’analisi della sessione del visitatore (non installare il cookie di rinuncia `amcglobal.sc.omtrdc.net`) - Fai clic qui.

   Per accedere ai collegamenti effettivi, esegui le operazioni precedenti.

   >[!NOTE]
   >
   > C’è un’ulteriore descrizione nella **2. Privacy.** sezione dei [termini di utilizzo generali di Adobe](https://www.adobe.com/it/legal/terms.html).

## Analytics Foundation {#analytics-foundation}

AEM Sites include un’integrazione opzionale con Analytics Foundation che utilizza funzionalità interne al servizio Adobe Analytics On-demand.

Per ulteriori informazioni sulla gestione delle richieste dei soggetti interessati in relazione ad Adobe Analytics, consulta [Adobe Analytics e privacy dei dati](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html?lang=it).

## Personalization Foundation by Target {#personalization-foundation-by-target}

AEM Sites include un’integrazione opzionale con Personalization Foundation by Target che utilizza funzionalità interne al servizio Adobe Target On-demand.

Per ulteriori informazioni sulla gestione delle richieste dei soggetti interessati in relazione ad Adobe Target, consulta [Adobe Target - Privacy e Regolamento generale sulla protezione dei dati (RGPD)](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=it).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM fornisce un livello dati facoltativo con ContextHub. In questo modo i dati specifici del visitatore vengono mantenuti nel browser e utilizzati per la personalizzazione basata su regole.

Per impostazione predefinita, i dati visitatore non sono memorizzati in AEM. AEM invia regole al livello dati per prendere decisioni sulla personalizzazione nel browser.

### Implementazione di consenso/rinuncia {#implementing-opt-in-opt-out}

Il proprietario del sito deve implementare un componente di rinuncia in base alle seguenti linee guida.

In queste linee guida il consenso è implementato per impostazione predefinita. Pertanto, un visitatore del sito Web deve dare il suo consenso esplicito prima che qualsiasi dato personale venga memorizzato nella persistenza del browser (lato client).

* Il componente di rinuncia deve essere incluso ogni volta che il componente ContextHub è incluso.
* I termini e le condizioni relativi alla protezione dei dati e alla privacy del sito web devono essere visualizzati al visitatore del sito web, consentendo loro di:

   * accetta
   * rifiuta
   * cambia la scelta precedente

* Se un visitatore del sito accetta i termini e le condizioni del sito, il cookie di rinuncia di ContextHub deve essere rimosso:

  ```
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* Se un visitatore del sito non accetta i termini e le condizioni del sito, il cookie di rinuncia di ContextHub deve essere impostato:

  ```
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* Per verificare se ContextHub è in esecuzione in modalità di rinuncia, è necessario effettuare la seguente chiamata nella console del browser:

  ```
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### Anteprima della persistenza di ContextHub {#previewing-persistence-of-contexthub}

Per visualizzare in anteprima la persistenza utilizzata in ContextHub, un utente può:

* Utilizzare la console del browser, ad esempio:

   * Chrome:

      * Apri Strumenti per sviluppatori > Applicazione > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistence
         * Archiviazione sessione > (sito Web) > ContextHubPersistence
         * Cookie > (sito Web) > SessionPersistence

   * Firefox:

      * Apri Strumenti di sviluppo web > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistence
         * Archiviazione sessione > (sito Web) > ContextHubPersistence
         * Cookie > (sito Web) > SessionPersistence

   * Safari:

      * Apri Preferenze > Avanzate > Mostra menu Sviluppo nella barra dei menu
      * Apri Sviluppo > Mostra console JavaScript

         * Console > Archiviazione > Archiviazione locale > (sito Web) > ContextHubPersistence
         * Console > Archiviazione > Archiviazione sessione > (sito Web) > ContextHubPersistence
         * Console > Archiviazione > Cookie > (sito Web) > ContextHubPersistence

   * Internet Explorer:

      * Apri Strumenti di sviluppo > Console

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`

* Utilizza l’API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     L’archivio ContextHub definisce il livello di persistenza utilizzato, in modo da visualizzare lo stato attuale della persistenza in tutti i livelli che devono essere controllati.

Ad esempio, per visualizzare i dati memorizzati in localStorage:

Per visualizzare in anteprima la persistenza utilizzata in ContextHub, un utente può:

* Usa la console del browser:

   * Chrome - apri Strumenti per sviluppatori > Applicazione > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistence
      * Archiviazione sessione > (sito Web) > ContextHubPersistence
      * Cookie > (sito Web) > SessionPersistence

   * Firefox - apri Strumenti di sviluppo web > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistence
      * Archiviazione sessione > (sito Web) > ContextHubPersistence
      * Cookie > (sito Web) > SessionPersistence

* Utilizza l’API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     L’archivio ContextHub definisce il livello di persistenza utilizzato, in modo da visualizzare lo stato attuale della persistenza in tutti i livelli che devono essere controllati.

Ad esempio, per visualizzare i dati memorizzati in localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Cancellazione della persistenza di ContextHub {#clearing-persistence-of-contexthub}

Per cancellare la persistenza di ContextHub:

* Per cancellare la persistenza degli archivi attualmente caricati:

  ```
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* Per cancellare un livello di persistenza specifico, ad esempio, sessionStorage:

  ```
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* Per cancellare tutti i livelli di persistenza ContextHub, è necessario chiamare il codice appropriato per tutti i livelli:

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
