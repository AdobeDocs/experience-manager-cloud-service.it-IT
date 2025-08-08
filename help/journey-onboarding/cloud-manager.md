---
title: Accesso a Cloud Manager
description: Scopri come accedere a Cloud Manager per configurare le risorse del progetto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 4cad0ea1be4cba1c7f1af55cc760fb65fdc3cc4a
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 75%

---

# Accesso a Cloud Manager {#cloud-resources}

In questa sezione del [percorso di onboarding](overview.md) scoprirai come accedere a Cloud Manager per configurare le risorse del progetto.

## Obiettivo {#objective}

Nell’articolo precedente di questo percorso di onboarding, [Assegnazione dei membri del team ai profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md), hai assegnato i ruoli appropriati al team AEMaaCS. Scopri ora come accedere a Cloud Manager per configurare le risorse del progetto che il team intende utilizzare.

Ora che hai completato il passaggio precedente in questo percorso, il team può accedere a Cloud Manager. Cloud Manager viene utilizzato per creare e gestire le risorse del progetto, ad esempio programmi e ambienti.

Dopo aver letto questo documento avrai compreso:

* Che l’amministratore di sistema assegnato al ruolo **Proprietario business** deve essere la prima persona dell’organizzazione ad accedere a Cloud Manager.
* Come accedere a Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per il team. Supporta i clienti con configurazioni di sviluppo di livello Enterprise e pipeline CI/CD appositamente progettate per garantire test approfonditi e la massima qualità del codice, in modo da poter offrire esperienze eccezionali. Cloud Manager offre tutto il necessario per iniziare a lavorare in autonomia, inclusa la possibilità di creare risorse e ambienti cloud.

In genere un membro del team assegnato al profilo di prodotto **Proprietario business** è responsabile dell&#39;aggiunta delle risorse cloud, ad esempio programmi e ambienti. Si tratta della persona che, in base alle esigenze aziendali, completa la configurazione iniziale di Cloud Manager.

Ai fini di questo percorso di onboarding, come amministratore di sistema dovresti aver già assegnato te stesso/a al profilo di prodotto **Proprietario business** e ti occuperai della configurazione delle risorse cloud. A seconda dei requisiti effettivi del progetto, gli utenti con ruolo Proprietario business e Amministratore di sistema possono corrispondere.

## Accesso a Cloud Manager come Amministratore di sistema e Proprietario business {#access-sysadmin-bo}

Prima che i membri del team assegnati al ruolo **Proprietario business** possano accedere a Cloud Manager e iniziare a creare risorse cloud, è necessario assegnare all&#39;amministratore di sistema il ruolo **Proprietario business**. Devono anche accedere a Cloud Manager come hai fatto nel passaggio precedente in questo percorso di onboarding.

1. Come amministratore di sistema, assicurati di aver assegnato il tuo utente al ruolo **Proprietario business**.

   Tornare al passaggio precedente, [Assegnare membri del team ai profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md), per informazioni dettagliate sull&#39;assegnazione del ruolo **Proprietario business** all&#39;amministratore di sistema.

1. Accedi a Cloud Manager in [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

Dopo aver effettuato l&#39;accesso come amministratore di sistema con il ruolo **Proprietario business**, è possibile inizializzare Cloud Manager per l&#39;utilizzo da parte di altri utenti con il ruolo **Proprietario business**. Non ricevi alcuna conferma o messaggio. È sufficiente effettuare l’accesso.

Finché non accedi a Cloud Manager come amministratore di sistema con il ruolo **Proprietario business**, gli altri utenti con ruolo **Proprietario business** non possono creare programmi in Cloud Manager. Questa regola vale anche se sono stati assegnati i ruoli corretti.

## Passa a Cloud Manager {#navigate-cloud-manager}

Gli utenti con il ruolo **Proprietario business** ricevono un’e-mail di benvenuto con un collegamento per iniziare. Per accedere a Cloud Manager da questa e-mail di benvenuto, segui la procedura riportata di seguito.

1. Dall’e-mail di benvenuto, fai clic su **Inizia** come mostrato nella figura in basso.
   ![Esempio di e-mail](/help/journey-onboarding/assets/get-started-email.png)

1. Passa alla pagina **Programmi e prodotti** di Cloud Manager.

   >[!TIP]
   >
   >Puoi passare direttamente alla pagina di accesso di Cloud Manager dall’indirizzo `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Aggiungi un segnalibro a questa pagina per riferimenti futuri.

1. Si apre la pagina di destinazione di Cloud Manager.

In alternativa, è possibile passare alla pagina **Programmi e prodotti** di Cloud Manager dalla home page di Adobe Experience Cloud seguendo la procedura riportata di seguito.

1. Passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com) e accedi con il tuo Adobe ID.

1. Dalla pagina Home di Adobe Experience Cloud, seleziona **Experience Manager** per aprire la pagina Home di AEM.

   ![Pagina Home di Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Nel riquadro **Cloud Manager**, seleziona **Avvia**.

   ![Pagina Home di AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Dopo aver effettuato correttamente l’accesso, si apre la pagina di destinazione di Cloud Manager. Per ulteriori dettagli, consulta [Visualizzazione dei programmi di Cloud Manager](#viewing-programs).

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

Se nell’organizzazione sono già presenti dei programmi, questi vengono visualizzati nella pagina di destinazione, insieme a un pulsante per aggiungerne di nuovi.

![Con programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### In presenza di programmi e con il ruolo di amministratore di sistema {#programs-exist-sysadmin}

Se nell&#39;organizzazione sono presenti programmi e l&#39;utente è l&#39;amministratore di sistema, nella pagina di destinazione verrà visualizzato il pulsante **Gestisci accesso** insieme all&#39;opzione **Aggiungi programma**.

![Vista dell’amministratore di sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifica dei ruoli utente {#verify-user-roles}

Dopo aver effettuato l’accesso a Cloud Manager, puoi verificare che il tuo utente sia stato correttamente assegnato al profilo di prodotto **Proprietario business**.

1. Seleziona il tuo profilo nella parte in alto a destra della finestra.

1. Per visualizzare i ruoli assegnati ai tuoi utenti, seleziona **Ruoli utente**.

   ![Ruoli utente](/help/journey-onboarding/assets/setup-resources6.png)

1. La finestra di dialogo deve confermare che ti è stato assegnato il ruolo **Proprietario business**.

   ![Elenco dei ruoli utente](/help/journey-onboarding/assets/setup-resources7.png)

Hai completato correttamente l’accesso a Cloud Manager come Proprietario business. Se il tuo utente non è assegnato al ruolo **Proprietario business**, contatta l’amministratore di sistema.

## Passaggio successivo {#whats-next}

Ora che puoi accedere a Cloud Manager come amministratore di sistema, tutto è pronto per creare il primo programma.

Continua il tuo percorso di onboarding passando al documento [Creazione di un programma](create-program.md) per scoprire come farlo.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): scopri Cloud Manager, i suoi programmi e gli ambienti che offre.
* [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
