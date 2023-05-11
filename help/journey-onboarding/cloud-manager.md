---
title: Accesso a Cloud Manager
description: Scopri come accedere a Cloud Manager per configurare le risorse del progetto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 95%

---

# Accesso a Cloud Manager {#cloud-resources}

In questa sezione del [percorso di onboarding](overview.md) scoprirai come accedere a Cloud Manager per configurare le risorse del progetto.

## Obiettivo {#objective}

Nell’articolo precedente di questo percorso di onboarding, [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) hai assegnato i ruoli appropriati ai membri del gruppo AEMaaCS. Scopri subito come accedere a Cloud Manager per configurare le risorse del progetto che verranno utilizzate dal team.

Ora che hai completato il passaggio precedente in questo percorso, il team può accedere a Cloud Manager. Cloud Manager consente di creare e gestire le risorse del progetto, come ad esempio programmi e ambienti.

Dopo aver letto questo documento saprai:

* Che l’amministratore di sistema assegnato al ruolo **Proprietario business** deve essere la prima persona dell’organizzazione ad accedere a Cloud Manager.
* Come accedere a Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per il team. Supporta i clienti con configurazioni di sviluppo di livello Enterprise e pipeline CI/CD appositamente progettate per garantire test approfonditi e la massima qualità del codice, in modo da poter offrire esperienze eccezionali. Cloud Manager offre tutti gli strumenti necessari per iniziare a lavorare in autonomia, inclusa la possibilità di creare risorse e ambienti cloud.

In genere chi è assegnato al profilo di prodotto **Proprietario business** è responsabile dell’aggiunta delle risorse cloud, ad esempio programmi e ambienti. Si tratta della persona che, in base alle esigenze aziendali, completa la configurazione iniziale di Cloud Manager.

Ai fini di questo percorso di onboarding, come amministratore di sistema, dovrai aver già assegnato te stesso o te stessa al profilo di prodotto **Proprietario business** e ti occuperai della configurazione delle risorse cloud. A seconda dei requisiti effettivi del progetto, gli utenti con ruolo Proprietario business e Amministratore di sistema possono corrispondere.

## Accesso a Cloud Manager come Amministratore di sistema e Proprietario business {#access-sysadmin-bo}

Prima che i membri del gruppo assegnati al ruolo **Proprietario business** possano accedere a Cloud Manager e iniziare a creare risorse cloud, è necessario assegnare l’amministratore di sistema al ruolo **Proprietario business** e accedere a Cloud Manager come già eseguito nel passaggio precedente di questo percorso di onboarding.

1. Come amministratore di sistema, assicurati di aver assegnato il tuo utente al ruolo **Proprietario business**.

   * Se non l’hai già fatto, torna al passaggio precedente di questo percorso, [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) per ulteriori informazioni su come assegnare il ruolo **Proprietario business** all’amministratore di sistema.

1. Accedi a Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) per visualizzare la normale pagina di destinazione.

Dopo aver effettuato l’accesso come amministratore di sistema con il ruolo **Proprietario business**, hai inizializzato Cloud Manager per l’uso da parte di altri utenti con il ruolo **Proprietario business**. Non riceverai alcuna conferma o messaggio al riguardo. È sufficiente effettuare l’accesso.

Fino a quando non accedi a Cloud Manager come amministratore di sistema con il ruolo **Proprietario business**, gli altri utenti con ruolo **Proprietario business** non potranno creare programmi in Cloud Manager anche se sono stati assegnati ai ruoli corretti.

## Accesso a Cloud Manager {#navigate-cloud-manager}

Gli utenti con il ruolo **Proprietario business** ricevono un’e-mail di benvenuto con un collegamento per iniziare. Per accedere a Cloud Manager da questa e-mail di benvenuto, segui la procedura riportata di seguito.

1. Dall’e-mail di benvenuto, fai clic sul collegamento **Inizia** come mostrato nella figura in basso.
   ![Esempio di e-mail](/help/journey-onboarding/assets/get-started-email.png)

