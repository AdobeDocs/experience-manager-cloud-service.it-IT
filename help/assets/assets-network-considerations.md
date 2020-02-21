---
title: Considerazioni sulla rete delle risorse
description: Considerazioni sulla rete durante la progettazione di una distribuzione di Risorse AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ccfb07b3aef2e357434993cdf87ea9962b3c3566

---


# Considerazioni sulla rete delle risorse {#assets-network-considerations}

La comprensione della rete è importante quanto la comprensione delle risorse Adobe Experience Manager (AEM). La rete può influenzare le esperienze di caricamento, scaricamento e utente. Il diagramma della topologia di rete consente di identificare i punti di interruzione e le aree sottoottimizzate della rete che è necessario correggere per migliorare le prestazioni della rete e l&#39;esperienza dell&#39;utente.

Assicurati di includere quanto segue nel diagramma della rete:

* Connettività dal dispositivo client (ad esempio, computer, mobile e tablet) alla rete
* Topologia della rete aziendale
* Connessione a Internet dalla rete aziendale e dall’ambiente AEM
* Topologia dell’ambiente AEM
* Definizione simultanea di utenti dell’interfaccia di rete di AEM
* Flussi di lavoro definiti per l’istanza AEM

## Connettività dal dispositivo client alla rete aziendale {#connectivity-from-the-client-device-to-the-corporate-network}

Iniziate a creare un diagramma della connettività tra i singoli dispositivi client e la rete aziendale. In questa fase, identificate le risorse condivise, come le connessioni WiFi, in cui più utenti accedono allo stesso punto o switch Ethernet per caricare e scaricare le risorse.

![chlimage_1-353](assets/chlimage_1-353.png)

I dispositivi client si connettono alla rete aziendale in vari modi, ad esempio WiFi condiviso, Ethernet a uno switch condiviso e VPN. L’identificazione e la comprensione dei punti di collegamento in questa rete è importante per la pianificazione delle risorse e per modificare la rete.

Nella parte superiore sinistra del diagramma, tre dispositivi sono rappresentati come condivisione di un punto di accesso WiFi a 48 Mbps. Se tutti i dispositivi vengono caricati contemporaneamente, la larghezza di banda della rete WiFi viene condivisa tra i dispositivi. Rispetto al sistema nel suo insieme, un utente può incontrare un diverso punto di scelta per i tre client attraverso questo canale diviso.

È una sfida misurare la velocità reale di una rete WiFi, perché un dispositivo lento può influenzare altri client sul punto di accesso. Se prevedete di utilizzare il WiFi per le interazioni delle risorse, eseguite un test di velocità da più client contemporaneamente per valutare il throughput.

Nella parte inferiore sinistra del diagramma sono rappresentati due dispositivi collegati alla rete aziendale attraverso canali indipendenti. Pertanto, ogni dispositivo può utilizzare una velocità minima di 10 Mbps e 100 Mbps.

Il computer visualizzato a destra ha un limite a monte della rete aziendale su una VPN con una velocità di 1 Mbps. L&#39;esperienza dell&#39;utente per la connessione a 1 Mbps è molto diversa dall&#39;esperienza dell&#39;utente attraverso la connessione a 1 Gbps. A seconda delle dimensioni delle risorse con cui gli utenti interagiscono, il collegamento di collegamento VPN potrebbe non essere sufficiente per l’attività.

## Topologia della rete aziendale {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

Il diagramma mostra velocità di uplink superiori all&#39;interno della rete aziendale rispetto a quelle generalmente utilizzate. Questi tubi sono risorse condivise. Se si prevede che lo switch condiviso gestisca 50 client, potrebbe essere un punto critico. Nel diagramma iniziale, solo due computer condividono la connessione specifica.

## Connessione a Internet dalla rete aziendale e dall’ambiente AEM {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

