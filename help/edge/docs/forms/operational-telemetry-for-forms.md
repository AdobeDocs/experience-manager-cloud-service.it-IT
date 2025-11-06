---
title: Telemetria operativa per Edge Delivery Services per AEM Forms as a Cloud Service
description: La telemetria operativa per Edge Delivery Services per AEM Forms as a Cloud Service comporta il tracciamento e l’analisi continui delle interazioni dell’utente con i moduli.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Developer
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 100%

---

# Telemetria operativa per Edge Delivery Services per AEM Forms as a Cloud Service

La telemetria operativa ti consente di ottenere informazioni approfondite e realistiche sul modo in cui i visitatori interagiscono con i siti web di Adobe Experience Manager (AEM). Questo strumento incorporato fornisce dati preziosi per comprendere il comportamento degli utenti, diagnosticare problemi di prestazioni e misurare l’efficacia degli esperimenti sul sito web. La telemetria operativa va oltre i test sintetici, acquisendo le interazioni dell’utilizzo reale, offrendo un quadro più accurato delle prestazioni del sito.

Tuttavia, la telemetria operativa dà priorità alla privacy dei visitatori. Utilizza tecniche di campionamento per raccogliere dati da un sottoinsieme rappresentativo di utenti, garantendo che non venga mai acquisita alcuna informazione di identificazione personale (PII). Inoltre, la telemetria operativa è progettata per una minimizzazione dei dati, per raccogliere solo le metriche essenziali richieste per l’analisi delle prestazioni. Questo approccio consente di ottimizzare i siti AEM mantenendo la fiducia degli utenti.


## Prerequisiti

Puoi visualizzare la dashboard di monitoraggio di Edge Delivery Services per AEM Forms as a Cloud Service accedendo al seguente URL:

https://data.aem.live/?ext=forms

![Schermata di accesso alla telemetria operativa per i moduli di Edge Delivery Services](/help/edge/assets/rum-login-screen.png)

Per accedere alla dashboard di monitoraggio di Edge Delivery Services per AEM Forms as a Cloud Service, inserisci quanto segue:

- **URL**: l’URL è specifico per il sito utente o il dominio. Gli utenti possono filtrare il sito o il dominio per visualizzare la dashboard in base alle proprie esigenze.

- **Chiave dominio**: l’utente genera manualmente la chiave di dominio. Per ottenere le chiavi di dominio per i moduli, contatta il rappresentante Adobe.

### Dashboard di monitoraggio di Edge Delivery Services per AEM Forms as a Cloud Service

Dopo aver inserito l‘URL e le chiavi di dominio nella schermata di accesso, ottieni l’accesso alla dashboard di monitoraggio di Edge Delivery Services per AEM Forms as a Cloud Service.

L’illustrazione seguente mostra la dashboard di Edge Delivery Services per AEM Forms as a Cloud Service:

![Dashboard moduli di telemetria operativa](/help/edge/assets/rum-forms-dashboard.png)

### Diverse metriche chiave della dashboard dei moduli {#different-metrics-operational-telemetry-dashboard-forms}

Questa dashboard fornisce informazioni chiave sul modo in cui i visitatori interagiscono con i moduli sul sito web di Adobe Experience Manager (AEM). Monitorando queste metriche, puoi identificare le aree di miglioramento e ottimizzare i moduli per una migliore esperienza utente e tassi di conversione:

- **Visualizzazioni modulo**: tengono traccia del numero totale di volte in cui vengono visualizzati i moduli
- **Invii di moduli**: tengono traccia del numero totale di invii completati

- **Largest Contentful Paint**: mostra la velocità di caricamento dell’URL, indicando il tempo necessario per rendere visibile nel riquadro di visualizzazione l’elemento di contenuto più grande dal momento in cui l’utente richiede l’URL. Questo elemento di contenuto più grande può essere un’immagine, un video o un elemento di testo sostanziale a livello di blocco. Le valutazioni delle prestazioni per la velocità di caricamento degli URL sono suddivise come segue:
   - **Buona**: se il tempo di caricamento è pari o inferiore a 2,5 secondi.
   - **Ok**: se il tempo di caricamento è superiore a 2,5 secondi ma pari o inferiore a 4 secondi.
   - **Scarsa**: se il tempo di caricamento supera i 4 secondi

- **Spostamento del layout cumulativo**: misura la somma totale di tutti i singoli punteggi di spostamento del layout per ogni spostamento imprevisto che si verifica per l’intera durata della pagina. Svolge un ruolo cruciale nell’identificare le prestazioni di una pagina perché quando gli elementi di una pagina si spostano mentre un utente cerca di interagire con essi, l’esperienza utente risulta scadente. Questo punteggio va da zero a qualsiasi numero positivo: zero indica che non vi sono spostamenti, mentre un numero più alto indica più spostamenti di layout sulla pagina. Le metriche delle prestazioni utilizzate per valutare i punteggi di spostamento del layout sono suddivise nelle seguenti categorie:

   - **Buona**: se il punteggio di spostamento del layout è pari o inferiore a 0,1.
   - **Ok**: se il punteggio di spostamento del layout è maggiore di 0,1 ma minore o uguale a 0,25.
   - **Scarsa**: se il punteggio di spostamento del layout supera 0,25.

- **Interazione con elemento successivo**: valuta la velocità con cui una pagina reagisce alle interazioni dell’utente, considerando il tempo necessario alla pagina per rispondere a clic, tocchi e input da tastiera durante la visita di un utente alla pagina. Il valore finale è l’interazione più lunga osservata, senza tenere conto di eventuali anomalie. Le metriche delle prestazioni per l’interazione con l’elemento successivo sono suddivise nelle categorie seguenti:
   - **Buona**: se la durata tra le azioni dell’utente è inferiore o pari a 200 millisecondi (ms).
   - **Ok**: se la durata è superiore a 200 ms ma non superiore a 500 ms.
   - **Scarsa**: se la durata supera i 500 ms.

## Informazioni utilizzabili

Analizzando queste metriche, puoi identificare opportunità per:

- Semplificare i moduli e ridurre il numero dei campi.
- Migliorare la chiarezza dei moduli con istruzioni ed etichette chiare.
- Ottimizzare il layout del modulo per la reattività mobile.
- Risolvere i problemi tecnici che rallentano il caricamento dei moduli.

Concentrandoti su queste aree, puoi creare moduli più facili da usare e incoraggiare i visitatori a completarli, portando in definitiva a tassi di conversione più elevati.


