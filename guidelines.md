---
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 51%

---
# Linee guida per contribuire alla documentazione di Adobe Experience Manager

## Filosofia della documentazione

Gli utenti di Adobe Experience Manager lavorano in ambienti altamente competitivi per creare esperienze digitali che li distinguano dalla concorrenza. Pertanto, è fondamentale che, quando Adobe offre nuovi strumenti avanzati nell’AEM, questi siano integrati da una documentazione accurata e chiara che consenta al cliente di utilizzare immediatamente il proprio investimento nell’AEM e massimizzare il ROI.

Per la documentazione di AEM, l’obiettivo è renderla disponibile agli utenti della soluzione il prima possibile. Pertanto, il team di documentazione dell’AEM dà la priorità a una documentazione accurata e fruibile e si impegna ad aggiornarla e migliorarla continuamente.

## Contributi alla documentazione

Al fine di migliorare continuamente la documentazione di AEM, apprezziamo il contributo dell’intera comunità di utenti AEM. I miglioramenti apportati alla documentazione, che derivino da richieste o segnalazioni di problemi, possono essere correzioni, chiarimenti, ampliamenti ed esempi aggiuntivi.

## Standard della documentazione

Mentre il team di documentazione di Experience Manager accoglie con favore i contributi alla documentazione di Adobe, qualsiasi contributo alla documentazione di AEM, sotto forma di richiesta o problema, deve essere conforme agli standard di contributo e documentazione del team.

I contributi che non soddisfano tali standard possono essere rifiutati.

### Experience Manager di documenti del team casi di utilizzo standard.

La documentazione di AEM riguarda i casi di utilizzo standard. I casi di utilizzo che esulano dall’ambito di installazione e utilizzo standard del prodotto non rientrano nella documentazione di AEM.

### Il team addetto alla documentazione di Experience Manager in genere non documenta i bug o le relative soluzioni.

La documentazione di AEM riguarda i casi di utilizzo standard. Per questo motivo, i bug, gli effetti causati dai bug e le soluzioni alternative per i bug non sono documentati,

Fanne eccezione le note sulla versione, in cui possono essere elencati i problemi noti con possibili soluzioni approvate dal team AEM Product Management.

### I contributi alla documentazione non devono essere usati per rispondere a domande tecniche.

È gradita come contributo qualsiasi idea che punti al miglioramento della documentazione di AEM. Tuttavia, commenti, problemi e richieste sono intesi solo come *contributi*. Non hanno l’obiettivo di rispondere a domande su come usare AEM, come implementare un progetto AEM o risolvere problemi tecnici.

Eventuali domande sull’utilizzo di AEM o su errori tecnici possono essere segnalate attraverso il normale processo di assistenza tramite il [portale di assistenza Experience Manager](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&lang=it#home) o discusse nella [community di Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community).

***I contributi alla documentazione AEM non sostituiscono, ad Adobe, l’Assistenza clienti*** e tutti i contributi che richiedono risposte a domande correlate al supporto sono respinti.

### I contributi devono fare riferimento in modo chiaro alle pagine della documentazione interessate.

Se apri una segnalazione per suggerire miglioramenti alla documentazione, devi includere i collegamenti alle pagine interessate. Se apri una segnalazione utilizzando il collegamento **Modifica pagina** di una pagina della documentazione, il problema verrà creato automaticamente con un collegamento alla pagina in questione.

Ciò non si applica alle richieste pull, che per loro natura fanno riferimento alle pagine interessate.

## Linee guida per la documentazione

Qualsiasi contributo alla documentazione dell’AEM deve seguire determinate linee guida di stile.

L’aderenza a queste linee guida semplifica la revisione del contributo fornito e velocizza quindi l’integrazione nella documentazione dell’AEM.

### Lingua e stile

#### Lingua

* La documentazione di AEM è creata e mantenuta in inglese americano.
* Usa frasi quanto più semplici possibile.
* Usa un linguaggio chiaro e conciso.

Ricorda che i lettori della documentazione dell’AEM sono di tutto il mondo e non ci si può aspettare che siano di madrelingua inglese o che parlino inglese correntemente. Evita i colloquialismi e usa un linguaggio chiaro e semplice.

#### Segui il Manuale di stile di Microsoft®

[Manuale di stile di Microsoft®](https://learn.microsoft.com/en-us/style-guide/welcome/) è una guida di stile per la documentazione disponibile gratuitamente, specifica per la documentazione di software. La documentazione AEM segue questa guida quando possibile.

### Formattazione

| Elemento | Stile |
|---|---|
| Elemento o opzione dell’interfaccia utente | **grassetto** |
| Nome file, percorso, input utente, valori di parametri | `monospaced` |
| Codice, riga di comando | ```Code Block``` |

### Schermate

Le schermate devono essere utilizzate con cautela e solo quando una descrizione testuale è insufficiente.

Non utilizzare marcatori o altre annotazioni nelle schermate (come riquadri rossi, frecce o testo). In questo modo le schermate possono essere riutilizzate o replicate più facilmente nelle versioni localizzate della documentazione.

### Riferimenti a specifiche versioni

È meglio evitare, quando possibile, riferimenti diretti a una versione specifica nel contenuto della documentazione. In tal modo la documentazione sarà più flessibile e potrà essere estesa anche a versioni future.

### Utilizzo di Day, AEM, CQ, CRX

Il prodotto deve sempre essere chiamato con il suo nome completo **Adobe Experience Manager** per la prima volta in un articolo e possono essere successivamente denominati **AEM**.

Non utilizzare Day, Day Software, CQ e CRX, salvo se inevitabile ad esempio nei nomi delle classi o se si fa riferimento alla storia dell’AEM.
