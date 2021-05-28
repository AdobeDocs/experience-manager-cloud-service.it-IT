---
title: Normative sulla protezione dei dati e la privacy dei dati - Preparazione di Adobe Experience Manager as a Cloud Service Sites
description: Scopri il supporto di Adobe Experience Manager as a Cloud Service Sites per le varie normative su privacy e protezione dei dati; incluso il Regolamento generale sulla protezione dei dati (RGPD) dell’UE, il California Consumer Privacy Act e le modalità per conformarsi all’implementazione di un nuovo AEM come progetto di Cloud Service.
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 1%

---

# Preparazione di Adobe Experience Manager as a Cloud Service Sites per le normative su privacy e protezione dei dati {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende sostituirsi a una consulenza legale.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative su privacy e protezione dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta del Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta [Centro per la privacy di Adobe](https://www.adobe.com/privacy.html).

Adobe Experience Manager as a Cloud Service Sites è pronto ad aiutare i clienti a rispettare gli obblighi in materia di privacy e protezione dei dati. Questa pagina guida i clienti attraverso le procedure per gestire tali richieste in AEM Sites. Descrive la posizione dei dati privati memorizzati e come rimuoverli manualmente o con codice.

Per ulteriori informazioni, consulta l’ [Centro per la privacy degli Adobi](https://www.adobe.com/privacy.html).

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) .

## Livello di authoring AEM {#aem-author-tier}

