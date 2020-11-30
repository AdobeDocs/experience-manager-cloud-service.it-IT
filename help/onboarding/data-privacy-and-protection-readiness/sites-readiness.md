---
title: Norme sulla protezione dei dati e sulla privacy dei dati - Adobe Experience Manager come Cloud Service
description: 'Scopri Adobe Experience Manager come Cloud Service di supporto dei Siti per le varie normative sulla protezione dei dati e la privacy dei dati; incluso il Regolamento generale sulla protezione dei dati (GDPR) dell''UE, il California sulla privacy Act e le modalità per conformarsi all''implementazione di una nuova AEM come progetto di Cloud Service. '
translation-type: tm+mt
source-git-commit: 7b5a427853075054d56bc7ea6569d5d839e282a1
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---


# Adobe Experience Manager come Cloud Service Siti pronti per la protezione dei dati e le normative sulla privacy {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto del presente documento non costituisce consulenza giuridica e non è inteso come sostituto della consulenza legale.
>
>Consulta l&#39;ufficio legale della tua azienda per consigli in merito alle normative sulla protezione dei dati e sulla privacy dei dati.

>[!NOTE]
>
>Per ulteriori informazioni  Adobe  risposta ai problemi di privacy e ciò che ciò significa per voi in quanto clienti  Adobe, consultate [Adobe Centro](https://www.adobe.com/privacy.html)per la privacy.

Adobe Experience Manager come Cloud Service Siti è pronta ad aiutare i clienti a rispettare i loro obblighi in materia di privacy e protezione dei dati. Questa pagina illustra ai clienti le procedure per gestire tali richieste in  AEM Sites. Descrive la posizione dei dati privati memorizzati e come rimuoverli manualmente o con il codice.

Per ulteriori informazioni, vedere il Centro [per la privacy](https://www.adobe.com/privacy.html)Adobe.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Adobe Experience Manager come Cloud Service di preparazione per la protezione dei dati e le normative](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) sulla privacy dei dati.

## Livello di authoring AEM {#aem-author-tier}

Gli account utente e il contenuto UGC sul server di creazione sono trattati nella documentazione [di](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)AEM Foundation.

## Livello di pubblicazione AEM {#aem-publish-tier}

Gli account utente utilizzati per autenticare i visitatori del sito e i contenuti UGC sul server di pubblicazione sono descritti nella documentazione [di](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)AEM Foundation.

Per impostazione predefinita,  componenti AEM Sites non memorizzano i dati dei moduli immessi dai visitatori sul server di pubblicazione. Si consiglia di inoltrare i dati a un sistema di terze parti o  Adobe Campaign per un&#39;ulteriore elaborazione.

## Opt-In/Opt-Out {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager è soggetto a un servizio di rinuncia ai cookie utilizzato per gestire il consenso o il rifiuto per gli utenti.

Per rifiutare:

1. Accedi a:
   [Centro per la privacy  Adobe - Rifiuto](https://www.adobe.com/privacy/opt-out.html)

1. Scorri verso il basso fino a **Servizi** - **Experience Cloud dati** di utilizzo del servizio.

1. Selezionare il collegamento di riferimento; attualmente **con titolo qui**.

1. Verranno presentati i seguenti dettagli, insieme alle opzioni per rifiutare o accettare:

   * Per rifiutare l&#39;aggregazione e l&#39;analisi dei dati relativi alla visita a questo sito, è necessario installare un cookie nel browser. Questo cookie indica che avete rinunciato.

      Se si elimina il cookie di rinuncia, o se si modifica il computer o il browser Web, sarà necessario scegliere di nuovo il rifiuto.

      Rifiuto - Escludi dall’aggregazione e dall’analisi delle sessioni dei visitatori (installa il cookie di `amcglobal.sc.omtrdc.net` rinuncia) - Fai clic qui.

      Consenso: includi me nell’aggregazione e nell’analisi delle sessioni dei visitatori (non installa il cookie di `amcglobal.sc.omtrdc.net` rinuncia) - Fai clic qui.
   Segui i passaggi indicati sopra per accedere ai collegamenti effettivi.

   >[!NOTE]
   >
   > C&#39;è un&#39;ulteriore descrizione nel **2. Privacy.** della sezione [Condizioni generali d&#39;uso](https://www.adobe.com/legal/terms.html)del Adobe.

## Analytics Foundation {#analytics-foundation}

 AEM Sites include un&#39;integrazione opzionale con Analytics Foundation che utilizza funzionalità all&#39;interno  Adobe Analytics On-demand Service.

Per ulteriori informazioni sulla gestione delle richieste di dati relativi a  Adobe Analytics, consulta [Adobe Analytics e privacy](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html)dei dati.

## Personalization Foundation by Target {#personalization-foundation-by-target}

 AEM Sites include un&#39;integrazione opzionale con Personalization Foundation by Target che utilizza funzionalità all&#39;interno  Adobe Target On-demand Service.

Per ulteriori informazioni sulla gestione delle richieste di dati relative a  Adobe Target, consulta [Adobe Target - Privacy e Regolamento](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)generale sulla protezione dei dati.

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM fornisce un livello dati opzionale con ContextHub. In questo modo i dati specifici del visitatore vengono conservati nel browser e utilizzati per la personalizzazione basata su regole.

Per impostazione predefinita, questi dati visitatore non sono memorizzati in AEM; AEM invia regole al livello dati per prendere decisioni di personalizzazione nel browser.

### Implementazione del consenso/rifiuto {#implementing-opt-in-opt-out}

Il proprietario del sito deve implementare un componente di rinuncia in base alle seguenti linee guida.

Queste linee guida implementano il consenso come impostazione predefinita. Pertanto, un visitatore del sito Web deve essere chiaramente d&#39;accordo, prima che qualsiasi dato personale venga memorizzato nella persistenza (lato client) del browser.

* Il componente di rinuncia deve essere incluso ogni volta che viene incluso il componente ContextHub.
* I termini e le condizioni relativi alla protezione dei dati e alla privacy del sito Web devono essere visualizzati al visitatore del sito Web, consentendo loro di:

   * accetto
   * rifiutare
   * modifica la scelta precedente

* Se un visitatore accetta i termini e le condizioni del sito, il cookie di rinuncia ContextHub deve essere rimosso:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Se un visitatore del sito non accetta i termini e le condizioni del sito, il cookie di rinuncia ContextHub deve essere impostato:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Per verificare se ContextHub è in esecuzione in modalità di rifiuto, nella console del browser deve essere effettuata la seguente chiamata:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Anteprima della persistenza di ContextHub {#previewing-persistence-of-contexthub}

Per visualizzare in anteprima la persistenza utilizzata ContextHub, un utente può:

* Utilizzare la console del browser; ad esempio:

   * Effetto cromatura:

      * Apri Strumenti Sviluppatore > Applicazione > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistenza
         * Archiviazione sessione > (sito Web) > ContextHubPersistenza
         * Cookie > (sito Web) > SessionPersistenza
   * Firefox:

      * Apri Strumenti Sviluppatore > Archiviazione:

         * Archiviazione locale > (sito Web) > ContextHubPersistenza
         * Archiviazione sessione > (sito Web) > ContextHubPersistenza
         * Cookie > (sito Web) > SessionPersistenza
   * Safari:

      * Apri Preferenze > Avanzate > Mostra menu Sviluppo nella barra dei menu
      * Apri Sviluppo > Mostra console JavaScript

         * Console > Storage > Archiviazione locale > (sito Web) > ContextHubPersistenza
         * Console > Storage > Archiviazione sessione > (sito Web) > ContextHubPersistenza
         * Console > Storage > Cookie > (sito Web) > ContextHubPersistenza
   * Internet Explorer:

      * Apri strumenti per sviluppatori > Console

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* Utilizzate l&#39;API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      L&#39;archivio ContextHub definisce il livello di persistenza da utilizzare, pertanto per visualizzare lo stato corrente della persistenza tutti i livelli devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

Per visualizzare in anteprima la persistenza utilizzata ContextHub, un utente può:

* Utilizzate la console del browser:

   * Chrome - aprire Strumenti per sviluppatori > Applicazione > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistenza
      * Archiviazione sessione > (sito Web) > ContextHubPersistenza
      * Cookie > (sito Web) > SessionPersistenza
   * Firefox - aprire Strumenti per sviluppatori > Archiviazione:

      * Archiviazione locale > (sito Web) > ContextHubPersistenza
      * Archiviazione sessione > (sito Web) > ContextHubPersistenza
      * Cookie > (sito Web) > SessionPersistenza


* Utilizzate l&#39;API ContextHub nella console del browser:

   * ContextHub fornisce i seguenti livelli di persistenza dei dati:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (impostazione predefinita)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      L&#39;archivio ContextHub definisce il livello di persistenza da utilizzare, pertanto per visualizzare lo stato corrente della persistenza tutti i livelli devono essere controllati.


Ad esempio, per visualizzare i dati memorizzati in localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Cancellazione della persistenza di ContextHub {#clearing-persistence-of-contexthub}

Per cancellare la persistenza ContextHub:

* Per eliminare la persistenza degli store attualmente caricati:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Cancellazione di un livello di persistenza specifico; ad esempio, sessionStorage:

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
