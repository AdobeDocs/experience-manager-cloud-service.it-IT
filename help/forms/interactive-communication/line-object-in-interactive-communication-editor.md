---
title: Oggetto Line nell'editor di comunicazioni interattive
description: L’oggetto linea nell’Editor di comunicazione interattiva di AEM Forms consente agli autori di inserire linee orizzontali o verticali all’interno di un layout di comunicazione.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 11%

---


# Oggetto Line nell&#39;editor di comunicazioni interattive

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## &#x200B;1. Introduzione

L&#39;oggetto Line nell&#39;editor di comunicazione interattiva (IC) consente agli autori di inserire linee orizzontali o verticali all&#39;interno di un layout di comunicazione. Queste linee consentono di segmentare visivamente il contenuto, migliorare la leggibilità o enfatizzare la struttura del modulo. Con stili personalizzabili quali linee solide o sottolineature e posizionamento flessibile, l&#39;oggetto linea può essere utilizzato per scopi sia funzionali che estetici nella progettazione del modulo.

![Trova documento IC](/help/forms/interactive-communication/assets/line.png)

## &#x200B;2. Proprietà

L&#39;oggetto Line viene fornito con una serie di proprietà configurabili per definirne l&#39;identità, l&#39;aspetto, il posizionamento e la visibilità all&#39;interno del documento.

2.1. Campo di base

- **Nome:** Identificatore univoco utilizzato internamente per fare riferimento all&#39;oggetto riga in modelli di dati, regole o script.

- **Tipo di aspetto:** Selezionare la modalità di visualizzazione della riga all&#39;interno del modulo.

   - **Nessuno:** Non viene visualizzata alcuna riga.

   - **Scatola continua:** Esegue il rendering della linea come una casella continua, in genere utilizzata come separatore.

   - **Sottolineatura:** Disegna una sottolineatura in genere utilizzata sotto intestazioni o campi.

2.2. Posizione

- **Descrizione:** definisce la posizione fisica della riga nel layout del modulo.

- **Impostazioni:**

   - **Coordinate X e Y:** Specifica il posizionamento orizzontale e verticale.

   - **Altezza e larghezza:** Impostare la lunghezza e lo spessore della linea (in mm).

2.3. Margine

- **Descrizione:** aggiunge spaziatura o riempimento attorno all&#39;oggetto di linea per controllare la densità del layout.

- **Opzioni:**

   - In alto

   - In basso

   - Sinistra

   - Destra

2.4. Aspetto

- **Descrizione:** consente lo stile della riga in base alla struttura del documento.

- **Opzioni:**

   - **Tratto:** Definisce il colore e lo spessore del tratto di linea.

   - **Larghezza:** Determina la larghezza della riga nel modulo.

   - **Stile:** Scegliere tra stili di linea tratteggiata, punteggiata o continua.

2.5. Presenza

- **Descrizione:** Controlla la visibilità dell&#39;oggetto linea durante il runtime.

- **Opzioni:**

   - **Visibile:** la riga viene rappresentata nell&#39;output finale.

   - **Nascosto:** La riga non viene visualizzata, ma lo spazio di layout è mantenuto.

## &#x200B;3. Utilizzo

L&#39;oggetto Line viene spesso utilizzato per:

- Dividere visivamente le sezioni in una forma lunga

- Sottolinea intestazioni o etichette per evidenziare

- Creare bordi o caselle intorno a gruppi di campi

- Migliorare la gerarchia visiva del layout di comunicazione

## &#x200B;4. Best practice

- Utilizza stili di linea coerenti in tutto il modulo per mantenere un aspetto professionale.

- Regolare i margini per evitare disagi visivi e garantire l&#39;allineamento.

- Scegliete le impostazioni di stile e tratto appropriate per la progettazione del marchio o del documento.

- Nascondere le linee non necessarie per evitare distrazioni e mantenere la spaziatura.

L&#39;oggetto linea nell&#39;editor di comunicazione interattiva è un elemento di progettazione semplice ma potente. Utilizzato strategicamente, migliora la struttura visiva dei documenti di comunicazione, consentendo agli utenti di navigare meglio nei contenuti e garantendo un layout più pulito e raffinato.


