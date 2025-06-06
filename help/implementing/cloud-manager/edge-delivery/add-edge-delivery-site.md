---
title: Aggiungere un sito Edge Delivery a Cloud Manager
description: Scopri come aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: e99bec4515c79e181ce38b94b1ea327fd99d2695
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 83%

---

# Aggiungere un sito Edge Delivery a Cloud Manager {#adding}

>[!IMPORTANT]
>
>Scopri perché devi effettuare l’onboarding del tuo sito Edge Delivery Services in Cloud Manager.
>>Consulta [Vantaggi dell’utilizzo del percorso consigliato da Adobe per Edge Delivery Services](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#recommended-path-eds).

**Per aggiungere un sito Edge Delivery a Cloud Manager:**

1. Prima di iniziare a utilizzare un sito Edge Delivery in Cloud Manager, assicurati di aver creato il programma con una licenza Edge Delivery Services.
Consulta [Creare un programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).
1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Effettua una delle seguenti operazioni:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Quindi, nell’angolo inferiore a destra della pagina, fai clic su **Aggiungi sito Edge Delivery**.

     ![Aggiungere un sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * Nell’angolo superiore a sinistra della pagina fai clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu sul lato sinistro.
Nell’intestazione **Servizi** fai clic sull’![icona Pagina Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.
Fai clic su **Aggiungi sito** nell’angolo superiore a destra della pagina.

     ![Aggiungere un sito Edge Delivery dal pulsante Edge Delivery Sites](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Nella finestra di dialogo **Aggiungi sito Edge Delivery**, fornisci le seguenti informazioni nei campi obbligatori:

   | Campo testo | Descrizione |
   | - | --- |
   | Nome sito | Immetti il nome del sito Edge Delivery che stai aggiungendo.<br>Il nome funge da identificatore univoco per il sito in Cloud Manager. |
   | Origine Edge Delivery | Questo valore specifica il percorso URL dell&#39;origine di contenuto per il sito in Edge Delivery Services. Collega inoltre Cloud Manager al tuo sito live.<br>L&#39;URL include in genere *branch*, *project* e *tenant*, come nell&#39;esempio seguente (solo a scopo illustrativo):<br>`https://main--{site}--{org}.aem.live` |
   | Descrizione sito (facoltativa) | Immetti una breve descrizione del sito Edge Delivery che stai aggiungendo.<br>Una descrizione consente di identificare e differenziare il sito, semplificandone la gestione e il riconoscimento tra gli altri siti aggiunti. |

1. Nell’angolo inferiore a destra della finestra di dialogo, fai clic su **Aggiungi**.

1. Nella finestra di dialogo **Verifica proprietà dell’archivio**, controlla la proprietà del repository eseguendo la procedura seguente:

   | Numero passaggio | Descrizione |
   | - | - |
   | **1** | Aggiungi un file con percorso e nome `well-known/adobe/cloudmanager-challenge.txt` al ramo `main` dell’archivio Git elencato nel campo **URL archivio**. *Non* aggiungere un punto all’inizio del percorso.<br>Se necessario, fai clic sull’![icona Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il percorso negli Appunti. |
   | **2** | Aggiungi il codice visualizzato nel campo di testo del passaggio 2 al file appena creato nel passaggio 1.<br>Se necessario, fai clic sull’![icona Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il codice negli Appunti. |
   | **3** | Crea una richiesta di pull nell’archivio Git per le modifiche appena create, quindi uniscila in `main` per eseguire il commit del codice. |

1. Fai clic su **Verifica**.

Una volta verificato l’archivio, il relativo stato viene aggiornato nella tabella dei siti Edge Delivery. Un cerchio verde con un segno di spunta bianco all’interno indica lo stato.

Nella stessa tabella fai clic sull’![icona Informazioni sul sito Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) per visualizzarne i dettagli. Queste informazioni includono l’URL dell’archivio verificato, insieme agli URL del sito web di anteprima e produzione.
