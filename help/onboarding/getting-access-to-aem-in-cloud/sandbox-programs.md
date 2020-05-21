---
title: Programmi sandbox - Servizio Cloud
description: Programmi sandbox - Servizio Cloud
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Programmi sandbox {#sandbox-programs}

## Introduzione {#introduction}

Un programma sandbox è uno dei due tipi di programmi disponibili in AEM Cloud Service, mentre l&#39;altro è un programma regolare.

Un sandbox viene in genere creato per scopi di formazione, demo in esecuzione, abilitazione o POC. Non sono fatti per trasportare traffico dal vivo.

I programmi sandbox includono Siti e Risorse e verranno forniti automaticamente con un ramo Git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.

Per ulteriori informazioni sui tipi di programma, vedere [Informazioni sui programmi e i tipi](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)di programma.

### Attributi dei programmi sandbox {#attributes-sandbox}

I programmi sandbox hanno i seguenti attributi:

1. **Creazione del programma:** La creazione del programma Sandbox include automaticamente:
   * configurazione del progetto con codice e contenuto di esempio
   * creazione di un ambiente di sviluppo
   * creazione di una pipeline non di produzione che viene implementata in un ambiente di sviluppo (implementazione di un ramo principale in un ambiente di sviluppo)

1. **Soluzioni incluse:** I programmi sandbox includono Siti e Risorse.

1. **Aggiornamenti AEM:** Gli aggiornamenti di AEM possono essere applicati manualmente agli ambienti in un programma sandbox e non vengono inviati automaticamente.

1. **Sospensione:** Gli ambienti in un programma sandbox saranno automaticamente bloccati se non viene rilevata alcuna attività per un determinato periodo di tempo. Gli ambienti con sospensione possono essere disattivati manualmente.

### Creazione di un programma sandbox {#creating-sandbox-program}

Una procedura guidata di creazione del programma chiederà all&#39;utente di inviare i dettagli.

Per informazioni su come creare un programma sandbox, consultate [Creazione di un programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)sandbox.

### Creazione di ambienti sandbox {#creating-sandbox-environments}

I programmi sandbox verranno forniti un ambiente di sviluppo al momento della creazione del programma in modo automatico. L’ambiente di sviluppo include per impostazione predefinita un livello di authoring e pubblicazione.

L&#39;ambiente Production-Stage impostato può essere aggiunto manualmente al programma Sandbox, quando l&#39;utente è pronto per impostare una pipeline di produzione.

Per informazioni su come creare manualmente un ambiente, vedere [Aggiunta di ambienti](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments).

### Eliminazione di ambienti sandbox  {#deleting-sandbox-environments}

L&#39;utente con le autorizzazioni necessarie sarà in grado di eliminare un ambiente/set di sviluppo o produzione/fase.

Per informazioni sull&#39;eliminazione di un ambiente, vedere [Eliminazione di ambienti](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment).


## Ambienti sandbox in sospensione e in sospensione {#hibernating-introduction}

Gli ambienti del programma sandbox entreranno in modalità *di* sospensione dopo un periodo di inattività.

>[!NOTE]
>La sospensione è unica per gli ambienti di programmi sandbox. Gli ambienti di programma regolari non saranno vietati.

### Sospensione {#hibernation-introduction}

La sospensione può avvenire automaticamente o manualmente. L&#39;attivazione di un ambiente potrebbe richiedere fino a pochi minuti. I dati vengono conservati durante la sospensione.

La sospensione è classificata come:

* **Gli ambienti con programma sandbox automatico** vengono automaticamente bloccati dopo otto ore di inattività, il che significa che non viene richiesta l&#39;autore o i servizi di pubblicazione.

* **Manuale**: I clienti possono ibernare manualmente un ambiente di programma sandbox, anche se non vi è alcun requisito a tal fine, poiché l&#39;ibernazione si verificherà automaticamente dopo un periodo di inattività.

#### Utilizzo della sospensione manuale {#using-manual-hibernation}


L’ibernazione manuale può essere effettuata su uno dei due schermi nella console per sviluppatori.

Seguite i passaggi riportati di seguito per attivare manualmente gli ambienti del programma:

1. Andate alla console per sviluppatori.
1. Fate clic su Sospendi
1. Fate clic su Sospendi per confermare.
1. Quando l&#39;ibernazione ha esito positivo, viene visualizzata la schermata seguente.
1. Nella schermata di elenco degli ambienti, illustrata di seguito e accessibile facendo clic sul collegamento Ambienti nella schermata di dettaglio dell&#39;ambiente, è possibile fare clic sul pulsante Sospendi nella riga dell&#39;ambiente desiderato. Viene visualizzata una schermata di conferma.

### De-ibernazione {#de-hibernation-introduction}

>[!IMPORTANT]
>L&#39;accesso alla Developer Console è definito dall&#39;opzione &quot;Cloud Manager - Ruolo sviluppatore&quot; nell&#39;Admin Console. Con tale autorizzazione, un utente può disattivare l’ambiente.

### Accesso a un ambiente sospeso {#accessing-hibernated-environment}

Quando si effettuano richieste del browser a fronte del livello di authoring o pubblicazione di un ambiente attivato, l’utente riceve una pagina di destinazione che descrive lo stato di ibernazione dell’ambiente, come illustrato di seguito:

Un utente con il &quot;Cloud Manager - Ruolo sviluppatore&quot; può fare clic sul pulsante Developer Console per accedere alla console per sviluppatori e disattivare l&#39;ambiente. Informazioni sull&#39;impostazione dei ruoli sono disponibili nella documentazione di Cloud Manager.

Se un utente in un&#39;organizzazione non può fare clic sul pulsante Developer Console per essere portato nella Developer Console, è probabile che gli sia necessario assegnare &quot;Cloud Manager - Ruolo sviluppatore&quot;.




## Aggiornamenti AEM agli ambienti sandbox {#aem-updates-sandbox}


Fate riferimento agli aggiornamenti delle versioni di [AEM](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates).

L&#39;utente può applicare manualmente gli aggiornamenti AEM agli ambienti in un programma sandbox (vedere la figura seguente). Questo può essere fatto quando lo stato visualizzato è UPDATE DISPONIBILE. L&#39;opzione Aggiorna sarà disponibile dal menu a discesa nella scheda Ambienti. Può anche essere selezionato dal menu Gestisci dalla schermata AMBIENTI.

>[!NOTE]
>Affinché sia avviata una pipeline di aggiornamento manuale, è necessario configurare una pipeline non di produzione che viene implementata nell&#39;ambiente di sviluppo di interesse.

>[!NOTE]
>Per avviare una pipeline di aggiornamento manuale per l&#39;ambiente Production+Stage, è necessario configurare una pipeline di produzione.

>[!NOTE]
>L&#39;aggiornamento manuale in ambiente Produzione o Stage aggiornerà automaticamente l&#39;altro. L’ambiente Production+Stage impostato deve trovarsi nella stessa versione di AEM.





