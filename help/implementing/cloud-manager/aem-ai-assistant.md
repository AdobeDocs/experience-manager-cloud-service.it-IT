---
title: Assistente AI in Adobe Experience Manager (Beta limitato)
description: Utilizza l’Assistente AI in Adobe Experience Manager per aiutarti a trovare risposte, risolvere problemi ed esplorare Sites, Assets, Forms e Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Informazioni sull’Assistente IA in Adobe Experience Manager {#aem-home}

L’Assistente per l’intelligenza artificiale in AEM (Adobe Experience Manager) offre un’interfaccia di conversazione progettata per semplificare la ricerca delle risposte alle query relative a Adobe Experience Manager. Consente di accedere alla conoscenza del prodotto, risolvere i problemi ed esplorare le informazioni disponibili in Experience League. Durante il programma Beta limitato, l’Assistente AI supporta Adobe Experience Manager as a Cloud Service, inclusi Sites, Assets, Forms e Cloud Manager.

>[!IMPORTANT]
>Assicurati di aver rivisto e inviato il contratto utente in modo che Adobe possa abilitare la funzione di AI Assistant per il test e la partecipazione al programma Beta.
>
>Per qualsiasi domanda, invia un&#39;e-mail a [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID.

## Privacy, sicurezza e governance

L’Assistente per l’intelligenza artificiale in AEM è progettato con una forte enfasi sulla privacy, la sicurezza e la governance.

Questo articolo delinea le funzioni incentrate sulla fiducia che è possibile aspettarsi dall’Assistente IA:

* Nessun dato personale viene utilizzato da AI Assistant, anche a scopo di formazione.
* L’Assistente AI non ha accesso ai dati del consumatore.
* Per interagire con l’Assistente AI è necessaria un’autorizzazione esplicita.
* I prompt forniti dall’utente (domande, query e così via) non vengono condivisi con altri clienti.


## Scopri l’Assistente all’intelligenza artificiale per conoscere il prodotto {#ai-prod-insights}

La conoscenza del prodotto include concetti e argomenti derivati dalla documentazione di Adobe Experience League. Queste domande possono essere suddivise nei seguenti sottogruppi:

| Conoscenza del prodotto | Esempi |
| --- | --- |
| Apprendimento puntato | <ul><li>Cos’è Universal Editor?</li><li>Come si crea un programma in Cloud Manager?</li></ul> |
| Rilevamento aperto | <ul><li>Come si utilizza Universal Editor?</li><li>Esiste un modo per copiare il contenuto da un ambiente all’altro?</li></ul> |
| Risoluzione dei problemi | <ul><li>Perché non è possibile accedere a Universal Editor?</li><li>Perché la pipeline non riesce?</li></ul> |

L’ambito attuale dell’Assistente per l’intelligenza artificiale si concentra sulla risoluzione delle domande relative alla conoscenza del prodotto per Adobe Experience Manager as a Cloud Service. Questo ambito include il supporto completo per aree chiave, come Sites, Assets, Forms e Cloud Manager.

## Assistente AI per AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Oltre all&#39;Assistente generale all&#39;intelligenza artificiale per la conoscenza del prodotto, AEM offre un **Assistente all&#39;intelligenza artificiale specializzato per AEM Forms (Forms Experience Builder)**. Questo assistente avanzato può aiutarti attivamente a creare e configurare i moduli tramite prompt in linguaggio naturale e a rispondere a domande specifiche relative ai moduli.

### Funzionalità principali

L’Assistente IA per AEM Forms fornisce:

* **Creazione di moduli**: creazione di nuovi moduli da zero utilizzando descrizioni in linguaggio naturale
* **Importazione progettazione**: converte le progettazioni esistenti (PDF, Figma, immagini) in moduli AEM funzionali
* **Configurazione modulo**: aggiunta di campi, pannelli, regole di convalida e logica condizionale
* **Gestione layout**: organizza la struttura del modulo e ottimizza per dispositivi diversi
* **Configurazione dell&#39;integrazione**: configurare l&#39;invio dei moduli e la gestione dei dati
* **Conoscenza del prodotto**: rispondi alle domande sulle funzioni e le best practice di AEM Forms

### Dove accedere

L’Assistente AI per AEM Forms è disponibile in:

* **Editor universale**: per Edge Delivery Services Form con funzionalità di modifica visiva
* **Editor Forms adattivo**: per configurazione modulo dettagliata e funzioni avanzate
* **Interfaccia utente gestione Forms**: per attività di gestione e creazione moduli di alto livello

### Guida introduttiva

>[!NOTE]
>
> L’Assistente all’intelligenza artificiale per AEM Forms (Forms Experience Builder) è disponibile nel programma per gli utenti che lo hanno adottato in anticipo. Invia un&#39;e-mail dal tuo indirizzo di lavoro a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) per richiedere l&#39;accesso.

Per ulteriori informazioni sull’utilizzo di AI Assistant per AEM Forms, inclusi esempi dettagliati e best practice, consulta la documentazione di AI Assistant per AEM Forms.

### Casi d’uso di esempio

* **&quot;Crea un modulo di feedback del cliente con i campi Nome, E-mail, Valutazione e Commenti&quot;**
* **&quot;Converti questo modulo di applicazione PDF caricato in un modulo adattivo digitale&quot;**
* **&quot;Aggiungere una logica condizionale per visualizzare le informazioni sul coniuge solo quando lo stato civile è &#39;Sposato&#39;&quot;**
* **&quot;Configura questo modulo per inviare dati al nostro sistema CRM&quot;**

Questo assistente specializzato per l’intelligenza artificiale di Forms rappresenta la prossima evoluzione nella creazione di moduli, combinando la potenza dell’intelligenza artificiale con le solide funzionalità dei moduli di AEM per semplificare il flusso di lavoro di creazione dei moduli.

## Come creare domande efficaci {#ai-craft-questions}

Per ricevere le risposte più precise dall’Assistente AI, è importante formulare le domande con chiarezza e contesto. Utilizza i seguenti suggerimenti per garantire che le query siano chiare e ben strutturate:

* Dichiara chiaramente il tuo compito o domanda in modo conciso.
* Evita formulazioni ambigue o sintassi troppo complessa per migliorare la comprensione.
* Includi un contesto pertinente all’attività o alla domanda, in quanto questo approccio aiuta l’Assistente AI a fornire risposte più precise e pertinenti.

### Esempi di domande non supportate {#ai-unsupported-questions}

| Area | Esempi |
| --- | --- |
| Informazioni operative | <ul><li>Quanti ambienti di sviluppo esistono nel mio tenant?</li><li>Chi ha avviato l’ultima pipeline di produzione?</li></ul> |
| Risoluzione dei problemi | <ul><li>Perché la pipeline di produzione non riesce?</li></ul> |
| Attività e automazione | <ul><li>Configura una pipeline di qualità del codice da un ramo di sviluppo.</li></ul> |


## Utilizza l’Assistente AI {#ai-use}


### Avviare o reimpostare una conversazione

È possibile reimpostare l&#39;Assistente AI e avviare una nuova conversazione quando si desidera modificare gli argomenti. Questa funzionalità è particolarmente utile quando si risolvono problemi relativi a query che hanno esito negativo o che forniscono informazioni non corrette.

![Pulsante Avvia conversazione](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Per avviare o reimpostare una conversazione:**

1. Nell&#39;Assistente AI fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Per informare l&#39;Assistente all&#39;intelligenza artificiale di un nuovo argomento o di una modifica dell&#39;argomento, fare clic su **Avvia nuova conversazione**.

### Utilizzare la funzionalità di individuazione

L’Assistente AI include una funzione di individuazione che consente di esplorare gli argomenti e le categorie supportati.

![Icona lampadina idea](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Per utilizzare la funzionalità di individuazione:**

1. Nell&#39;angolo superiore destro dell&#39;Assistente AI fare clic sull&#39;icona ![Informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Selezionare una categoria per visualizzare un elenco di prompt correlati.
1. Scegli un prompt per comprendere meglio i tipi di domande a cui l’Assistente AI può rispondere.

### Fornire feedback sull’Assistente AI

Il tuo input ti aiuta a migliorare l’Assistente AI per ottenere prestazioni e precisione migliori.

Condividi il tuo feedback sulla tua esperienza con l’Assistente AI tramite le seguenti opzioni:

![Miniature in alto, miniature in basso e icone dei flag](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Icona | Descrizione |
| --- | --- |
| ![Icona Anteprima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Fai clic su per indicare cosa è andato bene e per condividere un feedback positivo. |
| ![Icona della struttura delle miniature](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Fai clic su per fornire suggerimenti per migliorare. Aggiungi commenti specifici sulla tua esperienza, che vengono rivisti ogni giorno. |
| ![Icona contrassegno](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Fai clic su per segnalare i dubbi o fornire un feedback dettagliato sulla tua interazione con l’Assistente AI. |

## Domande frequenti sull’Assistente IA {#ai-faq}

Di seguito sono riportate le risposte ad alcune domande comuni sull’Assistente IA:

* **Le informazioni sono fornite dall&#39;Assistente di IA in tempo reale?**\
  No. I contenuti dell’Assistente AI provengono dalla documentazione di Adobe Experience League. Gli aggiornamenti al contenuto potrebbero richiedere un po’ di tempo per essere riflessi nelle risposte.
* **Quali applicazioni Adobe sono supportate dall&#39;Assistente AI?**\
  Attualmente, AI Assistant supporta AEM as a Cloud Service, tra cui Sites, Assets, Forms e Cloud Manager, in particolare per le richieste di informazioni sul prodotto.
* **Quali sono le funzionalità dell&#39;Assistente di intelligenza artificiale?**\
  L’Assistente AI è progettato per rispondere a domande relative alla conoscenza dei prodotti Adobe.
* **L&#39;Assistente IA utilizza informazioni personali per i dati di formazione?**\
  No. L’Assistente AI non utilizza informazioni personali a scopo di formazione. Evita di condividere informazioni personali su te stesso o su altri, inclusi nomi o dettagli di contatto, con l’Assistente AI.
