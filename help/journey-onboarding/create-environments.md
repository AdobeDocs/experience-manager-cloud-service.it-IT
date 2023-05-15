---
title: Creazione di ambienti
description: Scopri come creare i primi ambienti con Cloud Manager.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 56%

---

# Creazione di ambienti {#create-environments}

In questa parte del [percorso di bordo,](overview.md) scopri come utilizzare Cloud Manager per creare i tuoi primi ambienti.

## Obiettivo {#objective}

Dopo aver letto il documento precedente di questo percorso di onboarding, [Creazione di programmi,](create-program.md) ora disponi di un programma di Cloud Manager personale. Ora puoi scoprire come creare i primi ambienti per tale programma con Cloud Manager.

Dopo aver letto questo documento:

* Saprai che cos’è un ambiente.
* Conoscerai la differenza tra i diversi ambienti.
* Sarai in grado di creare un ambiente personalizzato.

## Che cos’è un ambiente? {#environments}

Nella gerarchia di Cloud Manager, gli ambienti si trovano al di sotto dei programmi. Mentre i programmi consentono di organizzare la soluzione e concedere l’accesso a determinati membri del gruppo, gli ambienti appartengono a programmi specifici e rappresentano istanze individuali delle soluzioni Adobe all’interno di tali programmi. Gli ambienti si utilizzano per uno scopo specifico, ad esempio per l’authoring dei contenuti o i test di nuovi sviluppi. Le pipeline CI/CD di Cloud Manager facilitano la distribuzione del codice in questi ambienti dagli archivi Git.

Se si ricorda l&#39;esempio della teorica WKND Travel and Adventure Enterprises, che è un locatario che si concentra sui media relativi ai viaggi, potrebbero avere due programmi. Un programma Sites per la divisione WKND Magazine e un programma Assets per la divisione WKND Media. In ogni programma sono spesso presenti due ambienti, ad esempio un ambiente di produzione per il traffico effettivo del sito e un ambiente di sviluppo per i test del nuovo codice dell’applicazione.

Esistono quattro diversi tipi di ambienti:

* **Produzione e staging**: gli ambienti di produzione e staging sono disponibili in coppia e vengono utilizzati rispettivamente a scopi di produzione e test.
* **Sviluppo** - Un ambiente di sviluppo può essere creato a scopo di sviluppo e test e può essere associato solo alle pipeline non di produzione.
* **Sviluppo rapido** - Un ambiente di sviluppo rapido (RDE) consente agli sviluppatori di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che sono comprovate funzionare in un ambiente di sviluppo locale.

Ai fini di questo percorso di onboarding, per iniziare con un minimo, è necessario creare un ambiente di sviluppo da utilizzare per esplorare AEM funzionalità di as a Cloud Service.

## Creazione di ambienti {#creating-environments}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Selezionare il programma per il quale si desidera aggiungere un ambiente.

1. Per aggiungere un ambiente, dal **Panoramica del programma** nella pagina **Ambienti** scheda, seleziona **Aggiungi ambiente**.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

      ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente** che viene visualizzata:

   * Seleziona un **Tipo di ambiente**.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dopo il tipo di ambiente di sviluppo.
   * Fornisci un **Nome ambiente**.
   * Fornisci una **Descrizione ambiente**.
   * Seleziona un’**Area geografica cloud**.

   ![Finestra di dialogo Aggiungi ambiente](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Quando l’ambiente è disponibile, i membri dell’organizzazione assegnati al profilo di prodotto **Sviluppatore** possono accedere a Cloud Manager e gestire gli archivi Git di Cloud Manager.

## Passaggio successivo {#whats-next}

Dopo aver letto questa sezione del percorso di onboarding, dovresti:

* Saprai che cos’è un ambiente.
* Conoscerai la differenza tra i diversi ambienti.
* Sarai in grado di creare un ambiente personalizzato.

Ora che le risorse cloud sono state create, il team è pronto per accedervi. In qualità di amministratore di sistema, devi innanzitutto assegnare i membri del team ai profili di prodotto in AEM as a Cloud Service da Adobe Admin Console, in modo che possano accedere a tali risorse.

Pertanto, prima di continuare il percorso di onboarding, rivedi il documento [Assegnazione dei membri del gruppo ai profili di prodotto di AEM as a Cloud Service](assign-profiles-aem.md). In questo documento viene illustrato come concedere ai membri del team i diritti per accedere ai nuovi ambienti.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori risorse facoltative, se desideri andare oltre il contenuto del percorso di onboarding.

* [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) - Informazioni sui tipi di ambienti che è possibile creare e su come crearli per il progetto Cloud Manager
* [Utilizzo di Adobe Cloud Manager - Ambienti](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=it) - Gli ambienti Cloud Manager sono composti da servizi di authoring, pubblicazione AEM e Dispatcher. Scopri in che modo i diversi ambienti supportano i ruoli e come utilizzarli con diverse pipeline CI/CD.
* [Ambienti di sviluppo rapidi](/help/implementing/developing/introduction/rapid-development-environments.md) - Vedi questa documentazione per i dettagli su come utilizzare un RDE

<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

