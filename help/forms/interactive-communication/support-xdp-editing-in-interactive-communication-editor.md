---
title: Supporto per la modifica XDP nell’Editor di comunicazione interattiva
description: Supporto per la modifica XDP nell’Editor di comunicazione interattiva consente di modificare gli xdp esistenti all’interno dell’Editor di comunicazione interattiva.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 957944da363b506c34c2630aeedbe984442f34b8
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 12%

---


# Supporto per la modifica XDP nell’Editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## Introduzione

L&#39;editor di comunicazione interattiva (IC) ora offre il supporto di **per la modifica dei file XDP (XML Data Package)** nell&#39;ambiente di authoring. Questo miglioramento consente agli autori di gestire, modificare e gestire i modelli XDP senza problemi, senza dover ricorrere a strumenti esterni. Grazie a questa funzionalità, gli utenti possono caricare, visualizzare e modificare i file XDP direttamente nell’editor IC, consentendo un flusso di lavoro unificato ed efficiente dal punto di vista della progettazione alla consegna.

## Come utilizzare il supporto per la modifica XDP nell’editor di comunicazione interattiva

![Trova documento IC](/help/forms/interactive-communication/assets/support-xdp.png)

1. Passa a **Forms > Forms e documenti**.

1. Carica il file XDP utilizzando l&#39;opzione **Crea > Carica file**.

1. Apri XDP in **Editor comunicazioni interattive**.

1. Apporta le **modifiche necessarie alla progettazione o all&#39;associazione dati**.

1. Salva le modifiche. Gli aggiornamenti vengono automaticamente rispecchiati nel file XDP di origine.

## Funzionalità principali

- **Carica e gestisci file XDP:**
Carica modelli XDP tramite **Forms Manager**. Una volta caricati, diventano disponibili per la modifica diretta nell’Editor di comunicazione interattiva.

- **Modifica tramite editor IC:**
Apri e modifica gli XDP utilizzando l’editor IC con accesso completo alle funzioni di modifica esistenti, tra cui le regolazioni di layout, l’associazione dati, lo stile e la configurazione dei componenti.

- **Salva in Source:**
Tutte le modifiche apportate tramite l&#39;editor IC vengono salvate direttamente nel file XDP originale, mantenendo l&#39;integrità della versione e semplificando il flusso di lavoro di progettazione.

## Supporto frammenti

- **Riferimenti frammento:**
Se un XDP fa riferimento a un frammento, tale frammento deve esistere in **AEM nello stesso percorso relativo** definito nel file XDP.
Se manca un frammento, l&#39;editor visualizza un **messaggio di avviso** che indica che il frammento richiesto non è presente.

- **Riutilizzo frammento nell&#39;editor:**
Tutti i frammenti XDP esistenti vengono visualizzati nel **pannello Frammenti** dell&#39;editor IC.
Gli autori possono **trascinare** questi frammenti direttamente nell&#39;area di lavoro. I riferimenti vengono mantenuti, garantendo che gli aggiornamenti ai frammenti si propaghino su tutti gli XDP che li utilizzano.

## Vantaggi

- Elimina la dipendenza da strumenti esterni per la modifica di XDP.

- Mantiene le associazioni di dati e le relazioni tra frammenti esistenti.

- Consente una progettazione coerente e cicli di iterazione più rapidi.

## Best practice

- Assicurati che tutti i frammenti a cui si fa riferimento siano presenti nel percorso relativo corretto prima della modifica.

- Utilizza il controllo della versione per gestire gli aggiornamenti tra XDP e le dipendenze dei frammenti.

- Convalida le associazioni dati dopo la modifica per confermare il rendering corretto.

