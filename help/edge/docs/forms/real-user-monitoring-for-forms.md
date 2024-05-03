---
title: Monitoraggio utenti reali per Edge Delivery Services per AEM Forms as a Cloud Service
description: Il monitoraggio degli utenti reali per i Edge Delivery Services per AEM Forms as a Cloud Service prevede il tracciamento e l’analisi continui delle interazioni degli utenti con i moduli.
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 4a534f4335376673c362ef91a877e67a523be560
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 44%

---


# Monitoraggio utenti reali per Edge Delivery Services per AEM Forms as a Cloud Service

Real User Monitoring (RUM) consente di ottenere informazioni sul modo in cui i visitatori interagiscono con i siti web di Adobe Experience Manager (AEM). Questo strumento integrato fornisce dati utili per comprendere il comportamento degli utenti, diagnosticare i problemi di prestazioni e misurare l’efficacia degli esperimenti effettuati sul sito web. RUM va oltre i test sintetici acquisendo interazioni utente reali, offrendo un&#39;immagine più precisa delle prestazioni del sito.

Tuttavia, RUM dà la priorità alla privacy dei visitatori. Utilizza tecniche di campionamento per raccogliere dati da un sottoinsieme rappresentativo di utenti, garantendo che non vengano mai acquisite informazioni personali (PII, personally identifiable information). Inoltre, RUM è progettato tenendo presente la minimizzazione dei dati, raccogliendo solo le metriche essenziali necessarie per l&#39;analisi delle prestazioni. Questo approccio consente di ottimizzare i siti AEM mantenendo al contempo l’affidabilità degli utenti.


## Prerequisiti

Per visualizzare il dashboard di monitoraggio dei Edge Delivery Services per AEM Forms as a Cloud Service, accedi al seguente URL:

https://data.aem.live/?ext=forms

![Schermata di accesso RUM per Edge Delivery Services per Forms](/help/edge/assets/rum-login-screen.png)

Per accedere al dashboard di monitoraggio dei Edge Delivery Services per AEM Forms as a Cloud Service, immetti quanto segue:

* **URL**: l’URL è specifico per il sito utente o il dominio. Gli utenti possono filtrare il sito o il dominio per visualizzare la dashboard in base alle proprie esigenze.

* **Chiave dominio**: l’utente genera manualmente la chiave di dominio.

Per informazioni sulle chiavi di dominio, consulta [Autenticazione](https://www.aem.live/developer/rum#authentication) documentazione.

### Dashboard di monitoraggio per Edge Delivery Services per AEM Forms as a Cloud Service

Dopo aver inserito l’URL e le chiavi del dominio nella schermata di accesso, puoi accedere al dashboard di monitoraggio per i Edge Delivery Services di AEM Forms as a Cloud Service.

L’illustrazione seguente illustra la dashboard RUM per Edge Delivery Services per AEM Forms as a Cloud Service:

![Dashboard dei moduli di Monitoraggio degli utenti reali (RUM)](/help/edge/assets/rum-forms-dashboard.png)

### Diverse metriche chiave del dashboard per Forms {#different-metrics-rum-dashboard-forms}

Questa dashboard fornisce informazioni chiave sul modo in cui i visitatori interagiscono con i moduli sul sito web Adobe Experience Manager (AEM). Monitorando queste metriche, è possibile identificare le aree da migliorare e ottimizzare i moduli per migliorare l’esperienza utente e i tassi di conversione:

* **Visualizzazioni modulo**: tiene traccia del numero totale di volte in cui i moduli vengono visualizzati
* **Invio modulo**: traccia il numero totale di invii completati

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

## Informazioni fruibili

Analizzando queste metriche, puoi identificare le opportunità per:

* Semplificare i moduli e ridurre il numero di campi.
* Migliora la chiarezza dei moduli con istruzioni ed etichette chiare.
* Ottimizza il layout dei moduli per la reattività dei dispositivi mobili.
* Risolvi i problemi tecnici che rallentano il caricamento dei moduli.

Concentrandoti su queste aree, puoi creare moduli più facili da utilizzare e incoraggiare i visitatori a completarli, portando in ultima analisi a tassi di conversione più elevati.