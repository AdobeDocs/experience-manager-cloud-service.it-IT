---
title: Gestione degli ambienti
description: Scopri i tipi di ambienti che puoi creare per il tuo progetto Cloud Manager e come farlo.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 72%

---


# Gestione degli ambienti {#managing-environments}

Scopri i tipi di ambienti che puoi creare per il tuo progetto Cloud Manager e come farlo.

## Tipi di ambienti {#environment-types}

L’utente con le autorizzazioni necessarie può creare i seguenti tipi di ambienti (entro i limiti delle opzioni disponibili per il tenant specifico).

* **Produzione e staging**: gli ambienti di produzione e staging sono disponibili in coppia e sono rispettivamente utilizzati a scopo di produzione e di test.

* **Sviluppo**: è possibile creare un ambiente di sviluppo sia per scopi di sviluppo che per scopi di test e associarlo solo a pipeline non destinate alla produzione.

* **Sviluppo rapido**: un ambiente di sviluppo rapido (RDE, Rapid Development Environment) consente allo sviluppatore di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale. Consulta [la documentazione sull’ambiente di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md) per ottenere informazioni dettagliate sull’utilizzo di un ambiente di sviluppo rapido.

Le funzionalità dei singoli ambienti dipendono dalle soluzioni abilitate nel [programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) di ciascuno di essi.

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/home.md)

>[!NOTE]
>
>Gli ambienti di produzione e staging vengono creati solo in coppia. Non è possibile creare solo un ambiente di staging o solo un ambiente di produzione.

## Aggiunta di un ambiente {#adding-environments}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma al quale desideri aggiungere un ambiente.

