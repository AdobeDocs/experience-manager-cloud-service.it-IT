---
title: Oggetto Rectangle nell'editor di comunicazioni interattive
description: L’oggetto Rectangle nell’editor di comunicazioni interattive di AEM Forms consente agli autori di aggiungere elementi grafici a forma di divisore di layout, accenti visivi o contenitori di contenuto.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 12%

---


# Oggetto Rectangle nell&#39;editor di comunicazioni interattive

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente Rettangolo nell’editor di comunicazioni interattive (IC) consente agli autori di aggiungere elementi grafici a forma di divisore di layout, accenti visivi o contenitori di contenuto. I rettangoli migliorano la gerarchia visiva e guidano l’attenzione dell’utente in layout di comunicazione strutturati.
Questo oggetto non è legato ai dati ma è utile per migliorare la chiarezza della progettazione, raggruppare i campi correlati e migliorare la presentazione complessiva.

![Trova documento IC](/help/forms/interactive-communication/assets/rectangle.png)

## &#x200B;2. Proprietà

L&#39;oggetto Rectangle include diverse proprietà personalizzabili:

2.1. Nome

Nome: un identificatore univoco del rettangolo. Utilizzato principalmente per fare riferimento a nelle gerarchie di layout o per applicare gli stili in modo coerente.

2.2. Posizione

- **Descrizione:** Determina la posizione del rettangolo nel layout del documento.

- **Impostazioni:**

   - **Coordinate X e Y:** Definire il posizionamento orizzontale e verticale.

   - **Altezza e larghezza (in mm):** controlla la dimensione del rettangolo.

2.3. Margine

Definisce la spaziatura intorno al componente Rettangolo per separarlo dagli altri elementi dell’interfaccia utente:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.4. Aspetto

- **Descrizione:** gestisce lo stile visivo del rettangolo.

- **Opzioni di personalizzazione:**

   - **Riempimento:** Il colore interno del rettangolo.

   - **Tratto:** Il colore del contorno del rettangolo.

   - **Larghezza tratto:** Spessore del bordo del rettangolo.

   - **Stile:** stili preimpostati come piatto, con bordi o con privilegi elevati.

   - **Spigoli:** Controlla l&#39;aspetto degli angoli (ad esempio, spigoli arrotondati o vivi).

2.5. Presenza

- **Descrizione:** Specifica se il rettangolo viene visualizzato quando viene eseguito il rendering della comunicazione.

- **Opzioni:**

   - **Visibile:** mostra il rettangolo in fase di esecuzione.

   - **Nascosto:** mantiene lo spazio di layout senza visualizzare il rettangolo.

## &#x200B;3. Utilizzo

L&#39;oggetto Rectangle viene in genere utilizzato per scopi di layout e stile anziché per l&#39;input di contenuto. I casi d’uso comuni includono:

- Creazione della separazione visiva tra le sezioni

- Evidenziazione di elementi raggruppati

- Miglioramento della leggibilità e dell&#39;equilibrio visivo

- Intestazioni di frame, piè di pagina o sezioni di chiamata in uscita

I rettangoli possono essere combinati con altri elementi di layout come sottomaschere o contenitori per strutture di progettazione visiva complesse.

## &#x200B;4. Best practice

- Utilizza uno stile coerente per i rettangoli nel layout per garantire armonia visiva.

- Applicare margini e spaziatura adeguati per evitare l&#39;affollamento dei campi adiacenti.

- Scegliere i colori di riempimento e traccia che si allineano al tema del marchio o del documento.

- Utilizza i bordi arrotondati in modo sottile per migliorare l’estetica nei layout dell’interfaccia utente moderni.

- Nascondi i rettangoli se necessari solo a scopo di progettazione durante la modifica ma non necessari nell&#39;output finale.

L&#39;oggetto Rectangle è uno strumento non interattivo ma potente nell&#39;editor IC. Se formattato e posizionato in modo efficace, migliora la precisione del layout, il flusso visivo e l’esperienza utente senza aggiungere complessità all’associazione dati o all’interattività.


