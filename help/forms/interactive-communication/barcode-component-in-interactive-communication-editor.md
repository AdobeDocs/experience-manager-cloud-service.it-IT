---
title: Componente Codice a barre nell’editor di comunicazioni interattive
description: Il componente Codice a barre nell’Editor comunicazioni interattive in AEM Forms consente agli autori di rappresentare visivamente i dati codificati all’interno dei modelli di comunicazione.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 7%

---


# Componente Codice a barre nell’editor di comunicazioni interattive

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Il componente Codice a barre nell’editor di comunicazioni interattive consente agli autori di rappresentare visivamente i dati codificati all’interno dei modelli di comunicazione. Questa funzione è particolarmente utile per le applicazioni che richiedono il tracciamento, l’identificazione, la fatturazione o l’automazione. Con il supporto di vari standard di codici a barre come Code 128, QR e altro ancora, questo componente offre opzioni flessibili di stile, posizionamento e associazione dati per soddisfare un’ampia gamma di esigenze aziendali.

Il componente Codice a barre semplifica il processo di creazione di fatture cliente, etichette di spedizione o schede di appartenenza incorporando dati leggibili direttamente nel documento.

![Trova documento IC](/help/forms/interactive-communication/assets/barcode.png)

## &#x200B;2. Proprietà

Il componente Codice a barre viene fornito con un set completo di opzioni configurabili per controllarne il comportamento e l’aspetto:

2.1 Campo di base

**Nome:** Identificatore univoco per il codice a barre. Viene utilizzato per fare riferimento al componente nei modelli di dati e nei set di regole.

**Posizione:** Specifica dove viene visualizzato il testo del codice a barre rispetto al simbolo del codice a barre.

**Opzioni:**

- **Nessuno:** Nasconde il testo.

- **Sopra:** Visualizza il testo sopra il codice a barre.

- **Sotto:** Visualizza il testo sotto il codice a barre.

- **Sopra incorporata:** incorpora il testo all&#39;interno dell&#39;area superiore del codice a barre.

- **Incorporato sotto:** Incorpora il testo all&#39;interno dell&#39;area inferiore del codice a barre.

- **Tipo:** Specifica lo standard del codice a barre (ad esempio, Codice 128, Codice 39, Codice QR e così via).

- **Predefinito:** Valore predefinito che viene visualizzato se non vengono forniti dati.

- **Lunghezza dati:** indica il numero previsto o massimo di caratteri che il codice a barre può contenere.

- **Checksum:** convalida i dati del codice a barre per la precisione.

   - **Opzioni:**

      - **Nessuno:** Nessuna convalida di checksum.

      - **Automatico:** calcola automaticamente il checksum in base al tipo.

- **Rapporto largo/stretto:** Definisce la larghezza relativa delle barre larghe rispetto a quelle strette (utilizzate in alcuni codici a barre 1D).

2.2 Ubicazione

Determina dove viene visualizzato il codice a barre in relazione al contenuto:

- **Nessuno:** Nessun posizionamento aggiuntivo.

- **Sopra:** inserisce il codice a barre sopra il contenuto correlato.

- **Sotto:** inserisce il codice a barre sotto il contenuto.

- **In alto incorporato:** Il codice a barre è incorporato e viene spostato sopra il contenuto.

- **Incorporato sotto:** Incorporato sotto il contenuto.

2.3 Posizione

Definisce la posizione esatta del codice a barre all’interno del layout:

- **Coordinate X e Y:** Posizionare il codice a barre all&#39;interno del modulo utilizzando unità di millimetro.

- **Altezza e larghezza:** Impostare le dimensioni fisiche del codice a barre.

2.4 Margine

Aggiunge una spaziatura attorno al codice a barre per una migliore separazione visiva:

- In alto

- In basso

- Sinistra

- Destra

Questi margini facilitano la coerenza del layout e la leggibilità.

2.5 Aspetto

Personalizzare lo stile visivo del codice a barre:

- **Riempimento:** Colore di sfondo dell&#39;area del codice a barre.

- **Tratto:** Colore bordo.

- **Larghezza:** Definisce lo spessore delle righe del codice a barre.

- **Stile:** scegliere tra predefiniti quali piatto, con bordi o con privilegi elevati.

- **Spigoli:** Consente di scegliere tra angoli arrotondati o spigoli vivi per la casella del codice a barre.

2.6 Presenza

Controlla se il codice a barre viene visualizzato o nascosto in fase di runtime:

- **Visibile:** Il codice a barre è visualizzato nell&#39;output finale.

- **Nascosto:** lo spazio è riservato ma il codice a barre non viene visualizzato.

2.7 Associazione dei dati

Associazione dati: connette il codice a barre a un modello di dati back-end (XML o JSON). In questo modo il codice a barre riflette dinamicamente dati univoci per istanza di documento, ad esempio un ID ordine o un numero di tracciamento.

## &#x200B;3. Utilizzo

Il componente Codice a barre è particolarmente utile per automatizzare i processi che si basano su dati digitalizzati. Può essere aggiunto a modelli di comunicazione quali:

- Fatture (per riferimento cliente e pagamenti tramite scansione rapida)

- Etichette di spedizione (per il tracciamento dei pacchetti)

- Iscrizione o schede fedeltà (per l&#39;identificazione basata su scansione)

- Coupon e voucher (per la convalida presso il punto vendita)

Gli autori possono incorporare il codice a barre nei contenitori di layout e assegnarvi uno stile in base al tema del marchio o del documento.

## &#x200B;4. Best practice

- Utilizza un tipo di codice a barre appropriato per il caso d’uso, ad esempio codice QR per gli URL, codice 128 per gli ID alfanumerici.

- Convalidare la leggibilità del codice a barre stampando le versioni dei test e analizzandole.

- Garantire l&#39;integrità dei dati utilizzando l&#39;opzione checksum se lo standard del codice a barre lo supporta.

- Scegli dimensioni leggibili e larghezze delle righe per evitare problemi di scansione.

- Mantenere margini adeguati per impedire il ritaglio durante la stampa.

Il componente Barcode nell&#39;editor di comunicazioni interattive consente ai creatori di documenti di colmare il divario tra i sistemi digitali e fisici. Se implementato in modo efficace, migliora l&#39;automazione, migliora la praticità dell&#39;utente e supporta l&#39;integrazione perfetta con i dispositivi di scansione e i flussi di lavoro.