Gli account utente e i contenuti UGC sul server di authoring sono descritti nella [documentazione di AEM Foundation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

## Livello di pubblicazione AEM {#aem-publish-tier}

Gli account utente utilizzati per autenticare i visitatori sul sito e i contenuti UGC sul server di pubblicazione sono descritti nella documentazione [AEM Foundation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

Per impostazione predefinita, i componenti AEM Sites non memorizzano i dati dei moduli immessi dai visitatori sul server di pubblicazione. Si consiglia di inoltrare i dati a un sistema di terze parti o ad Adobe Campaign per un’ulteriore elaborazione.

## Consenso/rinuncia {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager è soggetto a un servizio di rinuncia ai cookie utilizzato per gestire il consenso/diniego per gli utenti.

Per rinunciare:

1. Accedi a:
   [Centro per la privacy di Adobe - Rinuncia](https://www.adobe.com/privacy/opt-out.html)

1. Scorri verso il basso fino a **Servizi** - **Experience Cloud dati di utilizzo del servizio**.

1. Selezionare il collegamento a cui si fa riferimento; attualmente intitolato **here**.

1. Ti verranno presentati i seguenti dettagli, insieme alle opzioni di rinuncia o di accesso:

   * Per rinunciare all&#39;aggregazione e all&#39;analisi dei dati relativi alla visita a questo sito, è necessario installare un cookie sul browser. Questo cookie indica che hai rinunciato.

      Se elimini il cookie di rinuncia o se modifichi computer o browser Web, dovrai ripetere la rinuncia.

      Rinuncia - Escludimi dall&#39;aggregazione e dall&#39;analisi della sessione del visitatore (installa il cookie di `amcglobal.sc.omtrdc.net` rinuncia) - Fai clic qui.

      Opt-in: includi me nell’aggregazione e nell’analisi della sessione del visitatore (non installare il `amcglobal.sc.omtrdc.net` cookie di rinuncia) - fai clic qui.
   Per accedere ai collegamenti effettivi, effettua le seguenti operazioni.

   >[!NOTE]
   >
   > C&#39;è un&#39;ulteriore descrizione nel **2. Privacy.** sezione dell&#39; [Adobe Condizioni d&#39;uso generali](https://www.adobe.com/it/legal/terms.html).

## Analytics Foundation {#analytics-foundation}

AEM Sites include un’integrazione opzionale con Analytics Foundation che utilizza funzionalità all’interno del servizio Adobe Analytics On-demand.

Per ulteriori informazioni sulla gestione delle richieste delle persone interessate relative ad Adobe Analytics, consulta [Adobe Analytics e Privacy dei dati](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html).

## Fondazione per la personalizzazione per Target {#personalization-foundation-by-target}

AEM Sites include un’integrazione opzionale con Personalization Foundation by Target che utilizza funzionalità all’interno del servizio Adobe Target On-demand.

Per ulteriori informazioni sulla gestione delle richieste delle persone interessate relative ad Adobe Target, consulta [Adobe Target - Privacy e Regolamento generale sulla protezione dei dati](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM fornisce un livello di dati facoltativo con ContextHub. In questo modo i dati specifici del visitatore vengono mantenuti nel browser e utilizzati per la personalizzazione basata su regole.

Per impostazione predefinita, i dati visitatore non sono memorizzati in AEM; AEM invia regole al livello dati per prendere decisioni sulla personalizzazione nel browser.

### Implementazione di Opt-in/Opt-out {#implementing-opt-in-opt-out}

Il proprietario del sito deve implementare un componente di rinuncia in base alle seguenti linee guida.

Queste linee guida implementano l’opt-in come impostazione predefinita. Pertanto, un visitatore del sito web deve essere chiaramente d’accordo, prima che qualsiasi dato personale sia memorizzato nella persistenza del browser (lato client).

* Il componente di rinuncia deve essere incluso ogni volta che il componente ContextHub è incluso.
* I termini e le condizioni relativi alla protezione dei dati e alla privacy del sito web devono essere visualizzati al visitatore del sito web, consentendo loro di:

   * accettare
   * respingere
   * cambia la scelta

* Se un visitatore accetta i termini e le condizioni del sito, il cookie di rinuncia di ContextHub deve essere rimosso:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Se un visitatore del sito non accetta i termini e le condizioni del sito, il cookie di rinuncia di ContextHub deve essere impostato:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Per verificare se ContextHub è in esecuzione in modalità di rinuncia, la seguente chiamata deve essere effettuata nella console del browser:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Anteprima della persistenza di ContextHub {#previewing-persistence-of-contexthub}

Per visualizzare in anteprima la persistenza utilizzata ContextHub, un utente può:

* Utilizzare la console del browser; ad esempio:

   * Chrome:

      * Apri Strumenti per sviluppatori > Applicazione > Archiviazione:

         * Local Storage > (sito web) > ContextHubPersistence
         * Session Storage > (sito web) > ContextHubPersistence
         * Cookie > (sito web) > SessionPersistence
   * Firefox:

      * Apri Strumenti per sviluppatori > Archiviazione:

         * Local Storage > (sito web) > ContextHubPersistence
         * Session Storage > (sito web) > ContextHubPersistence
         * Cookie > (sito web) > SessionPersistence
   * Safari:

      * Apri Preferenze > Avanzate > Mostra menu di sviluppo nella barra dei menu
      * Apri Develop > Show JavaScript Console

         * Console > Storage > Local Storage > (sito web) > ContextHubPersistence
         * Console > Storage > Session Storage > (sito web) > ContextHubPersistence
         * Console > Archivio > Cookie > (sito web) > Persistenza ContextHub
   * Internet Explorer:

      * Apri Strumenti per sviluppatori > Console

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* Utilizza l’API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      L’archivio ContextHub definisce quale livello di persistenza verrà utilizzato, in modo da visualizzare lo stato corrente della persistenza tutti i livelli devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

Per visualizzare in anteprima la persistenza utilizzata ContextHub, un utente può:

* Usa la console del browser:

   * Chrome - apri Strumenti per sviluppatori > Applicazione > Archiviazione:

      * Local Storage > (sito web) > ContextHubPersistence
      * Session Storage > (sito web) > ContextHubPersistence
      * Cookie > (sito web) > SessionPersistence
   * Firefox - apri Strumenti per sviluppatori > Archiviazione:

      * Local Storage > (sito web) > ContextHubPersistence
      * Session Storage > (sito web) > ContextHubPersistence
      * Cookie > (sito web) > SessionPersistence


* Utilizza l’API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      L’archivio ContextHub definisce quale livello di persistenza verrà utilizzato, in modo da visualizzare lo stato corrente della persistenza tutti i livelli devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Cancellazione della persistenza di ContextHub {#clearing-persistence-of-contexthub}

Per cancellare la persistenza ContextHub:

* Per cancellare la persistenza degli archivi attualmente caricati:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Cancellare un livello di persistenza specifico; ad esempio, sessionStorage:

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
