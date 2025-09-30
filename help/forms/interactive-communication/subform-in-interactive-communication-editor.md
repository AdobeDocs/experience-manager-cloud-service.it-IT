---
title: Sottomodulo nell’editor di comunicazione interattiva
description: Subform in Interactive Communication Editor gestisce i layout, controlla il posizionamento degli oggetti e definisce il modo in cui il contenuto scorre tra le pagine.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 10%

---


# Sottomodulo nell’editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

Un sottomodulo nell’Editor comunicazioni interattive è un oggetto contenitore utilizzato per raggruppare campi, oggetti e componenti in una sezione logica. Consente di gestire i layout, controllare il posizionamento degli oggetti e definire il modo in cui il contenuto scorre tra le pagine. Le sottomaschere sono essenziali per la creazione di comunicazioni strutturate, riutilizzabili e reattive, soprattutto quando si tratta di contenuti dinamici o ripetuti.

Utilizzando le sottomaschere, gli autori possono mantenere la coerenza, gestire l’impaginazione e associare intere sezioni a origini dati strutturate.

## &#x200B;2. Proprietà

2.1 Layout struttura modulo

- **Layout fisso:** Gli oggetti mantengono le posizioni esatte sulla pagina. Consigliato per progetti statici in cui è richiesto il posizionamento di precisione (ad esempio fatture o lettere ufficiali).

- **Layout fluido:** Gli oggetti vengono regolati dinamicamente in base alla lunghezza del contenuto e alla dimensione dello schermo. Adatto per comunicazioni che richiedono una progettazione reattiva o lunghezze di dati variabili.

2.2 Posizionamento del sottomodulo

- **Paginazione:** Controlla il modo in cui le sottomaschere si suddividono tra le pagine. Le opzioni includono il mantenimento delle sottomaschere o l’autorizzazione di interruzioni di pagina al loro interno.

- **Posizione:** Specificare se la sottomaschera viene posizionata rispetto al relativo contenitore padre o se scorre naturalmente all&#39;interno del layout.

- **Aspetto:** Per separare visivamente il contenuto, definire sfondo, bordi e stile per il sottomodulo.

- **Presenza:** Configura le impostazioni di visibilità (Visibile, Nascosto o Condizionale) in base alle regole business o ai valori dei dati.

2.3 Associazione dei dati

- Le sottomaschere possono essere associate direttamente ai nodi o agli array **Form Data Model (FDM)**.

- L&#39;associazione consente di ripetere dinamicamente la sottomaschera per ogni record di una raccolta, ad esempio più criteri, transazioni o indirizzi.

- Supporta sia la popolazione statica che dinamica dei contenuti in base alla struttura dei dati.

## &#x200B;3. Utilizzo

I sottomoduli sono ampiamente utilizzati per:

- Strutturazione dei documenti in sezioni quali intestazione, corpo e piè di pagina.

- Contenuto ripetuto come tabelle, distinte dettagliate o elenchi di criteri.

- Gestione dell’impaginazione in modo che il contenuto raggruppato rimanga unito.

- Visualizzazione condizionale delle sezioni in base a regole o valori di dati.

- Applicazione del controllo layout (fisso o fluido) a seconda del tipo di comunicazione.

Gli autori possono trascinare un sottomodulo dalla libreria di oggetti nell&#39;area di lavoro e regolarne il layout, il posizionamento e l&#39;associazione dal pannello Proprietà.

## &#x200B;4. Best practice

- **Scegliere il layout in modo appropriato:** Utilizzare il layout fisso per i moduli che richiedono il posizionamento esatto e il layout scorrevole per le comunicazioni dinamiche basate sui dati.

- **Associare le raccolte con attenzione:** Per elenchi o matrici, associare i sottomoduli direttamente alle raccolte FDM con righe modello.

- **Ottimizza impaginazione:** Per evitare interruzioni impreviste, raggruppare oggetti correlati in un sottomodulo.

- **Usa presenza condizionale:** Nascondere o visualizzare le sottomaschere in modo dinamico in base ai valori dei dati.

- **Gestisci gerarchia:** annidare i sottomaschere in modo logico per semplificare la gestione dei layout complessi.

- **Verifica con dati variabili:** Anteprima con set di dati brevi, lunghi e vuoti per garantire che la progettazione si adatti correttamente.

Sfruttando in modo efficace i sottomoduli, gli autori possono ottenere layout più puliti, un migliore controllo dei contenuti dinamici e garantire che le comunicazioni si adattino perfettamente a scenari statici e basati sui dati.
