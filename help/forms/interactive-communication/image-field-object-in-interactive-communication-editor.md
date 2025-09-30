---
title: Oggetto campo immagine nell’editor di comunicazione interattiva
description: Oggetto campo immagine nell’Editor comunicazioni interattive in AEM Forms per consentire agli autori di inserire immagini in un layout di comunicazione.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 10%

---


# Oggetto campo immagine nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente Campo immagine nell’editor di comunicazione interattiva consente agli autori di inserire immagini in un layout di comunicazione. È ideale per casi d’uso come l’identificazione di foto, la verifica di documenti o la convalida visiva, in cui è essenziale mostrare un’immagine all’utente finale.

Supportando formati comuni come **JPEG** e **PNG**, questo componente offre opzioni di configurazione flessibili per definire la modalità di visualizzazione, archiviazione e stile dell&#39;immagine. Gli autori possono anche **assegnare un nome o un&#39;etichetta** al campo immagine, migliorando la chiarezza del layout e l&#39;organizzazione.

![Trova documento IC](/help/forms/interactive-communication/assets/imagefield.png)

## &#x200B;2. Proprietà

L’oggetto Campo immagine include diverse proprietà configurabili:

2.1. Campo di base

- **Nome:** Definisci un identificatore univoco per il campo, utilizzato per fare riferimento a modelli di dati e regole.

- **Didascalia:** Visualizza l&#39;etichetta mostrata agli utenti nell&#39;interfaccia.

- **Seleziona immagine:** Consenti all&#39;autore di caricare un&#39;immagine utilizzando questa proprietà, comunemente utilizzata per loghi, ID o altri elementi visivi.

- **Riserva immagine:** Definisci l&#39;allineamento dell&#39;immagine, a sinistra, a destra, in alto o in basso oppure specifica una **posizione personalizzata** utilizzando unità di misura come millimetri (ad esempio, 20 mm).

2.2. Posizione

Controlla il posizionamento spaziale dell&#39;immagine nel layout.

- Coordinate X e Y

- Altezza e larghezza (in mm)

2.3. Margine

Definire la spaziatura attorno alla casella di testo:

- Superiore (Su)

- Inferiore (giù)

- Sinistra

- Destra

2.4. Aspetto

Aspetto: definisce lo stile visivo del campo immagine, scegli predefiniti come Bordato, Piatto o Elevato e personalizza con il colore di riempimento, lo spessore del tratto e lo stile degli angoli (arrotondati o nitidi).

2.5. Presenza

Determina la visibilità dell&#39;oggetto immagine in fase di runtime.

- Visibile

- Nascosto (mantiene spazio)

2.6. Associazione dei dati

Collega il campo immagine a un’origine dati per recuperare e visualizzare contenuto immagine dinamico all’interno della comunicazione.

**Tipo di associazione dati:** Definisce il modo in cui il campo immagine si connette alla struttura dati o allo schema sottostante.

**Usa nome:** associa il campo immagine utilizzando il nome di campo specificato nel modello di dati o nello schema, consentendo il popolamento dinamico dell&#39;immagine in fase di esecuzione.

**Usa dati globali:** collega il campo immagine ai dati globali condivisi nell&#39;intera comunicazione, garantendo la coerenza del contenuto visivo.

**Nessuna associazione dati:** mantiene il campo disconnesso da qualsiasi dato backend, ideale nei casi in cui viene visualizzata un&#39;immagine statica o quando l&#39;immagine è controllata esclusivamente tramite le impostazioni dell&#39;interfaccia utente.

## &#x200B;3. Utilizzo

Il campo Immagine è utile nei contesti in cui è richiesto l’invio di contenuto visivo. I casi d’uso comuni includono:

- Caricamento bozza ID (passaporto, licenza)

- Invio profilo o foto personali

- Allegare visivamente i documenti di supporto

Gli autori possono inserire il campo all’interno di sottomaschere o contenitori di layout per l’allineamento e utilizzare regole di convalida personalizzate per controllare i tipi e le dimensioni di file accettati.

## &#x200B;4. Best practice

- Utilizza etichette o istruzioni chiare quando richiedi il caricamento delle immagini.

- Limita le dimensioni e i formati dei file tramite la convalida delle prestazioni.

- Assicurati che le immagini di fallback (riserva) siano accessibili.

- Associa il campo a un percorso schema significativo se l’integrazione con il back-end

L’oggetto Campo immagine nell’editor di comunicazione interattivo è un componente versatile che migliora l’interattività dei moduli abilitando il caricamento di contenuti visivi. Progettato con stile, convalida e associazione dati, supporta un’esperienza utente fluida ed efficiente nell’acquisizione dei dati per gli invii basati su immagini.




