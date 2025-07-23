---
title: Best practice per la progettazione di moduli ad alte prestazioni
description: Scopri le best practice essenziali per la creazione di moduli intuitivi, accessibili e dalle prestazioni elevate tramite AEM Forms. Migliora la qualità dei dati, l’esperienza utente e i tassi di successo degli invii.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: 37b20a97942f381b46ce36a6a3f72ac019bba5b7
workflow-type: ht
source-wordcount: '761'
ht-degree: 100%

---

# Best practice per la creazione di moduli

## Panoramica

La creazione di moduli efficaci va oltre l’implementazione tecnica: è importante anche tener conto della psicologia degli utenti, degli standard di accessibilità e dell’ottimizzazione delle prestazioni. Questa guida completa fornisce le best practice comprovate per la progettazione di moduli che gli utenti desiderano effettivamente completare.

### Che cosa imparerai

Alla fine di questo documento comprenderai come:

* Progettare moduli accessibili e di facile utilizzo adatti a tutti
* Ottimizzare le prestazioni dei moduli e dei tempi di caricamento
* Gestire i dati utente in modo responsabile e trasparente
* Implementare la corretta gestione e convalida degli errori
* Creare moduli che raggiungono tassi di completamento elevati

### Pubblico target

Questa guida è progettata per:

* **Sviluppatori di moduli** che desiderano creare esperienze utente migliori
* **Sviluppatori** che implementano la funzionalità del modulo
* **Professionisti UX** che ottimizzano i flussi di lavoro del modulo
* **Stakeholder aziendali** che cercano di migliorare i tassi di conversione del modulo

### Principi chiave

Le forme migliori seguono questi principi fondamentali:

1. **Progettazione incentrata sull’utente**: focus su ciò che gli utenti devono eseguire
2. **Prima accessibilità**: assicurati che tutti possano utilizzare i moduli
3. **Ottimizzazione delle prestazioni**: i moduli veloci vengono completati più spesso
4. **Responsabilità dei dati**: rispetta la privacy degli utenti e riduci al minimo la raccolta dati
5. **Comunicazione chiara**: guida gli utenti attraverso il processo senza problemi

Realizzare ottimi moduli va oltre la semplice tecnologia. Di seguito viene descritto come garantire la facilità d’uso dei moduli e il raggiungimento dei relativi obiettivi:

## Progettazione di moduli intuitivi e accessibili

* **Utilizza etichette chiare e visibili:** per ogni campo modulo è necessaria un’`<label>`. Non fare affidamento solo sul testo segnaposto (testo all’interno del campo di input), in quanto scompare quando gli utenti iniziano a digitare e compromette l’accessibilità.
   * *Buono:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *Non valido:* `<input type="email" placeholder="Email Address">`
* **Semplifica:** se possibile, utilizza i tipi di input standard di HTML (`<input type="date">`, `<input type="tel">`). Spesso dispongono di un supporto mobile e di un’accessibilità migliori rispetto ai widget personalizzati complessi.
* **Ordine logico e raggruppamento:** disponi i campi in modo appropriato per l’utente. Raggruppare i campi correlati utilizzando `<fieldset>` e `<legend>`.
* **Fornisci istruzioni chiare:** per i campi che potrebbero creare confusione, offri testo di aiuto concisi o descrizioni.
* **Navigazione tramite tastiera:** assicurati che gli utenti possano spostarsi attraverso l’intero modulo utilizzando solo la tastiera (Tab, Maiusc+Tab, Invio, Barra spaziatrice).
* **Gestione degli errori:** rendi gli errori evidenti e facili da correggere. Visualizza i messaggi di errore accanto al campo pertinente e spiega cosa è necessario correggere.

* **Assicurati che i moduli vengano caricati rapidamente e che siano visibili**

   * **Posiziona i moduli ben in vista:** se un modulo è importante, assicurati che gli utenti possano visualizzarlo facilmente senza dover scorrere troppo (“sopra la piega”, se possibile). Una ricerca di Adobe mostra che gran parte dei moduli ottengono basse interazioni in quanto nascosti.
   * **Ottimizza le risorse:** mantieni il JavaScript e il CSS personalizzati dei moduli il più leggeri possibile per garantire tempi di caricamento rapidi. Edge Delivery Services facilita il caricamento della pagina di base, ma gli script di moduli pesanti possono comunque rallentare i processi.

* **Gestione responsabile dei dati utente**
   * **Chiedi solo ciò di cui hai bisogno:** meno informazioni personali identificabili (PII) chiedi, meglio è. Ogni campo rappresenta un motivo potenziale per l’abbandono del modulo da parte dell’utente.
   * **Sii trasparente:** spiega chiaramente *perché* hai bisogno di determinate informazioni e *come verranno utilizzate*. Inserisci un collegamento all’informativa sulla privacy. Questo aumenta la fiducia degli utenti.

* **Miglioramento dell’esperienza utente: alternative Captcha**

   * **Ripensa i captcha visibili:** i test del tipo “digita il testo ondulato” o “fai clic su tutti i semafori” possono essere molto frustranti per gli utenti, specialmente quelli con disabilità, e spesso portano a tassi di abbandono elevati.

* **Valuta alternative:**
   * **Campi Honeypot:** aggiungi un campo nascosto che verrà compilato solo dai bot. Se dispone di dati, l’invio è probabilmente spam.
   * **Controlli basati sul tempo:** misura la velocità di invio di un modulo. Invii troppo veloci sono spesso dei bot.
   * **reCAPTCHA invisibile (v3):** questo servizio di Google analizza il comportamento dell’utente in background e presenta una verifica solo se l’utente sembra sospetto. In questo modo si offre spesso un’esperienza utente migliore.

## Progetti modulo - Da fare e da non fare

| ✅ Da fare - Per moduli migliori | ❌ Da non fare - Evita questi |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| Utilizzare tag `<label>` visibili per tutti i campi | Utilizzare solo il testo segnaposto invece delle etichette appropriate |
| Preferisci tipi di input HTML standard (ad esempio, `<input type="email">`) | Utilizzare widget personalizzati eccessivamente complessi |
| Assicurati che la navigazione da tastiera sia completa | Fornire messaggi di errore vaghi o mancanti |
| Mostra messaggi di errore chiari e attuabili | Richiedere dati personali eccessivi senza alcuna giustificazione |
| Richiedi solo le informazioni necessarie | Utilizzare CAPTCHA visibili difficili da risolvere |
| Spiega come vengono utilizzati i dati (informazioni o collegamenti alla privacy) | Nascondi il modulo all’interno della pagina |
| Utilizza tecniche CAPTCHA invisibili o comportamentali |                                                                  |
| Facilita la ricerca del modulo nella pagina (posizionamento prominente) |                                                                  |


## Passaggi successivi

Questa guida ha fornito una panoramica sull’utilizzo dei moduli con AEM Edge Delivery Services. Per istruzioni più dettagliate, passo dopo passo, su configurazioni specifiche, fai riferimento alla documentazione ufficiale di Adobe Experience Manager:

* [Authoring basato su documenti con moduli Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [Editor universale con moduli Edge Delivery Services](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Authoring di documenti (DA) e incorporamento di contenuti](https://www.aem.live/developer/da-tutorial)
* [Servizio di invio dei moduli AEM](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
