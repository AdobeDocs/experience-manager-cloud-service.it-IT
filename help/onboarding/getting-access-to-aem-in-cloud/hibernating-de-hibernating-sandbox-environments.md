---
title: 'Ambienti Sandbox sospensione e disattivazione '
description: 'Ambienti Sandbox sospensione e disattivazione '
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---


# Ambienti Sandbox sospensione e disattivazione {#hibernating-introduction}

Gli ambienti del programma sandbox immettono una *modalità di sospensione* se non viene rilevata alcuna attività per un determinato periodo di tempo.

>[!NOTE]
>La sospensione è unica negli ambienti del programma sandbox. Gli ambienti dei programmi di produzione non sono in ibernazione.

## Sospensione {#hibernation-introduction}

La sospensione può avvenire automaticamente o manualmente. Per gli ambienti del programma sandbox potrebbero essere necessari fino a pochi minuti per entrare in una modalità di sospensione **. I dati vengono conservati durante la sospensione.

La sospensione è classificata come:

* ****  Gli ambienti del programma AutomaticSandbox vengono automaticamente ibernati dopo otto ore di inattività, il che significa che né i servizi di authoring né quelli di pubblicazione ricevono richieste.

* **Manuale**: In qualità di utente puoi ibernare manualmente un ambiente di programma sandbox, anche se non è necessario farlo, in quanto la sospensione si verifica automaticamente dopo un certo periodo (otto ore) di inattività.

>[!CAUTION]
>Nell’ultima versione, il collegamento diretto alla Console per sviluppatori da Cloud Manager non ti darà la possibilità di attivare un ambiente di programma sandbox. La soluzione alternativa si trova una volta nella Console per sviluppatori, aggiungi il seguente pattern alla fine dell’url `#release-cm-p1234-e5678 where 1234` 1234 è il tuo *ID programma* e 5678 è il tuo *ID ambiente*.

### Utilizzo della sospensione manuale {#using-manual-hibernation}

Puoi attivare manualmente il programma sandbox dalla Console per sviluppatori in due modi diversi utilizzando:

* Schermata dei dettagli dell&#39;ambiente
* Schermata di elenco degli ambienti

>[!NOTE]
>L’accesso a Developer Console per un programma sandbox è disponibile per qualsiasi utente di Cloud Manager.

Per attivare manualmente gli ambienti del programma sandbox, effettua le seguenti operazioni:

1. Passa alla **Console per sviluppatori**.
Per informazioni su come accedere alla **Console per sviluppatori** dalla scheda **Ambienti**, consulta [Accesso alla Console per sviluppatori](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) .
   >[!IMPORTANT]
   >Il collegamento diretto a **Console per sviluppatori** da Cloud Manager non consente di attivare un ambiente di programmi sandbox. La soluzione alternativa si trova una volta nella Console per sviluppatori, aggiungi il seguente pattern alla fine dell’url `#release-cm-p1234-e5678 where 1234` 1234 è il tuo *ID programma* e 5678 è il tuo *ID ambiente*.

1. Fai clic su **Sospendi**, come illustrato nella figura seguente:

   ![](assets/hibernate-1.png)

   Oppure,

   Fai clic sul collegamento **Ambienti** in alto a sinistra per visualizzare l’elenco degli ambienti, quindi fai clic su **Sospendi**, come illustrato nella figura seguente:

   ![](assets/hibernate-1b.png)

1. Fai clic su **Sospendi** per confermare il passaggio.

   ![](assets/hibernate-2.png)

1. Quando la sospensione avrà esito positivo, nella schermata **Console per sviluppatori** verrà visualizzata la notifica completa del processo di ibernazione per l’ambiente.

   ![](assets/hibernate-4.png)


## Disiberazione {#de-hibernation-introduction}

