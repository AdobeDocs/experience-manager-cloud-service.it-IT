---
title: Monitoraggio degli utenti in tempo reale per i moduli di Edge Delivery Services
description: Il monitoraggio degli utenti in tempo reale per i moduli di Edge Delivery Services prevede il monitoraggio e l’analisi continui delle interazioni degli utenti con i moduli.
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: ht
source-wordcount: '701'
ht-degree: 100%

---


# Monitoraggio degli utenti in tempo reale per i moduli di Edge Delivery Services

Adobe Experience Manager utilizza il monitoraggio degli utenti reali (RUM, Real User Monitoring) per comprendere le interazioni dei visitatori con i siti basati su Adobe Experience Manager. Consente di diagnosticare i problemi relativi alle prestazioni e di valutare l’efficacia degli esperimenti. Il Monitoraggio degli utenti reali mantiene la privacy dei visitatori utilizzando le tecniche di campionamento, garantendo che i siti visitati non raccolgano informazioni personali. Non è consentito aggiungere dati personali alla raccolta dati del Monitoraggio degli utenti reali (RUM). Il Monitoraggio degli utenti reali in Adobe Experience Manager è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta dati.

## Vantaggi dell’utilizzo del Monitoraggio utenti reali per i moduli di Edge Delivery Services {#advantages}

AEM utilizza il monitoraggio degli utenti reali per le azioni seguenti:

* Identificare e correggere gli ostacoli delle prestazioni sui siti.
* Stimare il numero di visualizzazioni di pagina ai siti della clientela
* Comprendere l’interazione di Adobe Experience Manager con analisi, targeting o librerie esterne sulla stessa pagina, migliorando la compatibilità.

## Prerequisiti

Puoi visualizzare la dashboard del monitoraggio degli utenti reali per i moduli di Edge Delivery Services accedendo al seguente URL:
https://data.aem.live/?ext=forms

![Schermata di accesso di Monitoraggio degli utenti reali per i moduli di Edge Delivery Services ](/help/edge/assets/rum-login-screen.png)

Per accedere alla dashboard del monitoraggio degli utenti reali per i moduli di Edge Delivery Services, immetti quanto segue:
* **URL**: l’URL è specifico per il sito utente o il dominio. Gli utenti possono filtrare il sito o il dominio per visualizzare la dashboard in base alle proprie esigenze.
* **Chiave dominio**: l’utente genera manualmente la chiave di dominio. Per ricevere assistenza o richiedere informazioni, consulta la documentazione [Genera chiave di dominio RUM](https://aemcs-workspace.adobe.com/rum/generate-domain-key).

### Dashboard del monitoraggio degli utenti reali per i moduli di Edge Delivery Services

Dopo aver inserito l’URL e la chiave di dominio nella schermata di accesso, puoi accedere alla dashboard del monitoraggio degli utenti reali per i moduli di Edge Delivery Services.

L’illustrazione seguente illustra la dashboard del Monitoraggio degli utenti reali (RUM) per i moduli di Edge Delivery Services:

![Dashboard dei moduli di Monitoraggio degli utenti reali (RUM)](/help/edge/assets/rum-forms-dashboard.png)

### Diverse metriche chiave della dashboard dei moduli di Monitoraggio degli utenti reali (RUM) {#different-metrics-rum-dashboard-forms}

Puoi valutare le interazioni dei visitatori con i siti basati su Adobe Experience Manager utilizzando le metriche chiave seguenti:

* **Visualizzazioni moduli**: è il numero totale di moduli sottoposti a rendering per un URL all’interno dell’intervallo di date specificato.
* **Invio modulo**: è il numero totale di moduli inviati per un URL all’interno dell’intervallo di date specificato.
* **Largest Contentful Paint**: mostra la velocità di caricamento dell’URL, indicando il tempo necessario per rendere visibile nel riquadro di visualizzazione l’elemento di contenuto più grande dal momento in cui l’utente richiede l’URL. Questo elemento di contenuto più grande può essere un’immagine, un video o un elemento di testo sostanziale a livello di blocco. Le valutazioni delle prestazioni per la velocità di caricamento degli URL sono suddivise come segue:
   * **Buona**: se il tempo di caricamento è pari o inferiore a 2,5 secondi.
   * **Ok**: se il tempo di caricamento è superiore a 2,5 secondi ma pari o inferiore a 4 secondi.
   * **Scarsa**: se il tempo di caricamento supera i 4 secondi

* **Spostamento del layout cumulativo**: misura la somma totale di tutti i singoli punteggi di spostamento del layout per ogni spostamento imprevisto che si verifica per l’intera durata della pagina. Svolge un ruolo cruciale nell’identificare le prestazioni di una pagina perché quando gli elementi di una pagina si spostano mentre un utente cerca di interagire con essi, l’esperienza utente risulta scadente. Questo punteggio va da zero a qualsiasi numero positivo: zero indica che non vi sono spostamenti, mentre un numero più alto indica più spostamenti di layout sulla pagina. Le metriche delle prestazioni utilizzate per valutare i punteggi di spostamento del layout sono suddivise nelle seguenti categorie:

   * **Buona**: se il punteggio di spostamento del layout è pari o inferiore a 0,1.
   * **Ok**: se il punteggio di spostamento del layout è maggiore di 0,1 ma minore o uguale a 0,25.
   * **Scarsa**: se il punteggio di spostamento del layout supera 0,25.

* **Interazione con elemento successivo**: valuta la velocità con cui una pagina reagisce alle interazioni dell’utente, considerando il tempo necessario alla pagina per rispondere a clic, tocchi e input da tastiera durante la visita di un utente alla pagina. Il valore finale è l’interazione più lunga osservata, senza tenere conto di eventuali anomalie. Le metriche delle prestazioni per l’interazione con l’elemento successivo sono suddivise nelle categorie seguenti:
   * **Buona**: se la durata tra le azioni dell’utente è inferiore o pari a 200 millisecondi (ms).
   * **Ok**: se la durata è superiore a 200 ms ma non superiore a 500 ms.
   * **Scarsa**: se la durata supera i 500 ms.
