---
title: Importare ed esportare comunicazioni interattive
description: Importazione ed esportazione di comunicazioni interattive consente agli utenti di migrare, riutilizzare e gestire in modo semplice le comunicazioni tra ambienti diversi.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 14%

---


# Importare ed esportare comunicazioni interattive

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

La funzione di importazione ed esportazione di Interactive Communication (IC) consente agli utenti di migrare, riutilizzare e gestire senza problemi le comunicazioni tra ambienti diversi. Consente di esportare una comunicazione interattiva (IC) insieme ai frammenti e ai modelli di dati associati da un ambiente e di importarla in un altro, garantendo coerenza e riducendo la duplicazione delle attività durante la distribuzione.

## Vantaggi principali

- Semplifica la migrazione di IC tra ambienti diversi.
- Mantiene frammenti, modelli di dati e dipendenze.
- Riduce gli sforzi nella ricreazione di IC tra progetti.

## Importare ed esportare comunicazioni interattive

Creare una comunicazione interattiva (IC) in un ambiente e riutilizzarla in un altro esportandola e importandola seguendo la procedura riportata di seguito:

+++&#x200B;1. Come esportare la comunicazione interattiva

1.1. Selezionare una [comunicazione interattiva creata](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) (IC).
1.2. Fai clic sull&#39;opzione **Scarica** per esportarla come file ZIP.
1.3. Il file ZIP scaricato include l&#39;IC insieme al relativo **modello**, **frammenti** e **modello dati** selezionato.

![Trova documento IC](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++&#x200B;2. Importare la comunicazione interattiva

2.1. Passare all&#39;ambiente di destinazione.
2.2. Passa a **Forms > Forms e documenti > Crea > Caricamento file**.
2.3. Carica il file ZIP in **importa** l&#39;IC.

![Trova documento IC](/help/forms/interactive-communication/assets/uploadfile.png)

2.4. Dopo il caricamento, il componente di interoperabilità viene visualizzato insieme ai frammenti e al modello di dati associati.

![Trova documento IC](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++&#x200B;3. Importazione ed esportazione di frammenti

3.1. Per esportare, seleziona il frammento richiesto da **Forms > Forms and Documents**, quindi fai clic su **Scarica** per esportarlo come file ZIP.

3.2. Per importare, vai all&#39;ambiente di destinazione, passa a Forms > Forms and Documents > Create > **File Upload** e carica il file ZIP esportato.

Ciò consente di riutilizzare facilmente i frammenti in ambienti diversi, garantendo la coerenza del progetto e riducendo la duplicazione delle attività.
+++
