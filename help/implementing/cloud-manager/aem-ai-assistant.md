---
title: Assistente AI in Adobe Experience Manager (Beta)
description: Utilizza l’Assistente AI per trovare risposte e risolvere eventuali problemi relativi alle soluzioni disponibili in Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 71041c9e4d4afe964f549f193daf8ec72bd97a41
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 1%

---

# Assistente AI in Adobe Experience Manager {#aem-home}

L’Assistente per l’intelligenza artificiale di AEM (Adobe Experience Manager) offre un’interfaccia di conversazione progettata per semplificare la ricerca delle risposte alle query relative a Adobe Experience Manager. Consente di ottenere risposte immediate alle domande relative ai prodotti AEM (*disponibili per tutti gli utenti*) e automatizza la creazione di ticket di supporto (*disponibili per gli amministratori del supporto*).

Durante la versione beta privata, l’Assistente all’intelligenza artificiale di AEM supporta AEM as a Cloud Service, incluse le seguenti soluzioni:

* Sites
* Assets
* Dynamic Media
* Edge Delivery Services
* Cloud Manager
* Moduli

È direttamente incorporato in AEM e accessibile dall’interfaccia utente di AEM Experience Hub, Cloud Manager e Author.

Il seguente video di 3 minuti e 39 secondi offre una guida dettagliata dell’Assistente di intelligenza artificiale di AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3470354?learn=on)

>[!IMPORTANT]
>Assicurati di aver rivisto e inviato il contratto utente in modo che Adobe possa abilitare la funzione di AI Assistant per il test e la partecipazione al programma beta privato.
>
>Per qualsiasi domanda, invia un&#39;e-mail a [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID.

## Ambito {#scope}

L’attuale ambito di applicazione dell’Assistente all’intelligenza artificiale di AEM si concentra sulla risoluzione delle domande relative alla conoscenza del prodotto per Adobe Experience Manager as a Cloud Service. Questo ambito include il supporto completo per aree chiave, come Sites, Assets, Forms, Edge Delivery Services e Cloud Manager.

* **Superfici**: disponibile in AEM Experience Hub, Interfaccia utente Author, Cloud Manager.
* **Funzionalità**: conoscenza del prodotto e primo intervento per la risoluzione dei problemi e la guida, creazione automatizzata di ticket di supporto e ricerca.
* **Valore**: consente di risparmiare tempo, accelerare l&#39;apprendimento e il time-to-value, ridurre la necessità di creare ticket di supporto manualmente e migliorare l&#39;efficienza nella creazione di ticket di supporto.

## Privacy, sicurezza e governance{#privacy-security-governance}

L’Assistente per l’intelligenza artificiale di AEM è progettato con una forte enfasi sulla privacy, la sicurezza e la governance.

Questo articolo delinea le funzioni basate sulla fiducia che è possibile aspettarsi dall’Assistente di intelligenza artificiale di AEM:

