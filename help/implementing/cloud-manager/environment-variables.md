---
title: Variabili dell’ambiente di Cloud Manager
description: Le variabili di ambiente standard possono essere configurate e gestite tramite Cloud Manager e fornite all’ambiente di runtime, da utilizzare nella configurazione OSGi.
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---

# Variabili dell’ambiente di Cloud Manager {#environment-variables}

Le variabili di ambiente standard possono essere configurate e gestite tramite Cloud Manager. Vengono forniti all’ambiente in fase di esecuzione e possono essere utilizzati nelle configurazioni OSGi. Le variabili dell’ambiente possono essere valori specifici dell’ambiente o segreti dell’ambiente in base alle modifiche apportate.

## Panoramica {#overview}

Le variabili di ambiente offrono una serie di vantaggi agli utenti di AEM as a Cloud Service:

* Consentono di variare il comportamento del codice e dell’applicazione in base al contesto e all’ambiente. Ad esempio, possono essere utilizzati per abilitare diverse configurazioni nell’ambiente di sviluppo rispetto agli ambienti di produzione o di stage per evitare costosi errori.
* Devono essere configurati e configurati una sola volta e possono essere aggiornati ed eliminati quando necessario.
* I loro valori possono essere aggiornati in qualsiasi momento ed entrare in vigore immediatamente senza la necessità di alcuna modifica o distribuzione del codice.
* Possono separare il codice dalla configurazione e rimuovere la necessità di includere informazioni sensibili nel controllo delle versioni.
* Migliorano la sicurezza dell&#39;applicazione as a Cloud Service AEM poiché vivono al di fuori del codice.

I casi d’uso tipici per l’utilizzo delle variabili d’ambiente includono:

* Collegamento dell&#39;applicazione AEM con endpoint esterni diversi
* Utilizzo di un riferimento quando si memorizzano le password anziché direttamente nella base di codice
* Quando in un programma esistono più ambienti di sviluppo e alcune configurazioni sono diverse da un ambiente all’altro

## Aggiunta di variabili di ambiente {#add-variables}

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Cloud Manager elenca i vari programmi disponibili. Seleziona quello da gestire.
1. Seleziona la **Ambienti** nel pannello di navigazione a sinistra, seleziona l’ambiente per il quale desideri creare una variabile di ambiente.
1. Nel dettaglio dell’ambiente, seleziona la **Configurazione** scheda e seleziona **Aggiungi** per aprire **Configurazione dell&#39;ambiente** finestra di dialogo.
   * Se aggiungi una variabile di ambiente per la prima volta, viene visualizzata una **Aggiungi configurazione** al centro della pagina. Puoi usare questo pulsante o **Aggiungi** per aprire **Configurazione dell&#39;ambiente** finestra di dialogo.

   ![Scheda Configurazione](assets/configuration-tab.png)

1. Immetti i dettagli della variabile.
   * **Nome**
   * **Valore**
   * **Servizio applicato** - Definisce per quale servizio (Author/Publish/Preview) si applica la variabile o se si applica a tutti i servizi
   * **Tipo** - Definisce se la variabile è una variabile normale o un segreto

   ![Aggiunta di una variabile](assets/add-variable.png)

1. Dopo aver inserito la nuova variabile, devi selezionare **Aggiungi** nell’ultima colonna della riga contenente la nuova variabile.
   * È possibile immettere più variabili contemporaneamente immettendo una nuova riga e selezionando **Aggiungi**.

   ![Salva variabili](assets/save-variables.png)

1. Seleziona **Salva** per mantenere le variabili.

Un indicatore con lo stato **Aggiornamento** viene visualizzato nella parte superiore della tabella e accanto alla variabile appena aggiunta per indicare che l’ambiente viene aggiornato con la configurazione. Una volta completata, la nuova variabile di ambiente sarà visibile nella tabella.

![Aggiornamento delle variabili](assets/updating-variables.png)

>[!TIP]
>
>Per aggiungere più variabili, si consiglia di aggiungere la prima variabile, quindi utilizzare la **Aggiungi** nel **Configurazione dell&#39;ambiente** per aggiungere le variabili aggiuntive. In questo modo puoi aggiungerli con un aggiornamento all’ambiente.

## Aggiornamento delle variabili di ambiente {#update-variables}

Dopo aver creato le variabili di ambiente, puoi aggiornarle utilizzando **Aggiungi/Aggiorna** per avviare **Configurazione dell&#39;ambiente** finestra di dialogo.

1. Accedi ad Adobe Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Cloud Manager elenca i vari programmi disponibili. Seleziona quello da gestire.
1. Seleziona la **Ambienti** nel pannello di navigazione a sinistra, seleziona l’ambiente per il quale desideri creare una variabile di ambiente.
1. Nel dettaglio dell’ambiente, seleziona la **Configurazione** scheda e seleziona **Aggiungi/aggiorna** in alto a destra per aprire **Configurazione dell&#39;ambiente** finestra di dialogo.

   ![Pulsante Aggiungi/Aggiorna per le variabili](assets/add-update-variables.png)

1. Utilizzando il pulsante con i puntini di sospensione nell’ultima colonna della riga della variabile da modificare, selezionare **Modifica** o **Elimina**.

   ![Modificare o eliminare una variabile](assets/edit-delete-variable.png)

1. Modifica la variabile di ambiente in base alle esigenze.
   * Durante la modifica, il pulsante con i puntini di sospensione diventa Opzioni per ripristinare il valore originale o confermare la modifica.
   * Durante la modifica dei segreti, i valori possono essere aggiornati solo e non visualizzati.

   ![Modifica variabile](assets/edit-variable.png)

1. Dopo aver apportato tutte le modifiche di configurazione richieste, seleziona **Salva**.

[Come per l’aggiunta di variabili,](#add-variables) un indicatore con lo stato **Aggiornamento** viene visualizzato nella parte superiore della tabella e accanto alle variabili appena aggiornate per indicare che l’ambiente viene aggiornato con la configurazione. Una volta completate, le variabili di ambiente aggiornate saranno visibili nella tabella.

>[!TIP]
>
>Se desideri aggiornare più variabili, si consiglia di utilizzare il **Configurazione dell&#39;ambiente** per aggiornare tutte le variabili necessarie contemporaneamente prima di toccare o fare clic **Salva**. In questo modo puoi aggiungerli con un aggiornamento all’ambiente.
