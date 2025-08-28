---
title: Creazione di ambienti
description: Scopri come creare i primi ambienti con Cloud Manager.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
feature: Onboarding
source-git-commit: 9c5838a01ceecf094aea19578e6560a5e5ca8c4c
workflow-type: ht
source-wordcount: '775'
ht-degree: 100%

---

# Creare gli ambienti {#create-environments}

In questa sezione del [percorso di onboarding](overview.md) scoprirai come creare i primi ambienti con Cloud Manager.

## Obiettivo {#objective}

Dopo aver letto il documento precedente di questo percorso di onboarding, [Creazione di programmi](create-program.md), ora disponi di un programma di Cloud Manager personale. Ora puoi scoprire come utilizzare Cloud Manager e creare i primi ambienti per tale programma.

Dopo aver letto questo documento:

* Saprai che cos’è un ambiente.
* Conoscerai la differenza tra i diversi ambienti.
* Sarai in grado di creare un ambiente personalizzato.

## Che cos’è un ambiente? {#environments}

Nella gerarchia di Cloud Manager, gli ambienti si trovano al di sotto dei programmi. Mentre i programmi consentono di organizzare la soluzione e concedere l’accesso a determinati membri del gruppo, gli ambienti appartengono a programmi specifici e rappresentano istanze individuali delle soluzioni Adobe all’interno di tali programmi. Gli ambienti si utilizzano per uno scopo specifico, ad esempio per l’authoring dei contenuti o i test di nuovi sviluppi. Le pipeline CI/CD di Cloud Manager facilitano la distribuzione del codice in questi ambienti dagli archivi Git.

Se ricordi l’esempio teorico di WKND Travel and Adventure Enterprises, un tenant che si occupa di media legati ai viaggi. Potrebbe disporre di due programmi. Ovvero, un programma Sites per la divisione WKND Magazine e un programma Assets per la divisione WKND Media. In ogni programma sono spesso presenti due ambienti, ad esempio un ambiente di produzione per il traffico effettivo del sito e un ambiente di sviluppo per i test del nuovo codice dell’applicazione.

Esistono cinque diversi tipi di ambienti:

* **Produzione e staging**: gli ambienti di produzione e staging sono disponibili in coppia e vengono utilizzati rispettivamente a scopi di produzione e test.
* **Sviluppo**: è possibile creare un ambiente di sviluppo sia per scopi di sviluppo che per scopi di test, che può essere associato solo a pipeline non destinate alla produzione.
* **Sviluppo rapido**: un ambiente di sviluppo rapido (RDE) consente a uno sviluppatore di distribuire e rivedere le modifiche rapidamente. Riduce al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale.
* **Ambiente di test specializzato**: fornisce uno spazio dedicato per convalidare le funzionalità in condizioni di produzione vicine, ideale per i test di stress e i controlli avanzati di pre-distribuzione.

Ai fini di questo percorso di onboarding, per iniziare in modo basilare puoi creare un ambiente di sviluppo da utilizzare per esplorare le funzionalità di AEM as a Cloud Service.

## Creare un ambiente {#creating-environments}

>[!NOTE]
>
>Il sistema registra come creatore l’utente che crea un ambiente. Poiché a volte è possibile ripristinare gli utenti eliminati, scegli con attenzione il creatore dell’ambiente.

**Per creare un pubblico:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Seleziona il programma al quale desideri aggiungere un ambiente.

1. Per aggiungere un ambiente, dalla pagina **Panoramica del programma**, nella scheda **Ambienti**, seleziona l’opzione **Aggiungi ambiente**.

   ![Scheda Ambienti](/help/implementing/cloud-manager/assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

     ![Scheda Ambienti](/help/implementing/cloud-manager/assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente**, esegui le operazioni seguenti:

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

Il team può ora accedere alle risorse cloud create. In qualità di amministratore di sistema, devi innanzitutto assegnare i membri del team ai profili di prodotto in AEM as a Cloud Service da Adobe Admin Console in modo che possano accedere a tali risorse.

Pertanto, prima di continuare il percorso di onboarding, rivedi il documento [Assegnazione dei membri del team ai profili di prodotto di AEM as a Cloud Service](assign-profiles-aem.md). Nel documento scopri come concedere ai membri del team i diritti sui nuovi ambienti.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md): scopri di più sui tipi di ambiente che è possibile creare e come crearli per un progetto di Cloud Manager.
* [Utilizzo degli ambienti di Adobe Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/cloud-manager/environments): gli ambienti di Cloud Manager sono composti dai servizi di authoring, pubblicazione e Dispatcher di AEM. Scopri in che modo i diversi ambienti supportano i ruoli e possono essere utilizzati tramite pipeline CI/CD differenti.
* [Ambienti di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md) (RDE, Rapid Development Environment): consulta la documentazione per informazioni dettagliate sull’utilizzo di un RDE.
<!-- ERROR: Not Found (HTTP error 404) FIND AN ALTERNATE RESOURCE? * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

