---
title: Creare regole nell’editor di comunicazione interattiva
description: Creare regole nell’Editor comunicazioni interattive consente agli autori di definire comportamenti dinamici che rendono le comunicazioni interattive e intelligenti.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: b2b85d1e802c7f287b875d53a9347ca07ea2b806
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 10%

---


# Editor regole nell’Editor comunicazioni interattive


>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.


>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.


## &#x200B;1. Introduzione


L’editor di regole nell’editor di comunicazioni interattive consente agli autori di definire comportamenti dinamici che rendono le comunicazioni interattive e intelligenti. Le regole controllano il comportamento, la visualizzazione o il calcolo dei campi in base alle azioni degli utenti o ai dati sottostanti, garantendo che ogni comunicazione sia personalizzata e in base al contesto.


Dalle semplici impostazioni di visibilità alla logica condizionale complessa, le regole consentono agli autori di fornire esperienze in grado di adattarsi in tempo reale, migliorando l’usabilità, la precisione e il coinvolgimento.


![Trova documento IC](/help/forms/interactive-communication/assets/rule-creation.png)


## &#x200B;2. Proprietà


2.1 Impostazione delle proprietà e dei comportamenti dei campi


- **Tipi di input:** Definire il tipo di dati accettati da un campo, ad esempio testo, numeri, date o valori booleani, garantendo la corretta convalida e formattazione.


- **Regole di visibilità:** Controlla se un campo è visibile, nascosto o visualizzato dinamicamente in base alle condizioni (ad esempio, &quot;Mostra campo sconto solo se è applicato il codice promozionale&quot;).


- **Valori predefiniti:** Predefinisci i valori nei campi (ad esempio, data odierna, nome cliente da modello dati) per risparmiare tempo e migliorare la precisione.


2.2 Implementare calcoli, convalide e logica delle regole


- **Logica campo:** automatizza i calcoli e le relazioni tra i campi, ad esempio calcolando gli importi delle fatture o compilando automaticamente i campi dipendenti.


- **Regole personalizzate:** Crea una logica avanzata utilizzando l&#39;Editor regole per scenari complessi come i controlli di idoneità o i prezzi basati su livelli.


- **Azioni condizionali:** Definisci i trigger che rispondono ai valori di input o dati dell&#39;utente, ad esempio l&#39;attivazione/disattivazione di campi, la visualizzazione di messaggi o la diramazione in sezioni diverse.


![Trova documento IC](/help/forms/interactive-communication/assets/rule-creation1.png)


## &#x200B;3. Utilizzo


L’editor di regole è ampiamente utilizzato per garantire che i moduli e le comunicazioni siano reattivi e basati sul contesto:


- **Visualizzazione dinamica:** nascondere o visualizzare sezioni in base al tipo di cliente o alle opzioni selezionate.


- **Convalida:** Per evitare errori, controllare formati, intervalli o input obbligatori.


- **Calcoli automatici:** semplifica le attività dell&#39;utente con le formule (ad esempio, imposte, totali o sconti).


- **Controllo flusso di lavoro:** Abilita pulsanti, campi o azioni specifici solo quando vengono soddisfatti i prerequisiti.


- **Personalization:** adatta la comunicazione al profilo, alle preferenze o ai criteri di idoneità del destinatario.


## &#x200B;4. Best practice


- **Regole semplici:** Suddividere la logica complessa in regole modulari più piccole per semplificare la manutenzione.


- **Assegna priorità alla logica di visibilità:** Nascondi in anticipo i campi non necessari per semplificare l&#39;esperienza utente.


- **Verifica accuratamente:** Visualizza in anteprima le regole con più set di dati per confermare l&#39;accuratezza ed evitare conflitti.


- **Utilizza i valori predefiniti in modo appropriato:** campi precompilati che raramente vengono modificati, ma che offrono flessibilità per le modifiche.


- **Sfruttare le azioni condizionali:** Applicarle per migliorare l&#39;interattività, ma evitare di sopraffare gli utenti.


- **Regole documento:** mantiene un record di logica di business per garantire chiarezza agli sviluppatori e alle parti interessate.


Configurando le regole in modo accurato, gli autori possono creare comunicazioni che rispondono in modo intelligente ai dati e alle azioni degli utenti, semplificando i processi, riducendo gli errori e offrendo un’esperienza fluida e personalizzata.



