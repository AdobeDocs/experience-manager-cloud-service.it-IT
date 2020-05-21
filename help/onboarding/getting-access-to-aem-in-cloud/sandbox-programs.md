---
title: Programmi sandbox - Servizio Cloud
description: Programmi sandbox - Servizio Cloud
translation-type: tm+mt
source-git-commit: e7cad0cd67f04eac5627e72339ccb1c4f54cc8c8
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---


# Programmi sandbox {#sandbox-programs}

## Introduzione {#introduction}

Un programma sandbox è uno dei due tipi di programmi disponibili in AEM Cloud Service, mentre l&#39;altro è un programma regolare.

Un sandbox è in genere creato per scopi di formazione, demo in esecuzione, abilitazione o prova di concetto (POC). Non sono fatti per trasportare traffico dal vivo.

I programmi sandbox includono Siti e Risorse ed è popolato automaticamente con un ramo Git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.

Per ulteriori informazioni sui tipi di programma, vedere [Informazioni sui programmi e i tipi](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)di programma.

### Attributi dei programmi sandbox {#attributes-sandbox}

I programmi sandbox hanno i seguenti attributi:

1. **Creazione del programma:** La creazione del programma Sandbox include automaticamente:
   * configurazione del progetto con codice e contenuto di esempio
   * creazione di un ambiente di sviluppo
   * creazione di una pipeline non di produzione che viene implementata in un ambiente di sviluppo (implementazione di un ramo principale in un ambiente di sviluppo)

1. **Soluzioni:** I programmi sandbox includono AEM Sites e Assets.

1. **Aggiornamenti AEM:** Gli aggiornamenti di AEM possono essere applicati manualmente agli ambienti in un programma sandbox e non vengono inviati automaticamente.

1. **Sospensione:** Gli ambienti in un programma sandbox vengono automaticamente bloccati se non viene rilevata alcuna attività per un determinato periodo di tempo. Gli ambienti con sospensione possono essere disattivati manualmente.

### Creazione di un programma sandbox {#creating-sandbox-program}

Una procedura guidata per la creazione di programmi consente di creare un programma sandbox.

Per informazioni su come creare un programma sandbox, consultate [Creazione di un programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)sandbox.

### Creazione di ambienti sandbox {#creating-sandbox-environments}

I programmi sandbox vengono forniti un ambiente di sviluppo al momento della creazione del programma in modo automatico. L’ambiente di sviluppo include per impostazione predefinita un livello di authoring e pubblicazione.

L&#39;ambiente di fase di produzione può essere aggiunto manualmente al programma sandbox, quando l&#39;utente è pronto per impostare un ciclo di produzione.

Per ulteriori informazioni su come creare manualmente un ambiente, vedere [Aggiunta di ambienti](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) .

### Eliminazione di ambienti sandbox  {#deleting-sandbox-environments}

L&#39;utente con le autorizzazioni necessarie può eliminare un ambiente o set di ambienti di sviluppo o produzione/fase.

Per eliminare un ambiente, vedere [Eliminazione di ambienti](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) per ulteriori dettagli.


## Ambienti sandbox in sospensione e in sospensione {#hibernating-introduction}

Se non viene rilevata alcuna attività per un determinato periodo di tempo, gli ambienti del programma sandbox entrano in una modalità *di* sospensione.

>[!NOTE]
>La sospensione è unica per gli ambienti del programma Sandbox. Gli ambienti di programma regolari non sono in grado di effettuare la sospensione.

### Sospensione {#hibernation-introduction}

La sospensione può avvenire automaticamente o manualmente. Per gli ambienti Sandbox Program possono essere necessari fino a pochi minuti per entrare in modalità *di sospensione*. I dati vengono conservati durante la sospensione.

La sospensione è classificata come:

* **Gli ambienti con programma sandbox automatico** vengono automaticamente bloccati dopo otto ore di inattività, il che significa che non vengono richiesti né l&#39;autore né i servizi di pubblicazione.

* **Manuale**: In qualità di utente è possibile ibernare manualmente un ambiente del programma sandbox, anche se non vi è alcun obbligo di farlo, in quanto l&#39;ibernazione si verificherà automaticamente dopo un certo periodo (otto ore) di inattività.

