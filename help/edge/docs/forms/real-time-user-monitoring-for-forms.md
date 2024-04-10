---
title: Monitoraggio degli utenti in tempo reale per Edge Delivery Services Forms
description: Il monitoraggio degli utenti in tempo reale per i Edge Delivery Services Forms prevede il monitoraggio e l’analisi continui delle interazioni degli utenti con i moduli.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# Monitoraggio degli utenti in tempo reale per Edge Delivery Services Forms

Adobe Experience Manager utilizza il Monitoraggio utente reale (RUM, Real User Monitoring) per comprendere le interazioni dei visitatori con i siti basati su Adobe Experience Manager. Consente di diagnosticare i problemi relativi alle prestazioni e di valutare l’efficacia degli esperimenti. Real User Monitoring mantiene la privacy dei visitatori utilizzando le tecniche di campionamento, garantendo che i siti visitati non raccolgano informazioni personali. Non è consentito aggiungere dati personali alla raccolta dati RUM. Real User Monitoring in Adobe Experience Manager è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta di dati.

## Vantaggi dell&#39;utilizzo del monitoraggio utente in tempo reale per Edge Delivery Services Forms {#advantages}

L’AEM utilizza il monitoraggio degli utenti in tempo reale per i seguenti elementi:

* Identificare e correggere i colli di bottiglia delle prestazioni sui siti.
* Stima del numero di visualizzazioni di pagina alle sedi dei clienti
* Comprendere l’interazione di Adobe Experience Manager con Analytics, targeting o librerie esterne sulla stessa pagina, migliorando la compatibilità.

## Prerequisiti

Puoi visualizzare il dashboard di monitoraggio degli utenti in tempo reale per Edge Delivery Services Forms accedendo al seguente URL: https://data.aem.live/?ext=forms

![Schermata di accesso RUM per Edge Delivery Services Forms ](/help/edge/assets/rum-login-screen.png)

Per accedere al dashboard di monitoraggio utenti in tempo reale per Edge Delivery Services Forms, immetti quanto segue:
* **URL**: l’URL è specifico per il sito utente o il dominio. Gli utenti possono filtrare il sito o il dominio per visualizzare il dashboard in base alle proprie esigenze.
* **Chiave dominio**: l’utente genera manualmente la chiave di dominio. Per assistenza o richieste di informazioni, consultare [Genera chiave di dominio RUM](https://aemcs-workspace.adobe.com/rum/generate-domain-key) documentazione.

### Dashboard di monitoraggio utenti in tempo reale per Edge Delivery Services Forms

Dopo aver inserito l’URL e la chiave di dominio nella schermata di accesso, puoi accedere alla dashboard di monitoraggio degli utenti in tempo reale per Edge Delivery Services Forms.

L’illustrazione seguente illustra la dashboard RUM per Edge Delivery Services Forms:

![Dashboard RUM Forms](/help/edge/assets/rum-forms-dashboard.png)

### Diverse metriche chiave del dashboard RUM per Forms {#different-metrics-rum-dashboard-forms}

Puoi valutare le interazioni dei visitatori con i siti basati su Adobe Experience Manager utilizzando le metriche chiave seguenti:

* **Visualizzazioni moduli**: è il numero totale di moduli sottoposti a rendering per un URL all’interno dell’intervallo di date specificato.
* **Invio modulo**: è il numero totale di moduli inviati per un URL all’interno dell’intervallo di date specificato.
* **Vernice contestata più grande**: mostra la velocità di caricamento dell’URL, indicando il tempo necessario per rendere visibile nel riquadro di visualizzazione l’elemento di contenuto più grande dal momento in cui l’utente richiede l’URL. Questo elemento di contenuto più grande può essere un’immagine, un video o un elemento di testo sostanziale a livello di blocco. Le valutazioni delle prestazioni per la velocità di caricamento degli URL sono suddivise come segue:
   * **Buono**: se il tempo di caricamento è pari o inferiore a 2,5 secondi.
   * **Ok**: se il tempo di caricamento è superiore a 2,5 secondi ma pari o inferiore a 4 secondi.
   * **Non valido**: se il tempo di caricamento supera i 4 secondi

* **Spostamento layout cumulativo**: misura la somma totale di tutti i singoli punteggi di spostamento del layout per ogni spostamento imprevisto che si verifica per l’intera durata della pagina. Svolge un ruolo cruciale nell’identificare le prestazioni di una pagina perché quando gli elementi di una pagina si spostano mentre un utente cerca di interagire con loro, l’esperienza utente risulta scadente. Questo punteggio va da zero a qualsiasi numero positivo: zero indica che non vi sono spostamenti, mentre un numero più alto indica più spostamenti di layout sulla pagina. Le metriche delle prestazioni utilizzate per valutare i punteggi di spostamento del layout sono suddivise nelle seguenti categorie:

   * **Buono**: se il punteggio di spostamento del layout è pari o inferiore a 0,1.
   * **Ok**: se il punteggio di spostamento del layout è maggiore di 0,1 ma minore o uguale a 0,25.
   * **Non valido**: se il punteggio di spostamento del layout supera 0,25.

* **Interazione con la vernice successiva**: valuta la velocità con cui una pagina reagisce alle interazioni dell’utente, considerando il tempo necessario alla pagina per rispondere a clic, tocchi e input da tastiera durante la visita di un utente alla pagina. Il valore finale è l’interazione più lunga osservata, senza tenere conto di eventuali anomalie. Le metriche delle prestazioni per l&#39;interazione con il disegno successivo sono suddivise nelle categorie seguenti:
   * **Buono**: se la durata tra le azioni dell’utente è inferiore o pari a 200 millisecondi (ms).
   * **Ok**: se la durata è superiore a 200 ms ma non superiore a 500 ms.
   * **Non valido**: se la durata supera i 500 ms.

