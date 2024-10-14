---
title: Gestire gli ambienti
description: Scopri i tipi di ambienti che puoi creare per il tuo progetto Cloud Manager e come farlo.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 62%

---


# Gestire gli ambienti {#managing-environments}

Scopri i tipi di ambienti che puoi creare per il tuo progetto Cloud Manager e come farlo.

## Tipi di ambiente {#environment-types}

L’utente con le autorizzazioni necessarie può creare i seguenti tipi di ambienti (entro i limiti delle opzioni disponibili per il tenant specifico).

* **Produzione + Staging** - Gli ambienti di produzione e staging sono disponibili in coppia e vengono utilizzati rispettivamente a scopo di produzione e test. Esecuzione di test di prestazioni e sicurezza nell&#39;ambiente stage. Ha le stesse dimensioni della produzione.

* **Sviluppo** - È possibile creare un ambiente di sviluppo per scopi di sviluppo e test e associarlo solo a pipeline non di produzione.  Gli ambienti di sviluppo non hanno le stesse dimensioni di quelli di staging e produzione e non devono essere utilizzati per eseguire test di prestazioni e sicurezza.

* **Sviluppo rapido**: un ambiente di sviluppo rapido (RDE, Rapid Development Environment) consente allo sviluppatore di implementare e rivedere rapidamente le modifiche, riducendo al minimo il tempo necessario per testare le funzioni che hanno dimostrato di funzionare in un ambiente di sviluppo locale. Consulta [la documentazione sull’ambiente di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md) per ottenere informazioni dettagliate sull’utilizzo di un RDE.

Le funzionalità dei singoli ambienti dipendono dalle soluzioni abilitate nel [programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) di ciascuno di essi.

* [Sites](/help/overview/introduction.md)
* [Assets](/help/assets/overview.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/introduction/introduction.md)

>[!NOTE]
>
>Gli ambienti di produzione e staging vengono creati solo in coppia. Non è possibile creare solo un ambiente di staging o solo un ambiente di produzione.

## Aggiungere un ambiente {#adding-environments}

Per aggiungere o modificare un ambiente, un utente deve essere membro del ruolo **Proprietario business**.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** fare clic sul programma per il quale si desidera aggiungere un ambiente.

1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, fai clic su **Aggiungi ambiente** nella scheda **Ambienti** per aggiungere un ambiente.

   ![Scheda Ambienti](assets/no-environments.png)

   * L&#39;opzione **Aggiungi ambiente** è disponibile anche nella scheda ![Icona dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**.

     ![Scheda Ambienti](assets/environments-tab.png)

   * L’opzione **Aggiungi ambiente** potrebbe essere disattivata per mancanza di autorizzazioni o a seconda delle risorse concesse in licenza.

