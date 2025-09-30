---
title: Creare un frammento di comunicazione interattiva
description: Crea frammenti di comunicazione interattiva in AEM Forms per creare blocchi di contenuto modulari e riutilizzabili che garantiscano coerenza, risparmio di tempo e supporto di comunicazioni personalizzate basate su dati.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 9%

---


# Associazione dati nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

L’associazione dati nell’editor di comunicazioni interattive collega i campi su tela con un livello di dati gestito in modo che le comunicazioni vengano riprodotte con informazioni reali e contestuali. Collegando i componenti a un Form Data Model (FDM) o a un payload globale, gli autori possono garantire precisione, ridurre il lavoro manuale e fornire esperienze dinamiche e personalizzate.

Oltre alla semplice connessione dei valori, l’associazione dati in IC supporta la mappatura visiva, la precompilazione e la sincronizzazione, consentendo agli autori di progettare in modo più rapido mantenendo l’allineamento con i sistemi back-end e i modelli di dati.

## &#x200B;2. Proprietà

2.1 Gestione delle connessioni dati (FDM)

- **Selezione di FDM:** Scegliere il modello dati del modulo appropriato (ad esempio, clienti, account o criteri). Questo stabilisce lo schema autorevole per campi, array e oggetti utilizzati nella comunicazione.

- **Creazione di associazioni dati:** una volta abilitate le associazioni, ogni campo può essere associato ai percorsi FDM, riducendo al minimo gli errori e garantendo un&#39;integrazione coerente.

- **Associazione di campi ai modelli dati:** Posiziona i campi su nodi specifici (ad esempio, customer.name, policy.holder.id) per indirizzare il rendering con dati live e supportare le convalide o la logica condizionale.

2.2 Creazione di associazioni di dati

- **Mappatura visiva:** La mappatura mediante trascinamento tra campi e nodi FDM consente agli utenti non tecnici di evitare errori.

- **Associazione campo:** Definire il percorso di destinazione, il tipo di dati (testo, numero, data, booleano, immagine) e i formati facoltativi (ad esempio, maschera data, valuta).

- **Anteprima binding:** verifica le associazioni con set di dati di esempio per convalidare la formattazione e la correttezza prima della pubblicazione.

2.3 Associazione dei campi ai modelli di dati

- **Mappatura campi:** Collega testo, immagine o strutture ripetute (tabelle/elenchi) con i nodi FDM corretti. Le raccolte possono utilizzare origini di iterazione e righe di modello.

- **Sincronizzazione dati:** scegliere unidirezionale (interfaccia utente popolata dal modello) o bidirezionale (input utente salvati nuovamente nel modello).

- **Precompilazione:** Utilizza i valori predefiniti del modello o delle espressioni per semplificare l&#39;immissione dei dati e migliorare la precisione.

## &#x200B;3. Utilizzo

L’associazione dati viene comunemente utilizzata quando le comunicazioni devono visualizzare record autorevoli o acquisire gli input degli utenti. Alcuni esempi:

- **Personalization:** Popola i dettagli del cliente come nome, indirizzo o saldo del conto.

- **Contenuto condizionale:** mostra/nascondi le sezioni in base ai valori del modello (ad esempio, clienti attivi e inattivi).

- **Raccolte e tabelle:** Eseguire il rendering di cronologie, transazioni o elenchi dettagliati da array.

- **Immagini e file multimediali:** associare foto del profilo, logo aziendali o immagini di prodotti.

- **Rivedi e firma elettronica:** precompila i moduli con i dati e consenti aggiornamenti tramite sincronizzazione bidirezionale.

In genere, gli autori selezionano l’FDM nelle prime fasi del progetto, mappano visivamente i campi durante la progettazione e testano i dati di esempio prima di pubblicarli.

## &#x200B;4. Best practice

- **Definisci lo schema in anticipo:** Finalizza FDM prima dell&#39;associazione per evitare di ripetere il mapping in un secondo momento.

- **Utilizza la mappatura visiva:** Per evitare errori di battitura e percorsi non corrispondenti, utilizza il trascinamento della selezione.

- **Convalida tipi di dati:** Applica formattatori per valuta, date o numeri di telefono per garantire la coerenza.

- **Mantieni le associazioni esplicite:** Ogni campo deve essere mappato chiaramente su un singolo nodo di dati.

- **Test con dati di esempio:** Anteprima di casi comuni e perimetrali (ad esempio, valori vuoti, matrici lunghe).

- **Limita sincronizzazione bidirezionale:** Utilizzare solo quando sono necessarie modifiche o approvazioni.

- **Modulare raccolte:** Utilizzare righe modello per strutture ripetibili.

- **Proteggi dati sensibili:** Applica il mascheramento, la crittografia e l&#39;accesso con privilegi minimi per i dati PII o di pagamento.

Configurando con attenzione l’associazione dati, gli autori creano un ponte affidabile tra la progettazione e i dati, accelerando l’authoring delle comunicazioni, garantendo accuratezza e offrendo esperienze altamente personalizzate su larga scala.