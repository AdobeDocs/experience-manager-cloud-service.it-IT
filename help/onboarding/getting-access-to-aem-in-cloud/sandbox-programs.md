---
title: Programmi sandbox - Cloud Service
description: Programmi sandbox - Cloud Service
translation-type: tm+mt
source-git-commit: b3fbe13df886459c6b18369af1a6e550ccad0454
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---


# Programmi sandbox {#sandbox-programs}

## Introduzione {#introduction}

Un programma Sandbox è uno dei due tipi di programmi disponibili AEM Cloud Service, l&#39;altro è un programma Regolare.

Un sandbox è in genere creato per scopi di formazione, demo in esecuzione, abilitazione o prova di concetto (POC). Non sono fatti per trasportare traffico dal vivo. Essi non sono soggetti al [AEM come impegni](https://www.adobe.com/legal/service-commitments.html)Cloud Service.

Gli ambienti creati in una sandbox non sono configurati per il ridimensionamento automatico. Pertanto, non sono adatti per il test delle prestazioni o del carico.

I programmi sandbox includono Siti e Risorse e vengono compilati automaticamente con un repository Git, un ambiente di sviluppo e una pipeline non di produzione.  L&#39;archivio Git viene popolato con un progetto di esempio basato sull&#39;archetipo AEM progetto.

Per ulteriori informazioni sui tipi di programma, consulta [Informazioni sui programmi e i tipi](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) di programma.

### Attributi dei programmi sandbox {#attributes-sandbox}

I programmi sandbox hanno i seguenti attributi:

1. **Creazione del programma:** La creazione del programma Sandbox include automaticamente:
   * configurazione del progetto con codice e contenuto di esempio
   * creazione di un ambiente di sviluppo
   * creazione di una pipeline non di produzione che viene implementata in un ambiente di sviluppo (implementazione di un ramo principale in un ambiente di sviluppo)

1. **Soluzioni:** I programmi sandbox includono  AEM Sites e Risorse.

1. **Aggiornamenti AEM:** AEM aggiornamenti possono essere applicati manualmente agli ambienti in un programma sandbox e non vengono inviati automaticamente.

1. **Sospensione:** Gli ambienti in un programma sandbox vengono automaticamente bloccati se non viene rilevata alcuna attività per un determinato periodo di tempo. Gli ambienti disattivati possono essere disattivati manualmente.

### Creazione di un programma sandbox {#creating-sandbox-program}

Una procedura guidata per la creazione di programmi consente di creare un programma sandbox.

Per informazioni su come creare un programma sandbox, consultate [Creazione di un programma](/help/onboarding/getting-access-to-aem-in-cloud/creating-a-program.md#create-sandbox-program) sandbox per ulteriori dettagli.

### Creazione di ambienti sandbox {#creating-sandbox-environments}

I programmi sandbox vengono distribuiti in un ambiente di sviluppo al momento della creazione del programma in modo automatico. L’ambiente di sviluppo include per impostazione predefinita un livello di authoring e pubblicazione.

L&#39;ambiente di fase di produzione può essere aggiunto manualmente al programma sandbox, quando l&#39;utente è pronto per impostare un ciclo di produzione.

Per ulteriori informazioni su come creare manualmente un ambiente, vedere [Aggiunta di ambienti](/help/implementing/cloud-manager/manage-environments.md) .

### Eliminazione di ambienti sandbox {#deleting-sandbox-environments}

L&#39;utente con le autorizzazioni necessarie può eliminare un ambiente o set di ambienti di sviluppo o produzione/fase.

Per eliminare un ambiente, vedere [Eliminazione di ambienti](/help/implementing/cloud-manager/manage-environments.md#deleting-environment) per ulteriori dettagli.


## Ambienti sandbox in sospensione e in sospensione {#hibernating-introduction}

Se non viene rilevata alcuna attività per un determinato periodo di tempo, gli ambienti del programma sandbox entrano in una modalità *di* sospensione.

>[!NOTE]
>La sospensione è unica per gli ambienti del programma Sandbox. Gli ambienti di programma regolari non sono in grado di effettuare la sospensione.

### Sospensione {#hibernation-introduction}

La sospensione può avvenire automaticamente o manualmente. Per gli ambienti Sandbox Program possono essere necessari fino a pochi minuti per entrare in modalità *di sospensione*. I dati vengono conservati durante la sospensione.

La sospensione è classificata come:

* **Gli ambienti con programma sandbox automatico** vengono automaticamente bloccati dopo otto ore di inattività, il che significa che né l&#39;autore né i servizi di pubblicazione ricevono richieste.

* **Manuale**: In qualità di utente è possibile ibernare manualmente un ambiente del programma sandbox, anche se non vi è alcun obbligo di farlo, in quanto l&#39;ibernazione si verificherà automaticamente dopo un determinato periodo (otto ore) di inattività.

>[!CAUTION]
>Nell&#39;ultima versione, il collegamento alla console per sviluppatori direttamente da Cloud Manager non ti darà la possibilità di attivare un ambiente di programmi sandbox. La soluzione alternativa si trova una volta nella Developer Console. Alla fine dell’URL `#release-cm-p1234-e5678 where 1234` 1234, aggiungere il seguente pattern è l’ID ** programma e 5678 è l’ID ** ambiente.

#### Utilizzo della sospensione manuale {#using-manual-hibernation}

Potete attivare manualmente il programma sandbox dalla console per sviluppatori in due modi diversi, utilizzando:

* Schermata dei dettagli dell&#39;ambiente
* Schermata di elenco dell&#39;ambiente

>[!NOTE]
>L&#39;accesso a Developer Console per un programma sandbox è disponibile per qualsiasi utente di Cloud Manager.

Per attivare manualmente gli ambienti del programma sandbox, effettuate le seguenti operazioni:

1. Passate alla **console**per sviluppatori.
Per informazioni su come accedere alla [console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) per sviluppatori, consultate Accesso alla console **per sviluppatori dalla scheda** Ambienti **** .
   >[!IMPORTANT]
   >Il collegamento alla **Developer Console** direttamente da Cloud Manager non consente di attivare un ambiente di programmi sandbox. La soluzione alternativa si trova una volta nella Developer Console. Alla fine dell’URL `#release-cm-p1234-e5678 where 1234` 1234, aggiungere il seguente pattern è l’ID ** programma e 5678 è l’ID ** ambiente.

1. Click **Hibernate**, as shown in the figure below:

   ![](assets/hibernate-1.png)

   Oppure,

   Fate clic sul collegamento **Ambienti** in alto a sinistra per visualizzare l&#39;elenco degli ambienti e quindi fate clic su **Sospendi**, come illustrato nella figura seguente:

   ![](assets/hibernate-1b.png)

1. Fate clic su **Sospendi** per confermare il passaggio.

   ![](assets/hibernate-2.png)

1. Quando la sospensione ha esito positivo, nella schermata **Developer Console** visualizzerete la notifica completa del processo di ibernazione per il vostro ambiente.

   ![](assets/hibernate-4.png)


### De-ibernazione {#de-hibernation-introduction}

1. Passate alla **console**per sviluppatori.
Per informazioni su come accedere alla [console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) per sviluppatori, consultate Accesso alla console **per sviluppatori dalla scheda** Ambienti **** .

   >[!IMPORTANT]
   >Il collegamento alla **Developer Console** direttamente da Cloud Manager non consente di disattivare l&#39;ambiente del programma sandbox. La soluzione alternativa si trova una volta nella Developer Console. Alla fine dell’URL `#release-cm-p1234-e5678 where 1234` 1234, aggiungere il seguente pattern è l’ID ** programma e 5678 è l’ID ** ambiente.

   >[!NOTE]
   >In alternativa, è possibile accedere a **Developer Console** per disattivare la funzione di disattivazione tentando di accedere al servizio di creazione o pubblicazione di un ambiente già attivato; in tal caso, verrà visualizzata una pagina di destinazione con un collegamento alla Developer Console. Consultate la sezione Accesso a un ambiente sospeso di seguito.

   >[!IMPORTANT]
   >L&#39;accesso alla Developer Console è definito da **Cloud Manager - Developer Role** nel Admin Console ****. Un utente con un&#39;autorizzazione per il ruolo di sviluppatore può disattivare l&#39;ambiente di un programma sandbox.

1. Fate clic su **De-hibernate**, come illustrato nella figura seguente:

   ![](assets/de-hibernation-img1.png)

   Oppure,

   Fate clic sul collegamento **Ambienti** in alto a sinistra per visualizzare l&#39;elenco degli ambienti e quindi fate clic su **De-hibernate**, come illustrato nella figura seguente

   ![](assets/de-hibernate-1b.png)


1. Fate clic su **De Hibernate** per confermare il passaggio.

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

Per ulteriori informazioni, consultate [AEM aggiornamenti](/help/implementing/deploying/overview.md#version-updates) delle versioni.

Un utente può applicare manualmente AEM aggiornamenti agli ambienti in un programma sandbox.

Per informazioni sull&#39;aggiornamento di un ambiente, vedere [Aggiornamento dell&#39;ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) .

>[!NOTE]
>* Un aggiornamento manuale può essere eseguito solo se l&#39;ambiente di destinazione dispone di una pipeline configurata correttamente.
>* Un aggiornamento manuale per l&#39;ambiente *Produzione* o *Stage* aggiornerà automaticamente l&#39;altro. L&#39;ambiente Production+Stage impostato deve trovarsi nella stessa versione AEM.






