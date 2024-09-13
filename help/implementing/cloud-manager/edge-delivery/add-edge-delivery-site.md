---
title: Aggiungere un sito Edge Delivery a Cloud Manager
description: Scopri come aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


## Aggiungere un sito Edge Delivery a Cloud Manager {#eds-add-site}

Dopo aver aggiunto i Edge Delivery Services a un programma di produzione, viene applicata la licenza per i Edge Delivery Services.

Nella pagina Panoramica viene visualizzata una scheda selezionabile denominata **Edge Delivery**. Facendo clic sulla scheda viene visualizzata una tabella in cui sono elencati tutti i siti Edge Delivery aggiunti. Nel pannello di navigazione a sinistra, nel raggruppamento **Servizi**, noterai l&#39;opzione di menu denominata **Siti Edge Delivery**.

![Pagina Panoramica che mostra i siti Edge Delivery nel pannello di navigazione a sinistra e la scheda Edge Delivery a destra della scheda Consegna Publish](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Per aggiungere un sito Edge Delivery a Cloud Manager:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito Edge Delivery.
1. Effettuare una delle seguenti operazioni:
   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Quindi, nell&#39;angolo inferiore destro della pagina, fare clic su **Aggiungi sito Edge Delivery**.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     L&#39;**elenco attività di Edge Delivery**, come illustrato nell&#39;immagine precedente, è una guida opzionale all&#39;onboarding che ti aiuta a iniziare a utilizzare Edge Delivery. Consulta [Informazioni sull&#39;elenco attività di Edge Delivery](#ed-todo-list).

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**. Fai clic su **Aggiungi sito** nell&#39;angolo superiore destro della pagina.

     ![Aggiungi sito Edge Delivery dal pulsante Siti Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Nella finestra di dialogo **Aggiungi sito Edge Delivery** eseguire le operazioni seguenti:

   | Campo di testo | Cosa fare |
   | --- | --- |
   | Nome sito | Immetti il nome del sito Edge Delivery che stai aggiungendo. Il nome funge da identificatore univoco del sito all’interno di Cloud Manager. |
   | URL archivio | Questo campo si riferisce all’archivio Git in cui è memorizzato il codice del sito web.<br>Immetti l&#39;URL dell&#39;archivio Git che contiene i file e le risorse necessarie (ad esempio HTML, CSS, JavaScript e altre risorse Web) per il tuo sito Edge Delivery. Questa disposizione consente a Cloud Manager di estrarre il codice da tale archivio durante il processo di distribuzione. |
   | Descrizione sito (facoltativa) | Immetti una breve descrizione del sito Edge Delivery che stai aggiungendo.<br>Questa descrizione consente di identificare e differenziare il sito, semplificandone la gestione e il riconoscimento tra gli altri siti aggiunti. È possibile includere dettagli sullo scopo del sito, sul contenuto o su qualsiasi altra informazione rilevante che possa aiutare a chiarirne la funzione o l’ambito. |

1. Nell&#39;angolo inferiore destro della finestra di dialogo fare clic su **Aggiungi**.

1. Nella finestra di dialogo **Verifica proprietà repository** eseguire una delle operazioni seguenti:

   | Passaggio | Descrizione |
   | --- | --- |
   | 1 | Aggiungere un file con il percorso al ramo `main` dell&#39;archivio Git elencato nel campo **URL archivio**. Se necessario, fate clic sull&#39;icona Copia per copiare il percorso negli Appunti.<br> Percorso: <br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>Non *aggiungere* un punto all&#39;inizio del percorso, in:<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | Aggiungi il codice generato al file creato nel passaggio 1. Se necessario, fai clic sull’icona Copia per copiare il codice negli Appunti. |
   | 3 | Nell’archivio Git, crea una richiesta di pull, quindi uniscila per eseguire il commit del codice. |

1. Fare clic su **Verifica**. Dopo la verifica dell’archivio, il suo stato nella tabella Edge Deliver Sites cambia in un cerchio verde con un segno di spunta bianco all’interno.