* AEM AI Assistant non utilizza dati personali, anche a scopo di formazione.
* L’Assistente all’intelligenza artificiale di AEM non ha accesso ai dati dei consumatori.
* Per interagire con l’Assistente di intelligenza artificiale di AEM è necessaria un’autorizzazione esplicita.
* I prompt forniti dall’utente (domande, query e così via) non vengono condivisi con altri clienti.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Scopri AEM AI Assistant per la conoscenza del prodotto e la creazione automatizzata dei ticket di supporto {#ai-prod-insights}

La conoscenza del prodotto include concetti e argomenti derivati dalla documentazione di Adobe Experience League. Queste domande possono essere suddivise nei seguenti sottogruppi:


| Conoscenza del prodotto | Disponibile per tutti gli utenti<br>Esempi |
| :--- | :--- |
| Apprendimento puntato | <ul><li>Cos’è Universal Editor?</li><li>Come si crea un programma in Cloud Manager?</li></ul> |
| Rilevamento aperto | <ul><li>Come si utilizza Universal Editor?</li><li>Esiste un modo per copiare il contenuto da un ambiente all’altro?</li></ul> |
| Risoluzione di problemi | <ul><li>Perché non è possibile accedere a Universal Editor?</li><li>Perché la pipeline non riesce?</li></ul> |
| **Creazione ticket di supporto** | **Disponibile solo per gli amministratori del supporto &#x200B;**<br>**Esempi** |
| Creazione automatizzata di ticket di supporto per acquisire la cronologia e il contesto delle chat dell’Assistente di intelligenza artificiale | <ul><li>Crea un ticket di supporto per me.</li></ul> |
| Recupera lo stato del ticket di supporto | <ul><li>Mostrami tutti i biglietti di supporto che ho aperto.</li><li>Mostra lo stato del biglietto &quot;E-----------&quot;</li></ul> |

{style="table-layout:auto"}


## Come creare domande efficaci {#ai-craft-questions}

Per ricevere risposte più precise dall’Assistente di intelligenza artificiale di AEM, è importante formulare le domande con chiarezza e contesto. Utilizza i seguenti suggerimenti per garantire che le query siano chiare e ben strutturate:

* Dichiara chiaramente il tuo compito o domanda in modo conciso.
* Evita formulazioni ambigue o sintassi troppo complessa per migliorare la comprensione.
* Includi un contesto pertinente all’attività o alla domanda, in quanto questo approccio consente all’Assistente IA di AEM di fornire risposte più precise e pertinenti.
Ad esempio, nel prompt, è utile denominare la soluzione AEM in cui stai lavorando: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager o Forms.

### Esempi di domande non supportate {#ai-unsupported-questions}

| Area | Esempi |
| --- | --- |
| Informazioni operative | <ul><li>Quanti ambienti di sviluppo esistono nel mio tenant?</li><li>Chi ha avviato l’ultima pipeline di produzione?</li></ul> |
| Risoluzione di problemi | <ul><li>Perché la pipeline di produzione non riesce?</li></ul> |
| Attività e automazione | <ul><li>Configura una pipeline di qualità del codice da un ramo di sviluppo.</li></ul> |


## Utilizzare l’Assistente di AEM AI {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AEM AI Assistant access through Admin Console 

To use the AEM AI Assistant, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AEM AI Assistant in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AEM AI Assistant of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Avviare o reimpostare una conversazione

È possibile reimpostare l&#39;Assistente di AEM AI e avviare una nuova conversazione quando si desidera modificare gli argomenti. Questa funzionalità è particolarmente utile quando si risolvono problemi relativi a query che hanno esito negativo o che forniscono informazioni non corrette.

![Pulsante Avvia conversazione](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Per avviare o reimpostare una conversazione:**

1. Nell&#39;Assistente di AEM AI fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Per informare l&#39;Assistente di AEM AI di un nuovo argomento o di una modifica in un argomento, fare clic su **Avvia nuova conversazione**.

### Utilizzare la funzionalità di individuazione

L’Assistente all’intelligenza artificiale di AEM include una funzione di individuazione che consente di esplorare gli argomenti e le categorie supportati.

![Icona lampadina idea](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Per utilizzare la funzionalità di individuazione:**

1. Nell&#39;angolo superiore destro dell&#39;Assistente di AEM AI fare clic sull&#39;icona ![Informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Selezionare una categoria per visualizzare un elenco di prompt correlati.
1. Scegli un prompt per comprendere meglio i tipi di domande a cui l’Assistente all’intelligenza artificiale di AEM può rispondere.

### Fornire feedback sull’assistente di intelligenza artificiale di AEM

Il tuo input ti aiuta a migliorare l’Assistente all’intelligenza artificiale di AEM per migliorare le prestazioni e la precisione.

Condividi il tuo feedback sulla tua esperienza con l’Assistente di intelligenza artificiale di AEM tramite le seguenti opzioni:

![Miniature in alto, miniature in basso e icone dei flag](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Icona | Descrizione |
| --- | --- |
| ![Icona Anteprima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Fai clic su per indicare cosa è andato bene e per condividere un feedback positivo. |
| ![Icona della struttura delle miniature](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Fai clic su per fornire suggerimenti per migliorare. Aggiungi commenti specifici sulla tua esperienza, che vengono rivisti ogni giorno. |
| ![Icona contrassegno](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Fai clic su per segnalare dubbi o fornire feedback dettagliati sulla tua interazione con l’Assistente IA di AEM. |

## Domande frequenti sull’Assistente di intelligenza artificiale di AEM {#ai-faq}

Di seguito sono riportate le risposte ad alcune domande comuni sull’Assistente IA:

* **Le informazioni sono fornite dall&#39;Assistente di intelligenza artificiale di AEM in tempo reale?**\
  No. I contenuti dell’Assistente AI provengono dalla documentazione di Adobe Experience League. Gli aggiornamenti al contenuto potrebbero richiedere un po’ di tempo per essere riflessi nelle risposte.
* **Quali applicazioni Adobe sono supportate dall&#39;Assistente all&#39;intelligenza artificiale di AEM?**\
  Attualmente, AI Assistant supporta le richieste di informazioni sulla conoscenza del prodotto in AEM as a Cloud Service, tra cui Sites, Assets, Dynamic Media, Cloud Manager e Forms.
* **Quali sono le funzionalità di AEM AI Assistant?**\
  AEM AI Assistant è progettato per rispondere a query relative alla conoscenza dei prodotti Adobe.
* **L&#39;Assistente di AEM AI utilizza informazioni personali per i dati di formazione?**\
  No. AEM AI Assistant non utilizza informazioni personali a scopo di formazione. Evita di condividere informazioni personali su di te o su altri, inclusi nomi o dettagli di contatto, con l’Assistente di intelligenza artificiale di AEM.


## Assistente AI di AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Oltre all&#39;Assistente AEM AI per la conoscenza generale del prodotto, AEM offre anche un **[Assistente AEM Forms AI (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)** specializzato. Questo assistente avanzato può aiutarti attivamente a creare e configurare i moduli tramite prompt in linguaggio naturale e a rispondere a domande specifiche relative ai moduli.

### Funzionalità principali

L’Assistente di AEM Forms AI fornisce:

* **Creazione modulo**: crea nuovi moduli da zero utilizzando descrizioni in linguaggio naturale.
* **Importazione progettazione**: converte le progettazioni esistenti (PDF, Figma, immagini) in AEM Forms funzionali.
* **Configurazione modulo**: aggiungere campi, pannelli, regole di convalida e logica condizionale.
* **Gestione layout**: organizza la struttura del modulo e ottimizza per diversi dispositivi.
* **Configurazione dell&#39;integrazione**: configurare l&#39;invio dei moduli e la gestione dei dati.
* **Conoscenza del prodotto**: rispondi alle domande sulle funzioni e le best practice di AEM Forms.

### Dove accedere

L’Assistente all’intelligenza artificiale di AEM Forms è disponibile nei seguenti casi:

* **Editor universale**: per Edge Delivery Services Form con funzionalità di modifica visiva.
* **Editor Forms adattivo**: per configurazione modulo dettagliata e funzionalità avanzate.
* **Interfaccia utente gestione Forms**: per attività di gestione e creazione moduli di alto livello.

### Guida introduttiva

>[!NOTE]
>
> L’Assistente all’intelligenza artificiale di AEM Forms (Forms Experience Builder) è disponibile nel programma beta privato. Invia un&#39;e-mail dal tuo indirizzo di lavoro a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) per richiedere l&#39;accesso.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;Assistente all&#39;intelligenza artificiale di AEM Forms, consulta la documentazione di [Assistente all&#39;intelligenza artificiale di AEM Forms](/help/edge/docs/forms/forms-ai-assistant.md).

### Casi d’uso di esempio

* **&quot;Crea un modulo di feedback del cliente con i campi Nome, E-mail, Valutazione e Commenti&quot;**
* **&quot;Converti questo modulo di applicazione PDF caricato in un modulo adattivo digitale&quot;**
* **&quot;Aggiungere una logica condizionale per visualizzare le informazioni sul coniuge solo quando lo stato civile è &#39;Sposato&#39;&quot;**
* **&quot;Configurare questo modulo per inviare dati al sistema di gestione delle relazioni con i clienti&quot;**

Questo assistente specializzato per l’intelligenza artificiale di AEM Forms rappresenta la prossima evoluzione nella creazione di moduli, combinando la potenza dell’intelligenza artificiale con le solide funzionalità dei moduli di AEM per semplificare il flusso di lavoro di creazione dei moduli.