1. Passa alla **Console per sviluppatori**.
Per informazioni su come accedere alla **Console per sviluppatori** dalla scheda **Ambienti**, consulta [Accesso alla Console per sviluppatori](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) .

   >[!IMPORTANT]
   >Il collegamento diretto a **Console per sviluppatori** da Cloud Manager non consente di disattivare l’ambiente di un programma sandbox. La soluzione alternativa si trova una volta nella Console per sviluppatori, aggiungi il seguente pattern alla fine dell’url `#release-cm-p1234-e5678 where 1234` 1234 è il tuo *ID programma* e 5678 è il tuo *ID ambiente*.

   >[!NOTE]
   >In alternativa, puoi passare alla **Console per sviluppatori** per annullare l’ibernazione provando ad accedere al servizio di authoring o pubblicazione di un ambiente già attivato; in tal caso, viene visualizzata una pagina di destinazione con un collegamento alla Console per sviluppatori. Consulta la sezione Accesso a un ambiente sospeso di seguito.

   >[!IMPORTANT]
   >L’accesso alla Console per sviluppatori è definito da **Cloud Manager - Developer Role** nell’ **Admin Console**. Un utente con un’autorizzazione per ruolo sviluppatore può disattivare l’ibernazione di un ambiente Programma sandbox.

1. Fai clic su **De-hibernate**, come illustrato nella figura seguente:

   ![](assets/de-hibernation-img1.png)

   Oppure,

   Fai clic sul collegamento **Ambienti** in alto a sinistra per visualizzare l&#39;elenco degli ambienti, quindi fai clic su **Disiberna**, come illustrato nella figura seguente

   ![](assets/de-hibernate-1b.png)


1. Fai clic su **De Hibernate** per confermare il passaggio.

   ![](assets/de-hibernation-img2.png)

1. Riceverai la notifica dell’avvio del processo di de-ibernazione e verrai aggiornato con l’avanzamento.

   ![](assets/de-hibernation-img3.png)

1. Al termine del processo, l’ambiente del programma sandbox è nuovamente attivo.

   ![](assets/de-hibernation-img4.png)

### Autorizzazioni per la disattivazione {#permissions-de-hibernate}

Qualsiasi utente con un profilo di prodotto che dia accesso a AEM come Cloud Service dovrebbe essere in grado di accedere alla **Console per sviluppatori**, consentendo loro di disattivare l&#39;ambiente.

## Accesso a un ambiente sospeso {#accessing-hibernated-environment}

Quando effettua richieste del browser sul livello di authoring o pubblicazione di un ambiente in ibernazione, l’utente incontra una pagina di destinazione che descrive lo stato di ibernazione dell’ambiente, come illustrato nella figura seguente:

![](assets/de-hibernation-img5.png)

## Considerazioni importanti {#important-considerations}

Alcune considerazioni chiave relative agli ambienti ibernati e disattivati sono:

* Un utente può utilizzare una pipeline per distribuire codice personalizzato per gli ambienti in sospensione. L’ambiente rimarrà in ibernazione e il nuovo codice verrà visualizzato nell’ambiente una volta disattivato.

* Gli aggiornamenti AEM possono essere applicati agli ambienti in sospensione, attivabili manualmente dai clienti da Cloud Manager. L’ambiente rimarrà in ibernazione e la nuova versione apparirà nell’ambiente una volta disattivata.

>[!NOTE]
>Al momento, Cloud Manager non indica se un ambiente è ibernato.

## Aggiornamenti AEM ambienti Sandbox {#aem-updates-sandbox}

Per ulteriori informazioni, consulta [AEM aggiornamenti della versione](/help/implementing/deploying/aem-version-updates.md) .

Un utente può applicare manualmente AEM aggiornamenti agli ambienti in un programma sandbox.

Per informazioni su come aggiornare un ambiente, consulta [Aggiornamento ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) .

>[!NOTE]
>* È possibile eseguire un aggiornamento manuale solo se l’ambiente di destinazione dispone di una pipeline configurata correttamente.
>* Un aggiornamento manuale dell&#39;ambiente *Produzione* o *Stage* aggiornerà automaticamente l&#39;altro ambiente. L’ambiente Production+Stage deve trovarsi nella stessa versione AEM.