#### Utilizzo della sospensione manuale {#using-manual-hibernation}

Potete attivare manualmente il programma sandbox dalla console per sviluppatori in due modi diversi, utilizzando:

* Schermata dei dettagli dell&#39;ambiente
* Schermata di elenco dell&#39;ambiente

Per attivare manualmente gli ambienti del programma sandbox, effettuate le seguenti operazioni:

1. Passate alla **console**per sviluppatori.
Per informazioni su come accedere alla [console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) per sviluppatori, consultate Accesso alla console **per sviluppatori dalla scheda** Ambienti **** .
1. Fate clic su Sospendi, come illustrato nella figura seguente:
1. Fate clic su **Sospendi** per confermare il passaggio
1. Quando l&#39;ibernazione ha esito positivo, viene visualizzata la schermata seguente.

#### Accesso a un ambiente sospeso {#accessing-hibernated-environment}

Quando si effettuano richieste del browser a fronte del livello di authoring o pubblicazione di un ambiente attivato, l’utente riceve una pagina di destinazione che descrive lo stato di ibernazione dell’ambiente, come illustrato di seguito:

Un utente con **Cloud Manager - Developer Role** può fare clic sul pulsante Developer Console per accedere alla console per sviluppatori e disattivare l&#39;ambiente. Informazioni sull&#39;impostazione dei ruoli sono disponibili nella documentazione di Cloud Manager.

Se un utente in un&#39;organizzazione non può fare clic sul pulsante Developer Console per essere portato nella Developer Console, è probabile che gli sia necessario assegnare &quot;Cloud Manager - Ruolo sviluppatore&quot;.


### De-ibernazione {#de-hibernation-introduction}

1. Passate alla **console**per sviluppatori.
Per informazioni su come accedere alla [console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) per sviluppatori, consultate Accesso alla console **per sviluppatori dalla scheda** Ambienti **** .

   >[!IMPORTANT]
   >L&#39;accesso alla console per sviluppatori è definito da **Cloud Manager - Ruolo** sviluppatore nell&#39; **Admin Console**. Un utente con un&#39;autorizzazione per il ruolo di sviluppatore può disattivare l&#39;ambiente di un programma sandbox.

1. Fate clic su **De-hibernate**, come illustrato nella figura seguente:

   ![](assets/de-hibernation-img1.png)

1. Fate clic su **De Hibernate** per confermare il passaggio.

   ![](assets/de-hibernation-img2.png)

1. Riceverai la notifica che il processo di disattivazione è iniziato e che verrà aggiornato con l&#39;avanzamento.

   ![](assets/de-hibernation-img3.png)

1. Al termine del processo, l&#39;ambiente Sandbox Program è nuovamente attivo.

   ![](assets/de-hibernation-img4.png)


## Aggiornamenti AEM agli ambienti sandbox {#aem-updates-sandbox}


Per ulteriori informazioni, consultate Aggiornamenti [delle versioni di](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) AEM.

Un utente può applicare manualmente gli aggiornamenti AEM agli ambienti in un programma sandbox (vedere la figura di seguito). Questo può essere fatto quando lo stato visualizzato è **UPDATE DISPONIBILE**.

L&#39;opzione Aggiorna è disponibile nel menu a discesa della scheda **Ambienti** . Questa opzione è disponibile anche dal pulsante **Gestisci** , se fate clic su **Dettagli** dalla scheda **Ambienti** .

>[!NOTE]
>Affinché sia avviata una pipeline di aggiornamento manuale, è necessario configurare una pipeline *di* non produzione che viene distribuita nell&#39;ambiente di sviluppo di interesse.

>[!NOTE]
>Per avviare una pipeline di aggiornamento manuale per l&#39;ambiente Production+Stage, è necessario configurare una pipeline di *produzione* .

>[!NOTE]
>L&#39;aggiornamento manuale all&#39;ambiente *Produzione* o *Stage* aggiornerà automaticamente l&#39;altro. L’ambiente Production+Stage impostato deve trovarsi nella stessa versione di AEM.





