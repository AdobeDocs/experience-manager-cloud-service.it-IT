---
title: Componente Sottomodulo nell’editor di comunicazione interattiva
description: Il componente Sottomodulo nell’Editor di comunicazione interattiva in AEM Forms consente di organizzare più elementi del modulo in modo flessibile e strutturato.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 10%

---


# Componente Sottomodulo nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente **Sottomodulo** nell&#39;editor di comunicazione interattiva (IC) funge da contenitore di layout dinamico che consente di organizzare più elementi modulo in modo flessibile e strutturato. Viene comunemente utilizzato per raggruppare campi correlati, creare sezioni ripetute o definire strutture di dati nidificate per migliorare l’esperienza utente e l’associazione dei dati.

Le sottomaschere possono essere configurate per scorrere in layout diversi, ad esempio dall&#39;alto verso il basso o da sinistra a destra, rendendole ideali per le progettazioni di moduli complessi e le sezioni riutilizzabili.

![Trova documento IC](/help/forms/interactive-communication/assets/subform.png)

## &#x200B;2. Proprietà

2.1 Proprietà di base

- **Nome:** Identificatore univoco per il sottomodulo utilizzato nei riferimenti, nei modelli di dati e nelle regole business.

- **Contenuto:** Definisce la disposizione degli elementi all&#39;interno del sottomodulo.

   - **Posizionato:** Posizionamento assoluto degli elementi figlio utilizzando le coordinate X e Y.

   - **Con flusso (dall&#39;alto verso il basso):** Dispone gli elementi verticalmente.

   - **Con flusso (da sinistra a destra):** Dispone gli elementi orizzontalmente.

2.2 Posizione

- **Descrizione:** Determina la posizione del sottomodulo all&#39;interno del layout di comunicazione.

- **Impostazioni:**

   - Coordinate X e Y (in mm)

   - Larghezza e altezza (in mm)

2.3 Aspetto

- **Riempimento:** Specifica il colore di sfondo dell&#39;area del sottomodulo.

- **Tratto:** Definisce il colore del bordo.

- **Larghezza:** Imposta lo spessore del bordo.

- **Stile:** scegliere tra predefiniti visivi quali piatto, con bordi o con privilegi elevati.

- **Spigoli:** Determina lo stile degli angoli, arrotondato o tagliente.

2.4 Presenza

- **Descrizione:** Controlla la visibilità del sottomodulo durante il runtime.

- **Opzioni:**

   - **Visibile:** sempre visualizzato.

   - **Nascosto:** non visualizzato, ma lo spazio viene mantenuto nel layout.

2.5 Associazione dei dati

- **Tipo di associazione dati:** collega il sottomodulo a una struttura di dati (in genere XML o JSON).

- **Nome utente:** associa i dati utilizzando il nome assegnato della sottomaschera.

- **Usa dati globali:** collega il sottomodulo a un percorso schema globale per l&#39;utilizzo dei dati condivisi.

- **Nessuna associazione dati:** Il sottomodulo non memorizza o non interagisce con alcun modello dati esterno.

## &#x200B;3. Utilizzo

Le sottomaschere sono fondamentali in scenari che richiedono raggruppamenti, nidificazioni o set di campi ripetuti. Le applicazioni tipiche includono:

- Organizzazione dei blocchi di indirizzi (ad esempio, Via, Città, CAP)

- Sezioni ripetute per voci di riga o più voci

- Strutturare la logica dei moduli condizionali utilizzando visibilità e regole
Le sottomaschere possono essere utilizzate anche come contenitori per l&#39;allineamento della progettazione mediante trascinamento della selezione nei layout statici e dinamici.

## &#x200B;4. Best practice

- Scegli il layout giusto (fluido o posizionato) in base al design e alle esigenze di dati.

- Utilizza nomi significativi per semplificare l’integrazione dei dati e il riferimento alle regole.

- Applicare uno stile alle sottomaschere per distinguere visivamente le sezioni raggruppate.

- Quando si utilizzano sottomaschere ripetute, verificare che l&#39;associazione dei dati alle strutture di array sia corretta.

- Applicare regole di visibilità condizionale per ottimizzare l’esperienza utente nei moduli complessi.

Il componente **Sottomodulo** nell&#39;editor di comunicazioni interattive consente di strutturare e controllare layout di moduli complessi. Organizzando i campi di input, gestendo il contenuto dinamico o abilitando la progettazione modulare, le sottomaschere migliorano sia l&#39;usabilità che la gestibilità tra i modelli di documento.


