---
title: Creare ambienti
description: Scopri come utilizzare Cloud Manager per creare i tuoi primi ambienti.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---

# Creare ambienti {#create-environments}

In questa parte del [percorso di bordo,](overview.md) scoprite come utilizzare Cloud Manager per creare i primi ambienti.

## Obiettivo {#objective}

Dopo aver letto il documento precedente in questo percorso di onboarding, [Creazione di programmi,](create-program.md) ora disponi del tuo programma Cloud Manager. Ora puoi imparare a utilizzare Cloud Manager per creare i tuoi primi ambienti per quel programma.

Dopo aver letto questo documento:

* Comprendere cos&#39;è un ambiente.
* Scopri la differenza tra i diversi ambienti.
* Puoi creare il tuo ambiente.

## Che cos&#39;è un ambiente? {#environments}

Gli ambienti si trovano sotto i programmi nella gerarchia di Cloud Manager. Mentre i programmi consentono di organizzare la soluzione e concedere l&#39;accesso a determinati membri del team a tali programmi, gli ambienti appartengono a programmi specifici e sono istanze individuali delle soluzioni di Adobe all&#39;interno di tali programmi. Gli ambienti vengono utilizzati per uno scopo specifico, ad esempio per creare contenuti o testare nuovi sviluppi. Le pipeline CI/CD di Cloud Manager facilitano la distribuzione del codice a questi ambienti dagli archivi Git.

Se si ricorda l&#39;esempio della teorica WKND Travel and Adventure Enterprises, che è un locatario che si concentra sui media relativi ai viaggi, potrebbero avere due programmi: un programma Sites per la divisione WKND Magazine e un programma Assets per la divisione WKND Media. Ogni programma avrà probabilmente un paio di ambienti, ad esempio un ambiente di produzione che serve il traffico effettivo del sito e un ambiente di sviluppo per testare il nuovo codice dell&#39;applicazione.

Esistono tre diversi tipi di ambienti:

* **Produzione e stage** - Gli ambienti di produzione e di staging sono disponibili come coppia e sono utilizzati rispettivamente a scopo di produzione e di test.
* **Sviluppo** - È possibile creare un ambiente di sviluppo a scopo di sviluppo e test e associarlo solo alle pipeline non di produzione.

Ai fini di questo percorso di onboarding, creerai un ambiente di sviluppo.

## Creare ambienti {#creating-environments}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma per il quale desideri aggiungere un ambiente.

1. Da **Panoramica del programma** pagina, fai clic su **Aggiungi ambiente** sulla **Ambienti** per aggiungere un ambiente.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * La **Aggiungi ambiente** è disponibile anche nella **Ambienti** scheda .

      ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * La **Aggiungi ambiente** L’opzione può essere disabilitata a causa di autorizzazioni insufficienti o a seconda delle risorse concesse in licenza.

1. In **Aggiungi ambiente** finestra di dialogo visualizzata:

   * Seleziona un **Tipo di ambiente**.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dietro il tipo di ambiente di sviluppo.
   * Fornisci un **Nome dell&#39;ambiente**.
   * Fornisci un **Descrizione dell&#39;ambiente**.
   * Seleziona una **Area cloud**.

   ![Finestra di dialogo Aggiungi ambiente](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Fai clic su **Salva** per aggiungere l&#39;ambiente specificato.

Una volta disponibile l’ambiente, i membri dell’organizzazione vengono assegnati al **Sviluppatore** il profilo di prodotto può accedere a Cloud Manager e gestire gli archivi Git di Cloud Manager.

## Novità {#whats-next}

Dopo aver letto questa parte del percorso di onboarding, dovresti:

* Comprendere cos&#39;è un ambiente.
* Scopri la differenza tra i diversi ambienti.
* Puoi creare il tuo ambiente.

Le risorse cloud sono state create e sono pronte per essere accessibili dal team. In qualità di amministratore di sistema, devi innanzitutto assegnare i membri del team a AEM profili di prodotto as a Cloud Service da Adobe Admin Console per consentire loro di accedere a tali risorse.

Pertanto, è necessario continuare il percorso di onboarding rivedendo il documento successivo [Assegnazione di membri del team a AEM profili di prodotto as a Cloud Service.](assign-profiles-aem.md)  In questo documento verrà illustrato come concedere ai membri del team i diritti necessari per accedere ai nuovi ambienti.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) - Scopri i tipi di ambienti che puoi creare e come crearli per il progetto Cloud Manager
* [Utilizzo di Adobe Cloud Manager - Ambienti](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Gli ambienti Cloud Manager sono composti da servizi di authoring, pubblicazione e AEM dispatcher. Scopri in che modo diversi ambienti supportano i ruoli e possono essere coinvolti utilizzando diverse pipeline CI/CD.