1. Si apre la pagina **Programmi e prodotti** di Cloud Manager.

   >[!TIP]
   >
   >Puoi passare direttamente alla pagina di accesso di Cloud Manager dall’indirizzo `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Aggiungi un segnalibro a questa pagina per riferimenti futuri.

1. Si apre la pagina di destinazione di Cloud Manager.

In alternativa, segui questa procedura per accedere alla pagina **Programmi e prodotti** di Cloud Manager dalla pagina Home di Adobe Experience Cloud.

1. Passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com) e accedi con il tuo Adobe ID.

1. Dalla pagina Home di Adobe Experience Cloud, seleziona **Experience Manager**.

   ![Pagina Home di Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Viene visualizzata la pagina Home di AEM. Da qui, fai clic su **Avvia** dal riquadro **Cloud Manager**.

   ![Pagina Home di AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Dopo aver effettuato correttamente l’accesso, si apre la pagina di destinazione di Cloud Manager. Per ulteriori dettagli, consulta la sezione [Visualizzazione dei programmi di Cloud Manager](#viewing-programs).

La modalità di accesso a programmi e prodotti tramite Cloud Manager è a tua discrezione e non ha alcun effetto su come utilizzi Cloud Manager o come gestisci i programmi.

>[!NOTE]
>
>A seconda dei ruoli assegnati in Cloud Manager e dello stato dell’applicazione, vengono visualizzate diverse schermate durante l’utilizzo dell’interfaccia utente di Cloud Manager.

## Visualizzazione dei programmi {#viewing-programs}

Dopo aver effettuato correttamente l’accesso a Cloud Manager, gli elementi visualizzati dipendono dallo stato dei programmi, come descritto nelle sezioni seguenti.

### In assenza di programmi {#no-programs}

Se nell’organizzazione non sono presenti programmi, la pagina di destinazione ti invita a creare il primo programma.

![Senza programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### In presenza di programmi {#programs-exist}

Se nell’organizzazione sono già presenti dei programmi, nella pagina di destinazione vengono visualizzati i programmi esistenti e un pulsante per aggiungerne di nuovi.

![Con programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### In presenza di programmi e con il ruolo di amministratore di sistema {#programs-exist-sysadmin}

Se nell’organizzazione sono già presenti dei programmi e hai il ruolo di Amministratore di sistema, nella pagina di destinazione viene visualizzato il pulsante **Gestisci accesso** e l’opzione **Aggiungi programma**.

![Vista dell’amministratore di sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifica dei ruoli utente {#verify-user-roles}

Dopo aver effettuato l’accesso a Cloud Manager, puoi verificare che il tuo utente sia stato correttamente assegnato al profilo di prodotto **Proprietario business**.

1. Seleziona il tuo profilo nella parte in alto a destra della finestra.

   ![Profilo utente](/help/journey-onboarding/assets/setup-resources5.png)

1. Per visualizzare i ruoli assegnati al tuo utente, seleziona **Ruoli utente**.

   ![Ruoli utente](/help/journey-onboarding/assets/setup-resources6.png)

1. La finestra di dialogo deve confermare che ti è stato assegnato il ruolo **Proprietario business**.

   ![Elenco dei ruoli utente](/help/journey-onboarding/assets/setup-resources7.png)

Hai completato correttamente l’accesso a Cloud Manager come Proprietario business. Se il tuo utente non è assegnato al ruolo **Proprietario business**, contatta l’amministratore di sistema.

## Passaggio successivo {#whats-next}

Ora che puoi accedere a Cloud Manager come amministratore di sistema, tutto è pronto per creare il primo programma.

Continua il tuo percorso di onboarding passando al documento [Creazione di un programma](create-program.md) per scoprire come farlo.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori risorse facoltative, se desideri andare oltre il contenuto del percorso di onboarding.

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): scopri Cloud Manager, i suoi programmi e gli ambienti che offre.
* [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
* [Suggerimenti e trucchi per AEM Champion - Interfaccia utente di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Guarda questo video per una panoramica dell’interfaccia utente di Cloud Manager da un campione AEM.
