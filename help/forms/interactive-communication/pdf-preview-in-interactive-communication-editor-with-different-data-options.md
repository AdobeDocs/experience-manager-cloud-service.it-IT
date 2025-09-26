---
title: Anteprima PDF nell’Editor di comunicazione interattiva con diverse opzioni di dati
description: Anteprima PDF nell’Editor di comunicazione interattiva con diverse opzioni di dati per visualizzare in anteprima le comunicazioni interattive in tre modi diversi.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 13%

---


# Anteprima PDF nell’Editor di comunicazione interattiva

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

La funzione di anteprima di PDF consente agli utenti di visualizzare in anteprima le comunicazioni interattive in tre modi diversi: senza dati, con dati locali basati su JSON o con dati di esempio dal modello dati configurato.

## Vantaggi principali

- Visualizza un’anteprima delle comunicazioni interattive con dati di esempio per visualizzare come verranno visualizzati i dati live quando vengono uniti alla comunicazione.

- Carica i file di dati JSON locali per generare anteprime basate su dati senza configurazione del back-end.

- Utilizza i modelli di dati dei moduli collegati (FDM) per simulare l’integrazione di dati in tempo reale con dati di esempio durante la progettazione.

- Passa facilmente da un’opzione all’altra (nessun dato, dati locali, FDM) per convalidare layout, struttura e personalizzazione.

## Anteprima PDF nell’Editor di comunicazione interattiva con diverse opzioni di dati

Visualizza in anteprima le comunicazioni interattive senza dati, dati locali o dati di esempio dal modello dati configurato per test e convalida flessibili.

+++&#x200B;1. Anteprima senza dati.

1.1. Aprire la comunicazione interattiva nell&#39;editor IC.

1.2. Utilizzare l&#39;opzione Anteprima PDF e selezionare l&#39;opzione **Nessun dato** per visualizzare una comunicazione senza dati.

![Trova documento IC](/help/forms/interactive-communication/assets/nodata.png)

+++

+++&#x200B;2. Anteprima con dati JSON locali

2.1. Preparare un file JSON strutturato. Per riferimento, è possibile copiare i dati di esempio dallo schema JSON [(FDM)](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model) utilizzato per la comunicazione.

2.2. Nell&#39;editor IC, passare a **Anteprima PDF** > Utilizzo dei dati locali.

2.3. Seleziona e carica il file JSON per eseguire il rendering di un’anteprima PDF con i dati forniti.

![Trova documento IC](/help/forms/interactive-communication/assets/localdata.png)

+++

+++&#x200B;3. Anteprima con modello dati 

3.1. Selezionare **Utilizzo del modello dati** per utilizzare dati di esempio da un modello dati modulo (FDM) già configurato dell&#39;IC.

3.2. L’anteprima compila automaticamente i dati dai campi del modello. Assicurati che i dati di esempio vengano salvati in FDM al primo utilizzo, altrimenti l’anteprima potrebbe non essere visualizzata come dati.

![Trova documento IC](/help/forms/interactive-communication/assets/datamodel.png)

+++

