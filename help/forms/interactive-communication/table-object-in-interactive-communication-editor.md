---
title: Oggetto Table nell’editor di comunicazione interattiva
description: L’oggetto tabella nell’Editor di comunicazione interattiva di AEM Forms consente agli autori di inserire facilmente tabelle personalizzabili nei modelli di comunicazione.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 8%

---


# Oggetto Table nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

L’oggetto Table nell’editor di comunicazione interattiva (IC) consente agli autori di inserire facilmente tabelle personalizzabili nei modelli di comunicazione. Questo oggetto supporta la rappresentazione dei dati tabulari per casi d’uso quali riepiloghi, elenchi di elementi, input strutturati o layout di confronto.

Gli autori possono trascinare e rilasciare il componente tabella nell’area di lavoro, configurare il numero di righe e colonne e scegliere opzioni quali l’inclusione di righe di intestazione e piè di pagina o l’impostazione della direzione del layout. Le tabelle possono essere definite come modelli predefiniti per la coerenza tra più comunicazioni.

![Trova documento IC](/help/forms/interactive-communication/assets/table.png)

## &#x200B;2. Proprietà

L&#39;oggetto Table include diverse proprietà configurabili che consentono agli autori di personalizzare il comportamento e l&#39;aspetto della tabella:


2.1 Campo di base

- **Nome:** Identificatore univoco per la tabella. Questo nome viene utilizzato internamente per fare riferimento alla tabella nei modelli di dati e nella logica.

- **Righe:** Specifica il numero di righe di contenuto (escluse intestazione e piè di pagina).

- **Colonne:** Definisce il numero di colonne nella tabella.

- **Riga intestazione:** Opzione per includere una riga di intestazione nella parte superiore della tabella per le etichette di colonna.

- **Riga piè di pagina:** Opzione per includere una riga piè di pagina per i totali o i valori di riepilogo.

- **Imposta come predefinito:** Consente agli utenti di salvare la configurazione corrente come modello di tabella predefinito per utilizzi futuri.

- **Direzione layout:** definisce il modo in cui vengono compilate le righe, in genere impostate da sinistra a destra.

2.2 Posizione

- **Descrizione:** controlla la posizione della tabella all&#39;interno del layout.

- **Impostazioni:**

   - **Coordinate X e Y:** Imposta le posizioni orizzontale (X) e verticale (Y) della tabella nell&#39;area di lavoro.

   - **Altezza e larghezza:** Definisce le dimensioni complessive della tabella (in mm), consentendo l&#39;allocazione flessibile dello spazio.

2.3 Aspetto

**Aspetto:** Imposta lo stile visivo della tabella. Gli autori possono scegliere tra predefiniti predefiniti predefiniti quali Bordi, Piatti o Elevati.

- **Riempimento:** Colore di sfondo della tabella o delle celle.

- **Tratto:** Colore del bordo attorno alla tabella o a celle specifiche.

- **Larghezza:** spessore delle linee del bordo.

- **Stile:** Scegliere i tipi di spigolo, ovvero gli angoli arrotondati o gli angoli vivi.

- **Spigoli:** Configura la visibilità dei bordi delle celle e del raggio degli angoli.

2.4 Presenza

- **Descrizione:** Determina la visibilità della tabella in fase di esecuzione.

- **Opzioni:**

   - **Visibile:** Visualizza la tabella normalmente nell&#39;output.

   - **Nascosto:** Nascondi la tabella ma lascia spazio nel layout.

2.5 Associazione dei dati

**Associazione dati:** connettere la tabella con un&#39;origine dati (ad esempio, JSON, schema XML) per popolare dinamicamente righe e colonne con valori durante la generazione. Questo è utile per la fatturazione dettagliata, per i record delle transazioni o per gli elenchi di prodotti.

## &#x200B;3. Utilizzo

L&#39;oggetto Table è ideale per la visualizzazione di informazioni strutturate o ripetitive. I casi d’uso tipici includono:

- Fatture e distinte con righe articolo

- Confronti tra criteri o piani

- Riepiloghi dati profilo o conto

- Cataloghi di prodotti o matrici di funzioni

Gli autori possono configurare il numero di righe e colonne, applicare la visibilità condizionale o associare i dati per visualizzare informazioni dinamiche.

## &#x200B;4. Best practice

- Utilizza le righe di intestazione per etichettare chiaramente ogni colonna per migliorarne la leggibilità.

- Applicare le righe del piè di pagina per i totali o le note importanti, se applicabile.

- Sfrutta l’associazione dati per compilare le righe in modo dinamico in base a un input strutturato.

- Mantenete uno stile e una spaziatura coerenti utilizzando le impostazioni relative all&#39;aspetto e ai margini.

- Quando si nasconde una tabella, è necessario garantire la continuità del layout scegliendo se mantenere o meno lo spazio.

- Utilizzare i modelli predefiniti per standardizzare il contenuto tabulare tra i documenti.

L’oggetto tabella nell’editor IC è un componente flessibile e semplice da usare, progettato per supportare contenuti strutturati nelle comunicazioni. Grazie alle opzioni di layout personalizzabili, alle funzioni di stile e alla potente associazione dei dati, consente agli autori di presentare le informazioni in modo chiaro ed efficace.


