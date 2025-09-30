---
title: Oggetto Casella di testo nell’Editor di comunicazione interattiva
description: L’oggetto Casella di testo nell’Editor di comunicazione interattiva in AEM Forms consente agli autori di inserire e visualizzare contenuto di testo all’interno di una comunicazione.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 11%

---


# Oggetto Casella di testo nell’Editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

L&#39;oggetto **Casella di testo** nell&#39;Editor comunicazioni interattive consente agli autori di inserire e visualizzare contenuto di testo all&#39;interno di una comunicazione. È uno dei componenti più fondamentali e ampiamente utilizzati, comunemente utilizzato per raccogliere nomi, commenti, feedback o dati personalizzati durante la progettazione di comunicazioni interattive o frammenti di comunicazione.

La casella di testo supporta **associazione dati**, consentendo agli autori di combinare facilmente contenuti statici e dinamici, ad esempio: ***&quot;Nome utente: @name&quot;***, dove @name è un campo dati associato che viene popolato dinamicamente quando il documento viene salvato come PDF. Inoltre, supporta la formattazione di testo RTF e il posizionamento flessibile per un controllo preciso del layout.

![Trova documento IC](/help/forms/interactive-communication/assets/textbox.png)

## &#x200B;2. Proprietà

L&#39;oggetto casella di testo fornisce un&#39;ampia serie di proprietà che consentono di configurarne l&#39;aspetto e il comportamento.

2.1 Tipografia

**Famiglia di caratteri:** consente di selezionare stili di carattere quali Arial, Helvetica, Times New Roman e così via.

**Convalida font:** È possibile applicare vincoli di input facoltativi per garantire che vengano accettati solo formati di testo, numerici o speciali.

**Allineamento testo:** Le opzioni includono l&#39;allineamento a sinistra, a destra, al centro o giustificato.

**Stile testo:** Abilita la formattazione del testo con le funzioni grassetto, corsivo, barrato e sottolineato.

**Elenchi:** supporta l&#39;inserimento di elenchi ordinati (numerati) e non ordinati (puntati).

2.2 Posizione

**Larghezza e altezza:** Impostare le dimensioni della casella di testo in pixel o in percentuale rispetto al contenitore.

2.3 Margine

Definire la spaziatura attorno alla casella di testo:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.4 Aspetto

- **Riempimento testo:** Personalizza il colore e la trasparenza del testo.

- **Riempimento:** Imposta il colore di sfondo della casella di testo.

- **Tratto:** Aggiungi bordi con personalizzabile:

   - Larghezza (spessore)

   - Stile (tinta unita, tratteggiata, punteggiata)

   - Edge (angoli arrotondati o netti)

2.5 Presenza

**Visibile:** impostazione predefinita; la casella di testo viene visualizzata all&#39;utente.

**Casella di testo nascosta:** inclusa nel modulo ma non visualizzata.



## &#x200B;3. Utilizzo

La casella di testo viene utilizzata per:

- Raccolta di informazioni sui clienti come nomi, commenti o feedback.

- Inserimento di valori alfanumerici.

- Integrazione di messaggi personalizzati utilizzando modelli di dati associati.

- Incorporazione all’interno di frammenti per un utilizzo ripetuto nei documenti.

Gli autori possono trascinare la casella di testo dalla libreria oggetti nella visualizzazione Struttura o nella visualizzazione master e configurarne il comportamento utilizzando il pannello Proprietà.

## &#x200B;4. Best practice

- Associare sempre le caselle di testo a etichette di campo significative per migliorare l&#39;accessibilità.

- Utilizza le convalide di input appropriate per evitare errori di immissione dei dati.

- Assicurati di avere un layout dinamico impostando margini e larghezze relativi ai contenitori principali.

- Evitare stili di carattere eccessivi che potrebbero ostacolare la leggibilità.

Configurando accuratamente le proprietà della casella di testo, gli autori possono creare esperienze di comunicazione interattive, reattive e intuitive nell’Editor di comunicazione interattiva di AEM.