1. Per aggiungere un programma, dalla pagina **Panoramica del programma**, accedi alla scheda **Ambienti** e fai clic su **Aggiungi ambiente**.

   ![Scheda Ambienti](assets/no-environments.png)

   * L’opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti**.

     ![Scheda Ambienti](assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente** che viene visualizzata:

   * Seleziona un [**tipo di ambiente**.](#environment-types)
      * Il numero di ambienti disponibili/utilizzati è visualizzato tra parentesi dopo il nome del tipo di ambiente.
   * Specifica il **nome** dell’ambiente.
   * Inserisci la **descrizione** dell’ambiente.
   * Se stai aggiungendo una **Produzione e staging** ambiente, è necessario fornire un nome e una descrizione dell’ambiente sia per gli ambienti di produzione che per quelli di staging.
   * Seleziona un’**area geografica primaria** dal menu a discesa.
      * Tieni presente che questa operazione non può essere modificata una volta creata.
      * A seconda dei diritti disponibili, è possibile configurare [più aree geografiche.](#multiple-regions)

   ![Finestra di dialogo Aggiungi ambiente](assets/add-environment2.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Ora il nuovo ambiente viene visualizzato nella schermata **Panoramica** della scheda **Ambienti**. Ora puoi configurare le pipeline per il nuovo ambiente.

## Più aree geografiche di pubblicazione {#multiple-regions}

Un utente con **Proprietario business** Il ruolo può configurare gli ambienti di produzione e di staging in modo da includere fino a tre aree di pubblicazione aggiuntive oltre all’area primaria. Ulteriori aree geografiche di pubblicazione possono migliorare la disponibilità. Consulta la [Documentazione aggiuntiva sulle aree geografiche di pubblicazione](/help/operations/additional-publish-regions.md) per ulteriori dettagli.

>[!TIP]
>
>È possibile utilizzare [API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments) per eseguire una query su un elenco corrente di aree disponibili.

### Aggiunta di più aree di pubblicazione a un nuovo ambiente {#add-regions}

Quando aggiungi un nuovo ambiente, puoi scegliere di configurare altre aree oltre all’area principale.

1. Seleziona la **Area geografica primaria**.
   * Tieni presente che questo non può essere modificato dopo la creazione dell’ambiente.
1. Seleziona l’opzione **Aggiungi altre aree geografiche di pubblicazione** e un nuovo **Aree geografiche di pubblicazione aggiuntive** viene visualizzato un elenco a discesa.
1. In **Aree geografiche di pubblicazione aggiuntive** , selezionare un&#39;area aggiuntiva.
1. L’area selezionata viene aggiunta sotto il menu a discesa per indicarne la selezione.
   * Tocca o fai clic sulla X accanto all’area selezionata per deselezionarla.
1. Seleziona un’altra regione dal menu **Aree geografiche di pubblicazione aggiuntive** per aggiungere un’altra area geografica.
1. Tocca o fai clic su **Salva** quando sei pronto per creare l’ambiente.

![Selezione di più aree geografiche](assets/select-multiple-regions.png)

Le aree selezionate verranno applicate agli ambienti di produzione e di staging.

Se non si specifica alcuna area aggiuntiva, [puoi farlo in un secondo momento dopo la creazione degli ambienti.](#edit-regions)

Se desideri effettuare il provisioning [rete avanzata](/help/security/configuring-advanced-networking.md) Per il programma, si consiglia di eseguire questa operazione prima di aggiungere ulteriori aree di pubblicazione agli ambienti utilizzando l’API di Cloud Manager. In caso contrario, il traffico aggiuntivo delle aree di pubblicazione passerà attraverso il proxy dell’area primaria.

### Modifica di più aree di pubblicazione {#edit-regions}

Se inizialmente non hai specificato altre aree, puoi farlo dopo la creazione degli ambienti, se disponi dei diritti necessari.

Puoi anche rimuovere altre aree geografiche di pubblicazione. Tuttavia, è possibile aggiungere o rimuovere solo aree in una transazione. Se è necessario aggiungere una regione e rimuoverla, aggiungere, salvare la modifica e quindi rimuovere (o viceversa).

1. Dalla console Panoramica programma del programma, fai clic sul pulsante con i puntini di sospensione corrispondente all’ambiente di produzione e seleziona **Modifica** dal menu.

   ![Modifica ambiente](assets/select-edit-environment.png)

1. In **Modifica ambiente di produzione** , apportare le modifiche necessarie alle aree di pubblicazione aggiuntive.
   * Utilizza il **Aree geografiche di pubblicazione aggiuntive** per selezionare altre aree geografiche.
   * Fai clic sulla X accanto alle aree di pubblicazione aggiuntive selezionate per deselezionarle.

   ![Modifica ambiente](assets/edit-environment.png)

1. Tocca o fai clic su **Salva** per salvare le modifiche.

Le modifiche apportate all’ambiente di produzione verranno applicate sia agli ambienti di produzione che a quelli di staging. Le modifiche apportate a più aree di pubblicazione possono essere modificate solo nell’ambiente di produzione.

Se desideri effettuare il provisioning [rete avanzata](/help/security/configuring-advanced-networking.md) per il programma, si consiglia di eseguire questa operazione prima di aggiungere ulteriori aree di pubblicazione agli ambienti. In caso contrario, il traffico aggiuntivo delle aree di pubblicazione passerà attraverso il proxy dell’area primaria.

## Dettagli dell’ambiente {#viewing-environment}

La scheda **Ambienti** nella pagina della panoramica consente di accedere ai dettagli di un ambiente in due modi.

1. Dalla pagina **Panoramica**, fai clic sulla scheda **Ambienti** nella parte superiore della schermata.

   ![Scheda Ambienti](assets/environments-tab2.png)

   * In alternativa, per passare direttamente alla scheda **Ambienti**, fai clic sul pulsante **Mostra tutto** nella scheda **Ambienti**.

     ![Opzione Mostra tutto](assets/environment-showall.png)

1. La scheda **Ambienti** apre ed elenca tutti gli ambienti del programma.

   ![Scheda Ambienti](assets/environment-view-2.png)

1. Fai clic su un ambiente dell’elenco per visualizzarne i dettagli.

   ![Dettagli dell’ambiente](assets/environ-preview1.png)

In alternativa, fai clic sul pulsante con i puntini di sospensione dell’ambiente desiderato, quindi seleziona **Visualizza dettagli**.

![Visualizza dettagli ambiente](assets/view-environment-details.png)

>[!NOTE]
>
>Nella scheda **Ambienti** sono elencati solo tre ambienti. Per visualizzare tutti gli ambienti del programma, fai clic sul pulsante **Mostra tutto** come descritto in precedenza.

### Accesso al servizio di anteprima {#access-preview-service}

Cloud Manager fornisce un servizio di anteprima (fornito come servizio di pubblicazione aggiuntivo) per ogni ambiente di AEM as a Cloud Service.

Con il servizio puoi visualizzare in anteprima l’esperienza finale di un sito web prima di aggiungerla all’ambiente di pubblicazione effettivo e renderla disponibile agli utenti.

Al momento della creazione, al servizio di anteprima viene applicato un elenco IP consentiti predefinito, denominato `Preview Default [<envId>]`, che blocca tutto il traffico verso il servizio. Per abilitare l’accesso, rimuovi l’elenco consentiti IP predefinito dal servizio di anteprima.

![Servizio di anteprima e relativo elenco Consentiti](assets/preview-ip-allow.png)

Per garantire l’accesso, prima di condividere l’URL del servizio di anteprima, l’utente con le autorizzazioni necessarie deve completare i passaggi seguenti.

1. Crea un elenco IP consentiti appropriato, applicalo al servizio di anteprima e rimuovi immediatamente l’elenco Consentiti `Preview Default [<envId>]`.

   * Per ulteriori informazioni, consulta il documento [Applicazione e rimozione degli elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md).

1. Rimuovi l’IP predefinito e aggiungi gli IP appropriati con il flusso di lavoro per l’aggiornamento dell’**elenco IP consentiti**. Per ulteriori informazioni, consulta [Gestione degli elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md).

Una volta sbloccato l’accesso al servizio di anteprima, l’icona a forma di lucchetto che precede il relativo nome non verrà più visualizzata.

Dopo l’attivazione puoi pubblicare il contenuto nel servizio di anteprima tramite l’interfaccia utente Gestisci pubblicazione in AEM. Per ulteriori informazioni, consulta il documento [Anteprima del contenuto](/help/sites-cloud/authoring/fundamentals/previewing-content.md).

>[!NOTE]
>
>La versione dell’ambiente deve essere AEM `2021.05.5368.20210529T101701Z` o più recente per utilizzare il servizio di anteprima. Per eseguire l’operazione, assicurati che nell’ambiente sia stata eseguita correttamente una pipeline di aggiornamento.

## Aggiornamento degli ambienti {#updating-dev-environment}

Come servizio nativo per il cloud, Adobe gestisce automaticamente gli aggiornamenti degli ambienti di staging e produzione all’interno dei programmi di produzione.

Tuttavia, gli aggiornamenti degli ambienti di sviluppo e degli ambienti nei programmi sandbox vengono gestiti internamente ai programmi. Se in tale ambiente non è in esecuzione l’ultima versione di AEM disponibile pubblicamente, lo stato nella scheda **Ambienti** della schermata **Panoramica** del programma indica **Aggiornamento disponibile**.

![Stato dell’aggiornamento dell’ambiente](assets/environ-update.png)

### Aggiornamenti e pipeline {#updates-pipelines}

Le pipeline sono l’unico modo per [distribuire il codice negli ambienti di AEM as a Cloud Service.](deploy-code.md) Per questo motivo, ogni pipeline è associata a una particolare versione di AEM.

Se Cloud Manager rileva che è disponibile una versione di AEM più recente rispetto all’ultima distribuita con la pipeline, viene visualizzato lo stato **Aggiornamento disponibile** per l’ambiente.

Il processo di aggiornamento è quindi articolato in due fasi:

1. Aggiornamento della pipeline all’ultima versione di AEM
1. Esecuzione della pipeline per distribuire la nuova versione di AEM in un ambiente

### Aggiornamento degli ambienti {#updating-your-environments}

Per gli ambienti di sviluppo e gli ambienti nei programmi sandbox, facendo clic sul pulsante con i puntini di sospensione nella scheda **Ambienti** è disponibile l’opzione **Aggiorna**.

![Opzione Aggiorna dalla scheda Ambienti](assets/environ-update2.png)

L’opzione è disponibile anche facendo clic sulla scheda **Ambienti** del programma e selezionando il pulsante con i puntini di sospensione corrispondente all’ambiente.

![Opzione Aggiorna dalla scheda Ambienti](assets/environ-update3.png)

Con quest’opzione, l’utente con il ruolo **Responsabile dell’implementazione** può aggiornare alla versione di AEM più recente la pipeline associata a questo ambiente.

Dopo aver aggiornato la pipeline alla versione di AEM più recente disponibile al pubblico, viene richiesto di eseguire la pipeline associata per distribuire la suddetta versione nell’ambiente.

![Richiesta di esecuzione della pipeline per aggiornare l’ambiente](assets/update-run-pipeline.png)

Il comportamento dell’opzione **Aggiorna** varia a seconda della configurazione e dello stato corrente del programma.

* Se la pipeline è già stata aggiornata, l’opzione **Aggiorna** richiede all’utente di eseguire la pipeline.
* Se l’aggiornamento della pipeline è già in corso, l’opzione **Aggiorna** informa l’utente circa la presenza di un aggiornamento in corso.
* Se non esiste una pipeline appropriata, l’opzione **Aggiorna** richiede all’utente di crearne una.

## Eliminazione degli ambienti di sviluppo {#deleting-environment}

L’utente con l’autorizzazione necessaria è in grado di eliminare un ambiente di sviluppo.

Dalla schermata **Panoramica** del programma, accedi alla scheda **Ambienti** e fai clic sul pulsante con i puntini di sospensione corrispondente all’ambiente che desideri eliminare.

![Opzione Elimina](assets/environ-delete.png)

L’opzione Elimina è disponibile anche dalla scheda **Ambienti** della finestra **Panoramica** del programma. Fai clic sul pulsante con i puntini di sospensione corrispondente all’ambiente e seleziona **Elimina**.

![Opzione Elimina dalla scheda Ambienti](assets/environ-delete2.png)

>[!NOTE]
>
>* Non è possibile eliminare gli ambienti di produzione e di staging creati in un programma di produzione.
>* È possibile eliminare gli ambienti di produzione e di staging contenuti in un programma sandbox.

## Gestione dell’accesso {#managing-access}

Dal menu con i puntini di sospensione dell’ambiente nella scheda **Ambienti**, seleziona **Gestisci accesso**. Puoi accedere direttamente all’istanza di authoring e gestire l’accesso all’ambiente.

![Opzione Gestisci accesso](assets/environ-access.png)

>[!TIP]
>
>Consulta il documento [Profili di prodotto e team as a Cloud Service AEM](/help/onboarding/aem-cs-team-product-profiles.md) per scoprire come i profili di prodotto e team as a Cloud Service per l’AEM possono concedere e limitare l’accesso alle soluzioni Adobe con licenza.

## Accesso a Console sviluppatori {#accessing-developer-console}

Dal menu con i puntini di sospensione dell’ambiente nella scheda **Ambienti**, seleziona **Console sviluppatori**. Si apre una nuova scheda nel browser con la pagina di accesso a **Console sviluppatori**.

![](assets/environ-devconsole.png)

Solo gli utenti con il ruolo **Sviluppatore** possono accedere a **Console sviluppatori**. Tuttavia, per i programmi sandbox, tutti gli utenti con accesso al programma sandbox hanno accesso a **Console sviluppatori**.

Per ulteriori informazioni, consulta il documento [Sospensione e riattivazione degli ambienti sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html?lang=it#hibernating-introduction).

Questa opzione è disponibile anche nella scheda **Ambiente** della finestra **Panoramica**, facendo clic sul menu con i puntini di sospensione dell’ambiente di interesse.

## Accesso locale {#login-locally}

Per accedere a Adobe Experience Manager a livello locale, fai clic sul menu con i puntini di sospensione dell’ambiente nella scheda **Ambienti** e seleziona **Accesso locale**.

![Accesso locale](assets/environ-login-locally.png)

È possibile accedere a livello locale anche dalla scheda **Ambienti** della pagina **Panoramica**.

![Accesso locale dalla scheda Ambienti](assets/environ-login-locally-2.png)

## Gestione dei nomi di dominio personalizzati {#manage-cdn}

I nomi di dominio personalizzati sono supportati in Cloud Manager per i programmi Sites, sia per i servizi di pubblicazione sia per quelli di anteprima. Ogni ambiente di Cloud Manager può ospitare fino a un massimo di 250 domini personalizzati.

Per configurare i nomi di dominio personalizzati, accedi alla scheda **Ambienti** e fai clic su un ambiente per visualizzare i relativi dettagli.

![Dettagli dell’ambiente](assets/domain-names.png)

Nell’ambito del servizio di pubblicazione dell’ambiente, è possibile eseguire le azioni indicate di seguito.

* [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Controllo dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) o di un [certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Gestione degli elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Gestione degli elenchi IP consentiti {#manage-ip-allow-lists}

Gli elenchi IP consentiti sono supportati in Cloud Manager per i servizi di Author, Publish e anteprima dei programmi Sites.

Per gestire gli elenchi IP consentiti, accedi alla scheda **Ambienti** della pagina **Panoramica** del programma. Fai clic su un ambiente per gestire i relativi dettagli.

### Applicazione di un elenco IP consentiti {#apply-ip-allow-list}

Applicando un elenco IP consentiti, tutti gli intervalli IP inclusi nella definizione dell’elenco vengono associati a un servizio Author o Publish in un ambiente. Un utente in **Proprietario business** o **Responsabile dell’implementazione** Per applicare un elenco consentiti IP, il ruolo deve aver effettuato l’accesso.

L’elenco consentiti IP deve esistere in Cloud Manager per applicarlo a un ambiente. Per ulteriori informazioni sugli elenchi IP consentiti in Cloud Manager, consulta il documento [Introduzione agli elenchi IP consentiti in Cloud Manager.](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

Per applicare un elenco IP consentiti, segui la procedura riportata di seguito.

1. Dalla scheda **Ambienti** della schermata **Panoramica** del programma, accedi all’ambiente specifico e seleziona la tabella **Elenco IP consentiti**.
1. Seleziona l’elenco IP consentiti e il servizio Author o Publish che desideri applicare con i campi di immissione nella parte superiore della tabella Elenco IP consentiti.
1. Fai clic su **Applica** e conferma quanto inserito.

### Rimozione di un elenco IP consentiti {#unapply-ip-allow-list}

Rimuovendo un elenco IP consentiti, tutti gli intervalli IP inclusi nella definizione dell’elenco vengono rimossi da un servizio Author o Publish in un ambiente. Un utente in **Proprietario business** o **Responsabile dell’implementazione** Per rimuovere un elenco consentiti IP, è necessario che il ruolo abbia eseguito l’accesso.

Per rimuovere un elenco IP consentiti, segui la procedura riportata di seguito.

1. Dalla scheda **Ambienti** della schermata **Panoramica** del programma, accedi all’ambiente specifico e seleziona la tabella **Elenco IP consentiti**.
1. Individua la riga corrispondente alla regola dell’elenco IP consentiti che desideri rimuovere.
1. Seleziona il pulsante con i puntini di sospensione alla fine della riga.
1. Seleziona **Annulla applicazione** e conferma quanto inserito.
