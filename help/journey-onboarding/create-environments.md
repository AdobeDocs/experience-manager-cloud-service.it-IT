---
title: Creazione di ambienti
description: Scopri come creare i primi ambienti con Cloud Manager.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 86%

---

# Creazione di ambienti {#create-environments}

In questa sezione del [percorso di onboarding](overview.md) scoprirai come creare i primi ambienti con Cloud Manager.

## Obiettivo {#objective}

Dopo aver letto il documento precedente di questo percorso di onboarding, [Creazione di programmi,](create-program.md) ora disponi di un programma di Cloud Manager personale. Ora puoi scoprire come creare i primi ambienti per tale programma con Cloud Manager.

Dopo aver letto questo documento:

* Saprai che cos’è un ambiente.
* Conoscerai la differenza tra i diversi ambienti.
* Sarai in grado di creare un ambiente personalizzato.

## Che cos’è un ambiente? {#environments}

Nella gerarchia di Cloud Manager, gli ambienti si trovano al di sotto dei programmi. Mentre i programmi consentono di organizzare la soluzione e concedere l’accesso a determinati membri del gruppo, gli ambienti appartengono a programmi specifici e rappresentano istanze individuali delle soluzioni Adobe all’interno di tali programmi. Gli ambienti si utilizzano per uno scopo specifico, ad esempio per l’authoring dei contenuti o i test di nuovi sviluppi. Le pipeline CI/CD di Cloud Manager facilitano la distribuzione del codice in questi ambienti dagli archivi Git.

Richiamando alla memoria l’esempio precedente, l’ipotetica WKND Travel and Adventure Enterprises, un tenant che si occupa di media legati ai viaggi, potrebbe avere due programmi: Sites per la divisione WKND Magazine e Assets per la divisione WKND Media. In ogni programma sono spesso presenti due ambienti, ad esempio un ambiente di produzione per il traffico effettivo del sito e un ambiente di sviluppo per i test del nuovo codice dell’applicazione.

Esistono quattro diversi tipi di ambienti:

* **Produzione e staging**: gli ambienti di produzione e staging sono disponibili in coppia e vengono utilizzati rispettivamente a scopi di produzione e test.
* **Sviluppo**: è possibile creare un ambiente di sviluppo sia per scopi di sviluppo sia per scopi di test e associarlo solo a pipeline non di produzione.
* **Sviluppo rapido**: un ambiente di sviluppo rapido (RDE, Rapid Development Environment) consente allo sviluppatore di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale.

Ai fini di questo percorso di onboarding, per iniziare con un minimo è possibile creare un ambiente di sviluppo da utilizzare per esplorare AEM funzionalità di as a Cloud Service.

## Creazione di ambienti {#creating-environments}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma al quale desideri aggiungere un ambiente.

1. Per aggiungere un programma, dalla pagina **Panoramica del programma**, accedi alla scheda **Ambienti** e fai clic su **Aggiungi ambiente**.

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

Ora che le risorse cloud sono state create, il team è pronto per accedervi. In qualità di amministratore di sistema, devi anzitutto assegnare i membri del gruppo ai profili di prodotto di AEM as a Cloud Service da Adobe Admin Console per consentire loro di accedere alle risorse.

Pertanto, prima di continuare il percorso di onboarding, rivedi il documento [Assegnazione dei membri del gruppo ai profili di prodotto di AEM as a Cloud Service.](assign-profiles-aem.md) Nel documento vengono fornite informazioni su come concedere ai membri del gruppo i diritti necessari per accedere ai nuovi ambienti.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori risorse facoltative, se desideri andare oltre il contenuto del percorso di onboarding.

* [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md): scopri di più sui tipi di ambienti che è possibile creare e come crearli per un progetto di Cloud Manager.
* [Utilizzo degli ambienti di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=it): gli ambienti di Cloud Manager sono composti dai servizi di authoring, pubblicazione e dispatcher di AEM. Scopri in che modo i diversi ambienti supportano i ruoli e come utilizzarli con diverse pipeline CI/CD.
* [Suggerimenti e trucchi per i campioni AEM - Tipi di ambiente per Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Guarda questo video per una panoramica dei tipi di ambiente Cloud Manager da un campione AEM.
* [Ambienti di sviluppo rapidi](/help/implementing/developing/introduction/rapid-development-environments.md) - Vedi questa documentazione per i dettagli su come utilizzare un RDE
