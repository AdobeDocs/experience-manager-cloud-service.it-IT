---
title: Procedure consigliate per la progettazione di Forms ad alte prestazioni
description: Scopri le best practice essenziali per la creazione di moduli facili da usare, accessibili e dalle prestazioni elevate tramite AEM Forms. Migliora la qualità dei dati, l’esperienza utente e i tassi di successo degli invii.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Procedure consigliate per la creazione di Forms

Costruire grandi forme va oltre la semplice tecnologia. Di seguito viene descritto come garantire la facilità d&#39;uso dei moduli e il raggiungimento dei relativi obiettivi:

## Progettazione di Forms facili da usare e accessibili

* **Utilizza etichette chiare e visibili:** Per ogni campo modulo è necessario `<label>`. Non fare affidamento solo sul testo segnaposto (testo all’interno del campo di input), in quanto scompare quando gli utenti digitano e non è accessibile.
   * *Buono:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *Non valido:* `<input type="email" placeholder="Email Address">`
* **Semplifica:** se possibile, utilizza i tipi di input standard di HTML (`<input type="date">`, `<input type="tel">`). Spesso dispongono di un supporto mobile e di un’accessibilità migliori rispetto ai widget personalizzati complessi.
* **Ordine logico e raggruppamento:** Disporre i campi in modo appropriato per l&#39;utente. Raggruppare i campi correlati utilizzando `<fieldset>` e `<legend>`.
* **Fornisci istruzioni chiare:** Per i campi che potrebbero creare confusione, offri testo di aiuto o descrizioni.
* **Navigazione tramite tastiera:** Assicurarsi che gli utenti possano spostarsi nell&#39;intero modulo utilizzando solo la tastiera (Tab, Maiusc+Tab, Invio, Barra spaziatrice).
* **Gestione degli errori:** Rendere gli errori evidenti e facili da correggere. Visualizza i messaggi di errore accanto al campo pertinente e spiega cosa è necessario correggere.

* **Assicurarsi che il Forms venga caricato rapidamente e che sia visibile**

   * **Posiziona Forms in primo piano:** Se un modulo è importante, assicurati che gli utenti possano visualizzarlo facilmente senza troppi spostamenti (&quot;sopra la piega&quot;, se possibile). La ricerca di Adobe mostra che molte forme ottengono bassa interazione perché sono nascoste.
   * **Ottimizza Assets:** Per ridurre al minimo i tempi di caricamento, mantieni qualsiasi JavaScript o CSS personalizzato per i moduli. Edge Delivery Services facilita il caricamento della pagina di base, ma gli script di moduli pesanti possono comunque rallentare le cose.

* **Gestione responsabile dei dati utente**
   * **Chiedi solo ciò di cui hai bisogno:** meno informazioni personali identificabili (PII) chiedi, meglio è. Ogni campo rappresenta un motivo potenziale per l’abbandono del modulo da parte dell’utente.
   * **Sii trasparente:** Spiega chiaramente *perché* hai bisogno di determinate informazioni e *come verranno utilizzate*. Collega all’informativa sulla privacy. In questo modo si crea fiducia.

* **Miglioramento dell&#39;esperienza utente: alternative Captcha**

   * **Ripensa i captcha visibili:** i test &quot;digita il testo ondulato&quot; o &quot;fai clic su tutti i semafori&quot; possono essere molto frustranti per gli utenti, specialmente quelli con disabilità, e spesso portano a tassi di abbandono elevati.

* **Valuta alternative:**
   * **Campi Honeypot:** Aggiungi un campo nascosto che verrà compilato solo dai bot. Se dispone di dati, l’invio è probabilmente spam.
   * **Controlli basati sul tempo:** Misura la velocità di invio di un modulo. Gli invii troppo veloci sono spesso bot.
   * **reCAPTCHA invisibile (v3):** Questo servizio di Google analizza il comportamento dell&#39;utente in background e presenta una sfida solo se l&#39;utente sembra sospetto. Questa è spesso un’esperienza utente migliore.

## Progetti modulo - Da fare e da non fare

| ✅ cose da fare - Per un Forms migliore | ❌ Non eseguire - Evitare questi |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| Usa tag `<label>` visibili per tutti i campi | Utilizza solo il testo segnaposto invece delle etichette appropriate |
| Preferisci tipi di input HTML standard (ad esempio, `<input type="email">`) | Utilizzare widget personalizzati eccessivamente complessi |
| Assicurati che la navigazione da tastiera sia completa | Fornire messaggi di errore vaghi o mancanti |
| Mostra messaggi di errore chiari e actionable | Richiedere dati personali eccessivi senza giustificazione |
| Richiedi solo le informazioni necessarie | Utilizzare CAPTCHA visibili difficili da risolvere |
| Spiegare come vengono utilizzati i dati (informazioni o collegamenti sulla privacy) | Nascondi il modulo all’interno della pagina |
| Utilizzare tecniche CAPTCHA invisibili o comportamentali |                                                                  |
| Facilitare la ricerca del modulo nella pagina (posizionamento prominente) |                                                                  |


## Passaggi successivi

Questa guida offre una panoramica dell’utilizzo dei moduli con AEM Edge Delivery Services. Per istruzioni dettagliate su configurazioni specifiche, consulta la documentazione ufficiale di Adobe Experience Manager:

* [Authoring basato su documenti con Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universale con Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Authoring di documenti (DA) e incorporamento di contenuti](https://www.aem.live/developer/da-tutorial)
* [Servizio di invio AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