1. Nella finestra di dialogo **Aggiungi ambiente**:

   * Selezionare un tipo di ambiente [****](#environment-types).
      * Il numero di ambienti disponibili/utilizzati è visualizzato tra parentesi dopo il nome del tipo di ambiente.
   * Specifica il **nome** dell’ambiente.
      * Una volta creato l’ambiente, non è possibile modificarne il nome.
   * Inserisci la **descrizione** dell’ambiente.
   * Se stai aggiungendo un ambiente di **produzione e fase**, è necessario fornire un nome ambiente e una descrizione sia per l’ambiente di produzione che per quello di staging.
   * Seleziona un’**area geografica primaria** dal menu a discesa.
      * Dopo la creazione, non è possibile modificare l’area geografica primaria.
      * A seconda dei diritti disponibili, è possibile configurare [più aree geografiche](#multiple-regions).

   ![Finestra di dialogo Aggiungi ambiente](assets/add-environment2.png)

1. Per aggiungere l’ambiente specificato, fai clic su **Salva**.

Ora il nuovo ambiente viene visualizzato nella schermata **Panoramica** della scheda **Ambienti**. Ora puoi configurare le pipeline per il nuovo ambiente.

## Più aree geografiche di pubblicazione {#multiple-regions}

Un utente con il ruolo di **Proprietario business** può configurare gli ambienti di produzione e di staging in modo da includere fino a tre aree geografiche di pubblicazione aggiuntive, oltre all’area geografica primaria. Aree geografiche di pubblicazione aggiuntiva possono migliorare la disponibilità. Consulta la [Documentazione sulle aree geografiche di pubblicazione aggiuntiva](/help/operations/additional-publish-regions.md) per ulteriori dettagli.

>[!TIP]
>
>Puoi utilizzare l’[API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments.it) per eseguire una query su un elenco corrente di aree geografiche disponibili.

### Aggiungere più aree geografiche di pubblicazione a un nuovo ambiente {#add-regions}

Quando aggiungi un nuovo ambiente, puoi scegliere di configurare aree geografiche aggiuntive oltre all’area geografica primaria.

1. Seleziona l’**Area geografica principale**.
   * Dopo la creazione dell’ambiente, non è possibile modificare l’area geografica primaria.
1. Seleziona l’opzione **Aggiungi aree geografiche di pubblicazione aggiuntive**. In questo modo verrà visualizzato un nuovo menu a discesa **Aree geografiche di pubblicazione aggiuntive**.
1. Nel menu a discesa **Aree geografiche di pubblicazione aggiuntive**, seleziona un’area geografica aggiuntiva.
1. L’area geografica selezionata viene aggiunta sotto il menu a discesa per indicarne la selezione.
   * Selezionare `X` accanto all&#39;area selezionata per deselezionarla.
1. Seleziona un’altra area geografica dal menu a discesa **Aree geografiche di pubblicazione aggiuntiva** per aggiungere un’altra area geografica.
1. Seleziona **Salva** quando sei pronto per creare il tuo ambiente.

![Selezionare più aree geografiche](assets/select-multiple-regions.png)

Le aree geografiche selezionate verranno applicate agli ambienti di produzione e di staging.

Se non si specificano altre aree, [sarà possibile farlo in seguito dopo la creazione degli ambienti](#edit-regions).

Se desideri effettuare il provisioning di [rete avanzata](/help/security/configuring-advanced-networking.md) per il programma, si consiglia di eseguire questa operazione prima di aggiungere aree geografiche di pubblicazione aggiuntiva agli ambienti utilizzando API di Cloud Manager. In caso contrario, il traffico delle aree geografiche di pubblicazione aggiuntiva passerà attraverso il proxy dell’area geografica principale.

### Modificare più aree geografiche di pubblicazione {#edit-regions}

Se inizialmente non hai specificato aree geografiche aggiuntive, puoi farlo dopo la creazione degli ambienti, se disponi dei diritti necessari.

Puoi anche rimuovere le aree geografiche di pubblicazione aggiuntiva. Tuttavia, in un’unica operazione puoi solo aggiungere o solo rimuovere le aree geografiche. Se è necessario aggiungere un’area geografica e rimuoverne un’altra, per prima cosa aggiungi, salva la modifica e quindi rimuovi (o viceversa).

1. Dalla console Panoramica programma del programma, fai clic su https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg per l&#39;ambiente di produzione e seleziona **Modifica** dal menu.

   ![Modifica ambiente](assets/select-edit-environment.png)

1. Nella finestra di dialogo **Modifica ambiente di produzione**, apporta le modifiche necessarie alle aree geografiche di pubblicazione aggiuntiva.
   * Utilizza il menu **Aree geografiche di pubblicazione aggiuntiva** per selezionare altre aree geografiche.
   * Fai clic sulla X accanto alle aree geografiche di pubblicazione aggiuntiva selezionate per deselezionarle.

   ![Modifica ambiente](assets/edit-environment.png)

1. Seleziona **Salva** per salvare le modifiche.

Le modifiche apportate all’ambiente di produzione verranno applicate sia agli ambienti di produzione che a quelli di staging. Le modifiche apportate a più aree geografiche di pubblicazione possono essere modificate solo nell’ambiente di produzione.

Se desideri effettuare il provisioning di [rete avanzata](/help/security/configuring-advanced-networking.md) per il programma, si consiglia di eseguire questa operazione prima di aggiungere aree geografiche di pubblicazione aggiuntiva negli ambienti. In caso contrario, il traffico delle aree geografiche di pubblicazione aggiuntive passerà attraverso il proxy dell’area geografica principale.

## Dettagli dell’ambiente {#viewing-environment}

Dalla pagina **Panoramica** è possibile accedere ai dettagli di un ambiente in due modi.

1. Dalla pagina **Panoramica**, fai clic sulla scheda **Ambienti** nel menu a sinistra.

   ![Scheda Ambienti](assets/environments-tab2.png)

   * In alternativa, per passare direttamente alla scheda **Ambienti**, fai clic sul pulsante **Mostra tutto** nella scheda **Ambienti**.

     ![Opzione Mostra tutto](assets/environment-showall.png)

1. La scheda **Ambienti** apre ed elenca tutti gli ambienti del programma.

   ![Scheda Ambienti](assets/environments-tab2.png)

1. Fai clic su un ambiente dell’elenco per visualizzarne i dettagli.

   ![Dettagli dell’ambiente](assets/environ-preview1.png)

In alternativa, fare clic su https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg dell&#39;ambiente desiderato, quindi selezionare **Visualizza dettagli**.

![Visualizza dettagli ambiente](assets/view-environment-details.png)

>[!NOTE]
>
>Nella scheda **Ambienti** sono elencati solo tre ambienti. Per visualizzare tutti gli ambienti del programma, fai clic sul pulsante **Mostra tutto** come descritto in precedenza.

### Accedere al servizio di anteprima {#access-preview-service}

Cloud Manager fornisce un servizio di anteprima (fornito come servizio di pubblicazione aggiuntivo) per ogni ambiente di AEM as a Cloud Service.

Con il servizio puoi visualizzare in anteprima l’esperienza finale di un sito web prima di aggiungerla all’ambiente di pubblicazione effettivo e renderla disponibile agli utenti.

Al momento della creazione, al servizio di anteprima viene applicato un elenco Consentiti IP predefinito, denominato `Preview Default [<envId>]`, che blocca tutto il traffico verso il servizio. Per abilitare l’accesso, annulla l’applicazione dell’elenco Consentiti IP predefinito dal servizio di anteprima.

![Servizio di anteprima e relativo elenco Consentiti](assets/preview-ip-allow.png)

Per garantire l’accesso al servizio di anteprima, l’utente con le autorizzazioni necessarie deve completare i passaggi seguenti prima di condividere l’URL del servizio.

1. Crea un elenco Consentiti IP appropriato, applicaro al servizio di anteprima e annulla immediatamente l’applicazione l’elenco Consentiti `Preview Default [<envId>]`.

   * Consulta [Applicazione e rimozione di Elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) per ulteriori dettagli.

1. Per rimuovere l’IP predefinito e aggiungere gli IP appropriati, usa il flusso di lavoro per l’aggiornamento dell’**elenco IP consentiti**. Per ulteriori informazioni, vedi [Gestione degli elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md).

Dopo aver sbloccato l’accesso al servizio di anteprima, l’icona a forma di lucchetto che precede il relativo nome non verrà più visualizzata.

Dopo l’attivazione puoi pubblicare il contenuto nel servizio di anteprima tramite l’interfaccia utente Gestisci pubblicazione in AEM. Per ulteriori dettagli vedi [Anteprima del contenuto](/help/sites-cloud/authoring/sites-console/previewing-content.md).

>[!NOTE]
>
>La versione dell’ambiente deve essere AEM `2021.05.5368.20210529T101701Z` o più recente per utilizzare il servizio di anteprima. Assicurati che una pipeline di aggiornamento sia stata eseguita correttamente nell’ambiente in uso, in modo da poter utilizzare il servizio di anteprima.

### Stato di altre aree geografiche di pubblicazione {#additional-region-status}

Se hai attivato altre aree di pubblicazione, puoi controllarne lo stato dalla scheda **Ambienti**.

1. Nella pagina **Panoramica**, individua la scheda **Ambienti**.

1. Nella scheda **Ambienti**, la colonna **Stato** verrà visualizzata in caso di problemi con le aree di pubblicazione aggiuntive configurate. Fai clic sull&#39;icona **Info** per i dettagli delle aree geografiche.

   ![Ulteriori informazioni sullo stato delle aree di pubblicazione nella scheda Ambienti](assets/additional-publish-region-status-environments-card.png)

In alternativa, è possibile accedere alle stesse informazioni dalla scheda **Ambienti**.

1. Nella pagina **Panoramica**, seleziona la scheda **Ambienti**.

1. Nella scheda **Ambienti**, seleziona l&#39;ambiente in cui desideri eseguire la query nel menu a sinistra.

1. Una volta selezionato un ambiente:

   * Nella tabella **Informazioni ambiente** verranno visualizzate le aree configurate per l&#39;ambiente selezionato.
   * La colonna **Stato** della tabella **Segmenti di ambiente** rifletterà in caso di problemi con le aree di pubblicazione aggiuntive configurate. Passa il cursore del mouse sullo stato per visualizzare i dettagli di eventuali problemi.

   ![Ulteriori informazioni sullo stato delle aree di pubblicazione nella scheda Ambienti](assets/additional-publish-region-status-environments-tab.png)

In caso di problemi segnalati con altre aree geografiche di pubblicazione:

1. Siate pazienti. Cloud Manager cerca continuamente di recuperare la regione, che può diventare disponibile in qualsiasi momento.
1. Se il problema persiste dopo diverse ore, puoi rimuovere l’area di pubblicazione aggiuntiva e aggiungerla nuovamente (nella stessa area o in un’altra) per attivare una distribuzione completa.

Il tempo che si attende dal ripristino del sistema prima di intraprendere ulteriori azioni dipende dall&#39;impatto che il guasto di quell&#39;area ha sui sistemi.

In ogni caso, il traffico [viene sempre indirizzato all&#39;altra area più vicina che è online](/help/operations/additional-publish-regions.md). Se continui a visualizzare dei problemi, contatta l’Assistenza clienti di Adobe.

## Aggiornare ambienti {#updating-dev-environment}

In qualità di servizio nativo per il cloud, gli aggiornamenti degli ambienti di sviluppo, staging e produzione all’interno dei programmi di produzione vengono gestiti automaticamente da Adobe.

Tuttavia, gli aggiornamenti degli ambienti nei programmi sandbox vengono gestiti all’interno dei programmi. Se in tale ambiente non è in esecuzione l’ultima versione di AEM disponibile pubblicamente, lo stato nella scheda **Ambienti** della schermata **Panoramica** del programma indica **Aggiornamento disponibile**.

![Stato dell’aggiornamento dell’ambiente](assets/environ-update.png)

### Aggiornamenti e pipeline {#updates-pipelines}

Le pipeline sono l&#39;unico modo per [distribuire il codice negli ambienti di AEM as a Cloud Service](deploy-code.md). Per questo motivo, ogni pipeline è associata a una particolare versione dell’AEM.

Se Cloud Manager rileva che è disponibile una versione di AEM più recente rispetto all’ultima distribuita con la pipeline, viene visualizzato lo stato **Aggiornamento disponibile** per l’ambiente.

Il processo di aggiornamento è quindi articolato in due fasi:

1. Aggiornamento della pipeline all’ultima versione di AEM
1. Esecuzione della pipeline per distribuire la nuova versione di AEM in un ambiente

### Aggiornare gli ambienti {#updating-your-environments}

>[!NOTE]
> A partire dal 2024, le istanze di sviluppo e alcuni programmi sandbox sono già aggiornati automaticamente, pertanto non è necessario gestirne manualmente gli aggiornamenti. In seguito a questa transizione, l&#39;opzione di aggiornamento manuale dell&#39;ambiente per le istanze di sviluppo potrebbe non essere disponibile per _alcuni_ programmi.

L&#39;opzione **Aggiorna** è disponibile nella scheda **Ambienti** per alcuni ambienti di sviluppo e ambienti nei programmi sandbox facendo clic su https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg dell&#39;ambiente.

![Opzione Aggiorna dalla scheda Ambienti](assets/environ-update2.png)

Questa opzione è disponibile anche facendo clic sulla scheda **Ambienti** del programma e quindi su https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg dell&#39;ambiente.

![Opzione Aggiorna dalla scheda Ambienti](assets/environ-update3.png)

Un utente con il ruolo **Responsabile dell&#39;implementazione** o **Proprietario business** può utilizzare questa opzione per aggiornare la pipeline associata a questo ambiente alla versione più recente dell&#39;AEM.

Dopo aver aggiornato la pipeline alla versione di AEM più recente disponibile al pubblico, viene richiesto di eseguire la pipeline associata per distribuire la suddetta versione nell’ambiente.

![Richiesta di esecuzione della pipeline per aggiornare l’ambiente](assets/update-run-pipeline.png)

Il comportamento dell’opzione **Aggiorna** varia a seconda della configurazione e dello stato corrente del programma.

* Se la pipeline è già stata aggiornata, l’opzione **Aggiorna** richiede all’utente di eseguire la pipeline.
* Se l’aggiornamento della pipeline è già in corso, l’opzione **Aggiorna** informa l’utente circa la presenza di un aggiornamento in corso.
* Se non esiste una pipeline appropriata, l&#39;opzione **Aggiorna** richiede di crearne una.

## Eliminazione degli ambienti di sviluppo {#deleting-environment}

Un utente con il ruolo **Responsabile dell&#39;implementazione** o **Proprietario business** è in grado di eliminare un ambiente di sviluppo.

Dalla schermata **Panoramica** del programma nella scheda **Ambienti**, fai clic su https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg dell&#39;ambiente di sviluppo da eliminare.

![Opzione Elimina](assets/environ-delete.png)

L’opzione Elimina è disponibile anche dalla scheda **Ambienti** della finestra **Panoramica** del programma. Fare clic su https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg dell&#39;ambiente e selezionare **Elimina**.

![Opzione Elimina dalla scheda Ambienti](assets/environ-delete2.png)

>[!NOTE]
>
>* Non è possibile eliminare gli ambienti di produzione e di staging creati in un programma di produzione.
>* È possibile eliminare gli ambienti di produzione e di staging contenuti in un programma sandbox.

## Gestisci accesso {#managing-access}

Dal menu con i puntini di sospensione dell’ambiente nella scheda **Ambienti**, seleziona **Gestisci accesso**. Puoi accedere direttamente all’istanza di authoring e gestire l’accesso all’ambiente.

![Opzione Gestisci accesso](assets/environ-access.png)

>[!TIP]
>
>Vedi [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) se desideri scoprire come i team e i profili di prodotto di AEM as a Cloud Service possono concedere e limitare l’accesso alle soluzioni di Adobe con licenza.

## Accedere alla Console per sviluppatori {#accessing-developer-console}

Dal menu con i puntini di sospensione dell’ambiente nella scheda **Ambienti**, seleziona **Console sviluppatori**. Nel browser viene aperta una nuova scheda con la pagina di accesso a **Developer Console**.

![Accedi a Developer Console](assets/environ-devconsole.png)

Solo gli utenti con il ruolo **Sviluppatore** possono accedere a **Developer Console**. Tuttavia, per i programmi sandbox, tutti gli utenti con accesso al programma sandbox hanno accesso a **Developer Console**.

Vedi [Sospensione e riattivazione degli ambienti sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html?lang=it#hibernation) per ulteriori dettagli.

Questa opzione è disponibile anche nella scheda **Ambiente** della finestra **Panoramica**, facendo clic sul menu con i puntini di sospensione dell’ambiente di interesse.

## Accesso locale {#login-locally}

Seleziona **Accesso locale** dal menu con i puntini di sospensione dell&#39;ambiente nella scheda **Ambienti** per accedere localmente a Adobe Experience Manager.

![Accesso locale](assets/environ-login-locally.png)

È possibile accedere a livello locale anche dalla scheda **Ambienti** della pagina **Panoramica**.

![Accesso locale dalla scheda Ambienti](assets/environ-login-locally-2.png)

## Gestire i nomi di dominio personalizzati {#manage-cdn}

I nomi di dominio personalizzati sono supportati in Cloud Manager per i programmi Sites sia per i servizi di pubblicazione che per quelli di anteprima.

>[!TIP]
>
>Per ulteriori informazioni, vedere [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

## Gestire gli elenchi IP consentiti {#manage-ip-allow-lists}

Gli elenchi IP consentiti sono supportati in Cloud Manager per i servizi di authoring, pubblicazione e anteprima dei programmi Sites.

Per gestire gli elenchi IP consentiti, accedi alla scheda **Ambienti** della pagina **Panoramica** del programma. Fai clic su un singolo ambiente per gestirne i dettagli.

### Applicare un Elenco consentiti IP {#apply-ip-allow-list}

L’applicazione di un inserisco nell&#39;elenco Consentiti di consente di associare tutti gli intervalli IP inclusi nella definizione del elenco Consentiti di a un servizio Author o Publish in un ambiente.

>[!TIP]
>
>Per ulteriori informazioni, vedere [Introduzione agli Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).
