---
title: Oggetto immagine nell’editor di comunicazione interattiva
description: Crea frammenti di comunicazione interattiva in AEM Forms per consentire agli autori di migliorare i layout di comunicazione inserendo immagini statiche.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 14%

---


# Oggetto immagine nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

L&#39;oggetto Image nell&#39;Editor comunicazioni interattive consente agli autori di migliorare i layout di comunicazione inserendo immagini statiche. Questo componente è essenziale per creare layout accattivanti e incorporare elementi di branding come logo o icone visive. Gli autori possono inserirlo sia nelle pagine master che nella visualizzazione progettazione per garantire un aspetto coerente tra i vari formati di output, ad esempio PDF.

![Trova documento IC](/help/forms/interactive-communication/assets/image.png)

## 2.Properties

L&#39;oggetto Image fornisce diverse proprietà per consentirne la configurazione dell&#39;aspetto e del comportamento.

2.1. Descrizione dell’immagine

Nome:
Funge da identificatore univoco per il componente immagine, consentendo un facile riferimento all’interno della gerarchia dei componenti o dell’editor di regole.

Seleziona immagine: consente all’autore di caricare o fare riferimento a un’immagine, ad esempio un logo, un’icona o qualsiasi altra immagine statica proveniente da più sorgenti.


2.2. Posizione

Descrizione: controlla il posizionamento spaziale dell’immagine nel layout.

Impostazioni:

Coordinate X e Y

Altezza e larghezza (in mm)

2.3 Margine

Definire la spaziatura attorno alla casella di testo:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.4. Aspetto

Aspetto: definisce lo stile visivo del campo immagine, scegli predefiniti come Bordato, Piatto o Elevato e personalizza con il colore di riempimento, lo spessore del tratto e lo stile degli angoli (arrotondati o nitidi).

2.5. Presenza

Descrizione: determina la visibilità dell’oggetto immagine in fase di esecuzione.

- Opzioni:

   - Visibile

   - Nascosto (mantiene spazio)

## 3.Usage

L&#39;oggetto Image è ideale per:

- Inserimento di logo nelle intestazioni di documento

- Visualizzazione delle immagini dei prodotti in fatture o preventivi

- Migliorare il coinvolgimento visivo delle comunicazioni

## 4.Best practice

- Utilizza le immagini di una libreria condivisa per un facile riutilizzo e la coerenza.

- Mantenere coerente la forma dell&#39;immagine per evitare la dilatazione o la pixelazione.

- Evitare di utilizzare file immagine di dimensioni molto grandi per mantenere il documento veloce e reattivo.

- Imposta l&#39;immagine in modo che venga mostrata o nascosta in modo condizionale, se non è sempre necessaria.

L’oggetto Immagine nella comunicazione interattiva di AEM svolge un ruolo fondamentale nella creazione di comunicazioni di marchio, personalizzate ed efficaci dal punto di vista visivo. Con proprietà configurabili, migliora l’esperienza utente mantenendo la coerenza del design tra diversi formati.