È importante considerare fattori sconosciuti su Internet e la connessione VPC, perché la larghezza di banda su Internet può essere compromessa a causa del picco di carico o delle interruzioni del fornitore su larga scala. In generale, la connettività Internet è affidabile. Tuttavia, a volte può introdurre dei punti di interruzione.

Dall&#39;uplink di una rete aziendale a Internet, possono esserci altri servizi che utilizzano la larghezza di banda. È importante comprendere quanto della larghezza di banda può essere dedicata o impostata come priorità per Risorse AEM. Ad esempio, se un collegamento da 1 Gbps è già utilizzato all’80%, per le risorse AEM è possibile allocare solo un massimo del 20% della larghezza di banda.

I firewall e i proxy Enterprise possono inoltre modellare la larghezza di banda in molti modi diversi. Questo tipo di dispositivo può dare priorità alla larghezza di banda utilizzando qualità del servizio, limitazioni di larghezza di banda per utente o limiti di bitrate per host. Si tratta di punti di interruzione importanti da esaminare in quanto possono avere un impatto significativo sull’esperienza utente di Assets.

In questo esempio, l&#39;azienda dispone di un collegamento di sollevamento a 10 Gbps. Dovrebbe essere sufficientemente grande per diversi clienti. Inoltre, il firewall impone un limite di velocità host di 10 Mbps. Questa limitazione può limitare il traffico a un singolo host a 10 Mbps, anche se il collegamento a Internet è a 10 Gbps.

Questo è il più piccolo nodo orientato al client. Tuttavia, è possibile valutare la possibilità di apportare modifiche o inserire in una whitelist il gruppo di operazioni di rete responsabile di questo firewall.

Dai diagrammi di esempio, potete concludere che sei dispositivi condividono un canale concettuale a 10 Mbps. A seconda delle dimensioni delle risorse utilizzate, ciò potrebbe risultare inadeguato per soddisfare le aspettative degli utenti.

## Topologia dell’ambiente AEM {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

La progettazione della topologia dell’ambiente AEM richiede una conoscenza dettagliata della configurazione del sistema e della modalità di connessione della rete all’interno dell’ambiente dell’utente.

Lo scenario di esempio include una farm di pubblicazione con cinque server, uno store binario S3 e un supporto dinamico configurati.

Il dispatcher condivide una connessione di 100 Mbps con due entità, il mondo esterno e l’istanza di AEM. Per le operazioni di caricamento e scaricamento simultanee, dividete questo numero per due. L&#39;archivio esterno collegato utilizza una connessione separata.

L’istanza AEM condivide la connessione a 1 Gb/s con più servizi. Dal punto di vista della topologia di rete, equivale a condividere un singolo canale con diversi servizi.

## Flussi di lavoro definiti per l’istanza AEM {#defined-workflows-of-the-aem-instance}

Quando si considerano le prestazioni della rete, potrebbe essere importante considerare i flussi di lavoro e la pubblicazione che si verificheranno nel sistema. Inoltre, lo storage collegato in rete S3 o di altro tipo utilizzato e le richieste di I/O utilizzano la larghezza di banda della rete. Pertanto, anche in una rete completamente ottimizzata, le prestazioni possono essere limitate dall&#39;I/O del disco.

Per semplificare i processi relativi all’assimilazione delle risorse (in particolare durante il caricamento di un gran numero di risorse), esplora i flussi di lavoro delle risorse e scopri di più sulla loro configurazione.

Quando si valuta la topologia interna del flusso di lavoro, è necessario analizzare quanto segue:

* Procedure per la scrittura di una risorsa
* Flussi di lavoro/eventi che si attivano quando la risorsa/i metadati vengono modificati
* Procedure per la lettura di una risorsa

Alcuni elementi da considerare:

* Metadati XMP letti/scritti
* Attivazione e replica automatica
* Caricamento di risorse secondarie/estrazione di pagina
* Flussi di lavoro sovrapposti.

Esempio di cliente per la definizione di un flusso di lavoro risorse.

![chlimage_1-357](assets/chlimage_1-357.png)
