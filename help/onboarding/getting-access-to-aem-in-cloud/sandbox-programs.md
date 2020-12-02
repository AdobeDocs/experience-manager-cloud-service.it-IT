---
title: Programmi sandbox - Cloud Service
description: Programmi sandbox - Cloud Service
translation-type: tm+mt
source-git-commit: 8383dc023b35cf76f7dc0e41cedef8cfab7753aa
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---


# Programmi sandbox {#sandbox-programs}

## Introduzione {#introduction}

Un programma Sandbox è uno dei due tipi di programmi disponibili AEM Cloud Service, l&#39;altro è un programma Regolare.

Un sandbox è in genere creato per scopi di formazione, demo in esecuzione, abilitazione o prova di concetto (POC). Non sono fatti per trasportare traffico dal vivo. Essi non sono soggetti al [AEM come impegni di Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Gli ambienti creati in una sandbox non sono configurati per il ridimensionamento automatico. Pertanto, non sono adatti per il test delle prestazioni o del carico.

I programmi sandbox includono Siti e Risorse e vengono compilati automaticamente con un repository Git, un ambiente di sviluppo e una pipeline non di produzione.  L&#39;archivio Git viene popolato con un progetto di esempio basato sull&#39;archetipo AEM progetto.

Fare riferimento a [Informazioni sui programmi e i tipi di programmi](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) per ulteriori informazioni sui tipi di programma.

### Attributi dei programmi sandbox {#attributes-sandbox}

I programmi sandbox hanno i seguenti attributi:

1. **Creazione del programma:** La creazione del programma Sandbox include automaticamente:
   * configurazione del progetto con codice e contenuto di esempio
   * creazione di un ambiente di sviluppo
   * creazione di una pipeline non di produzione che viene implementata in un ambiente di sviluppo (implementazione di un ramo principale in un ambiente di sviluppo)

1. **Soluzioni:** i programmi sandbox includono  AEM Sites e Assets.

1. **AEM aggiornamenti:** AEM aggiornamenti possono essere applicati manualmente agli ambienti in un programma sandbox e non vengono inviati automaticamente.

1. **Sospensione:** gli ambienti in un programma sandbox vengono automaticamente ibernati se non viene rilevata alcuna attività per un determinato periodo di tempo. Gli ambienti disattivati possono essere disattivati manualmente.

### Creazione di un programma sandbox {#creating-sandbox-program}

Una procedura guidata per la creazione di programmi consente di creare un programma sandbox.

Per informazioni su come creare un programma sandbox, consultare [Creazione di un programma sandbox](/help/onboarding/getting-access-to-aem-in-cloud/creating-a-program.md#create-sandbox-program) per ulteriori dettagli.

### Creazione di ambienti sandbox {#creating-sandbox-environments}

I programmi sandbox vengono distribuiti in un ambiente di sviluppo al momento della creazione del programma in modo automatico. L’ambiente di sviluppo include per impostazione predefinita un livello di authoring e pubblicazione.

L&#39;ambiente di fase di produzione può essere aggiunto manualmente al programma sandbox, quando l&#39;utente è pronto per impostare un ciclo di produzione.

Per informazioni su come creare manualmente un ambiente, consultare [Adding Environment](/help/implementing/cloud-manager/manage-environments.md) (Aggiunta di ambiente&lt;a1/>) per ulteriori dettagli.

### Eliminazione di ambienti sandbox {#deleting-sandbox-environments}

L&#39;utente con le autorizzazioni necessarie può eliminare un ambiente o set di ambienti di sviluppo o produzione/fase.

Per eliminare un ambiente, fare riferimento a [Eliminazione dell&#39;ambiente](/help/implementing/cloud-manager/manage-environments.md#deleting-environment) per ulteriori dettagli.


## Ambienti sandbox in sospensione e in sospensione {#hibernating-introduction}

Gli ambienti del programma sandbox entrano in una *modalità di sospensione* se non viene rilevata alcuna attività per un determinato periodo di tempo.

>[!NOTE]
>La sospensione è unica per gli ambienti del programma Sandbox. Gli ambienti di programma regolari non sono in grado di effettuare la sospensione.

### Sospensione {#hibernation-introduction}

La sospensione può avvenire automaticamente o manualmente. Per gli ambienti del programma sandbox potrebbero essere necessari fino a pochi minuti per entrare in una *modalità di sospensione*. I dati vengono conservati durante la sospensione.

La sospensione è classificata come:

* **Gli ambienti**  AutomaticSandbox Program vengono automaticamente bloccati dopo otto ore di inattività, il che significa che né l&#39;autore né i servizi di pubblicazione ricevono richieste.

* **Manuale**: In qualità di utente è possibile ibernare manualmente un ambiente del programma sandbox, anche se non vi è alcun obbligo di farlo, in quanto l&#39;ibernazione si verificherà automaticamente dopo un determinato periodo (otto ore) di inattività.

>[!CAUTION]
>Nell&#39;ultima versione, il collegamento alla console per sviluppatori direttamente da Cloud Manager non ti darà la possibilità di attivare un ambiente di programmi sandbox. La soluzione alternativa si trova una volta nella Developer Console, aggiungere il seguente pattern alla fine dell&#39;URL `#release-cm-p1234-e5678 where 1234` 1234 è l&#39; *ID programma* e 5678 è l&#39; *ID ambiente*.

#### Utilizzo della sospensione manuale {#using-manual-hibernation}

Potete attivare manualmente il programma sandbox dalla console per sviluppatori in due modi diversi, utilizzando:

* Schermata dei dettagli dell&#39;ambiente
* Schermata di elenco dell&#39;ambiente

>[!NOTE]
>L&#39;accesso a Developer Console per un programma sandbox è disponibile per qualsiasi utente di Cloud Manager.

Per attivare manualmente gli ambienti del programma sandbox, effettuate le seguenti operazioni:

1. Andate alla **Developer Console**.
Per informazioni su come accedere alla **Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) dalla scheda** Ambienti **, fare riferimento alla sezione [Accesso a Developer Console&lt;a1/>.**
   >[!IMPORTANT]
   >Il collegamento a **Developer Console** direttamente da Cloud Manager non consente di attivare un ambiente di programmi sandbox. La soluzione alternativa si trova una volta nella Developer Console, aggiungere il seguente pattern alla fine dell&#39;URL `#release-cm-p1234-e5678 where 1234` 1234 è l&#39; *ID programma* e 5678 è l&#39; *ID ambiente*.

1. Fare clic su **Sospensione**, come illustrato nella figura seguente:

   ![](assets/hibernate-1.png)

   Oppure,

   Fare clic sul collegamento **Ambienti** in alto a sinistra per visualizzare l&#39;elenco degli ambienti, quindi fare clic su **Sospensione**, come illustrato nella figura seguente:

   ![](assets/hibernate-1b.png)

1. Fare clic su **Sospensione** per confermare il passaggio.

   ![](assets/hibernate-2.png)

1. Quando l&#39;ibernazione ha esito positivo, nella schermata **Developer Console** visualizzerete la notifica completa del processo di ibernazione per il vostro ambiente.

   ![](assets/hibernate-4.png)


### Disiberazione {#de-hibernation-introduction}

1. Andate alla **Developer Console**.
Per informazioni su come accedere alla **Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) dalla scheda** Ambienti **, fare riferimento alla sezione [Accesso a Developer Console&lt;a1/>.**

   >[!IMPORTANT]
   >Il collegamento a **Developer Console** direttamente da Cloud Manager non consente di disattivare l&#39;ambiente del programma sandbox. La soluzione alternativa si trova una volta nella Developer Console, aggiungere il seguente pattern alla fine dell&#39;URL `#release-cm-p1234-e5678 where 1234` 1234 è l&#39; *ID programma* e 5678 è l&#39; *ID ambiente*.

   >[!NOTE]
   >In alternativa, è possibile accedere a **Developer Console** per disattivare la funzione di disattivazione tentando di accedere al servizio di creazione o pubblicazione di un ambiente già attivato; in tal caso, verrà visualizzata una pagina di destinazione con un collegamento alla Developer Console. Consultate la sezione Accesso a un ambiente sospeso di seguito.

   >[!IMPORTANT]
   >L&#39;accesso alla Developer Console è definito dal **Cloud Manager - Developer Role** nel **Admin Console**. Un utente con un&#39;autorizzazione per il ruolo di sviluppatore può disattivare l&#39;ambiente di un programma sandbox.

1. Fare clic su **De-hibernate**, come illustrato nella figura seguente:

   ![](assets/de-hibernation-img1.png)

   Oppure,

   Fare clic sul collegamento **Ambienti** in alto a sinistra per visualizzare l&#39;elenco degli ambienti, quindi fare clic su **De-hibernate**, come illustrato nella figura seguente

   ![](assets/de-hibernate-1b.png)


1. Fare clic su **De Hibernate** per confermare il passaggio.

   ![](assets/de-hibernation-img2.png)

1. Riceverai la notifica che il processo di disattivazione è iniziato e che verrà aggiornato con l&#39;avanzamento.

   ![](assets/de-hibernation-img3.png)

1. Al termine del processo, l&#39;ambiente Sandbox Program è nuovamente attivo.

   ![](assets/de-hibernation-img4.png)

#### Autorizzazioni per la disattivazione {#permissions-de-hibernate}

Ogni utente con un profilo di prodotto che dia loro accesso a AEM come Cloud Service dovrebbe essere in grado di accedere alla **Developer Console**, consentendo loro di disattivare l&#39;ambiente.

#### Accesso a un ambiente sospeso {#accessing-hibernated-environment}

Quando si effettuano richieste del browser a fronte del livello di authoring o pubblicazione di un ambiente attivato, l’utente riceve una pagina di destinazione che descrive lo stato di ibernazione dell’ambiente, come illustrato nella figura seguente:

![](assets/de-hibernation-img5.png)

### Considerazioni importanti {#important-considerations}

Alcune considerazioni chiave relative agli ambienti in sospensione e in disattivazione sono:

* Un utente può utilizzare una pipeline per distribuire il codice personalizzato per gli ambienti ibernati. L&#39;ambiente resterà in ibernazione e il nuovo codice apparirà nell&#39;ambiente una volta disattivato.

* AEM aggiornamenti possono essere applicati agli ambienti bloccati, che i clienti possono attivare manualmente da Cloud Manager. L&#39;ambiente rimarrà bloccato e la nuova versione apparirà nell&#39;ambiente una volta disattivata.

>[!NOTE]
>Al momento, Cloud Manager non indica se un ambiente è bloccato.

## AEM aggiornamenti agli ambienti sandbox {#aem-updates-sandbox}

Per ulteriori informazioni, fare riferimento a [AEM aggiornamenti della versione](/help/implementing/deploying/aem-version-updates.md).

Un utente può applicare manualmente AEM aggiornamenti agli ambienti in un programma sandbox.

Fare riferimento a [Aggiornamento dell&#39;ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) per informazioni su come aggiornare un ambiente.

>[!NOTE]
>* Un aggiornamento manuale può essere eseguito solo se l&#39;ambiente di destinazione dispone di una pipeline configurata correttamente.
>* L&#39;aggiornamento manuale dell&#39;ambiente *Produzione* o *Stage* comporterà l&#39;aggiornamento automatico dell&#39;altro ambiente. L&#39;ambiente Production+Stage impostato deve trovarsi nella stessa versione AEM.






