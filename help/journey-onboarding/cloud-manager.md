---
title: Accesso a Cloud Manager
description: Scopri come accedere a Cloud Manager per configurare le risorse del progetto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 0db48ef4c15b6ca530b2626f7078c7172c872fff
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 84%

---

# Accesso a Cloud Manager {#cloud-resources}

In questa sezione del [percorso di onboarding](overview.md) scoprirai come accedere a Cloud Manager per configurare le risorse del progetto.

## Obiettivo {#objective}

Nell’articolo precedente di questo percorso di onboarding, [Assegnazione dei membri del team ai profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md), hai assegnato i ruoli appropriati al team AEMaaCS. Ora, scopri come accedere a Cloud Manager per configurare le risorse del progetto che verranno utilizzate dal team.

Ora che hai completato il passaggio precedente in questo percorso, il tuo team può accedere a Cloud Manager. Cloud Manager viene utilizzato per creare e gestire le risorse dei progetti, come ad esempio programmi e ambienti.

Dopo aver letto questo documento avrai compreso:

* Che l’amministratore di sistema assegnato al ruolo **Proprietario business** deve essere la prima persona dell’organizzazione ad accedere a Cloud Manager.
* Come accedere a Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per il team. Supporta i clienti con configurazioni di sviluppo di livello Enterprise e pipeline CI/CD appositamente progettate per garantire test approfonditi e la massima qualità del codice, in modo da poter offrire esperienze eccezionali. Cloud Manager offre tutti gli strumenti necessari per iniziare a lavorare in autonomia, inclusa la possibilità di creare le risorse e gli ambienti cloud.

In genere un membro del team assegnato al profilo di prodotto **Proprietario business** è responsabile dell’aggiunta delle risorse cloud, ad esempio programmi e ambienti. Si tratta della persona che, in base alle esigenze aziendali, completa la configurazione iniziale di Cloud Manager.

Ai fini di questo percorso di onboarding, come amministratore di sistema dovresti aver già assegnato te stesso/a al profilo di prodotto **Proprietario business** e ti occuperai della configurazione delle risorse cloud. A seconda dei requisiti effettivi del progetto, gli utenti con ruolo Proprietario business e Amministratore di sistema possono corrispondere.

## Accesso a Cloud Manager come Amministratore di sistema e Proprietario business {#access-sysadmin-bo}

Prima che i membri del gruppo assegnati al ruolo **Proprietario business** possano accedere a Cloud Manager e iniziare a creare risorse cloud, l’amministratore di sistema deve essere assegnato al ruolo **Proprietario business**. Devono anche accedere a Cloud Manager come hai fatto nel passaggio precedente in questo percorso di onboarding.

1. Come amministratore di sistema, assicurati di aver assegnato il tuo utente al ruolo **Proprietario business**.

   Torna al passaggio precedente, [Assegnare membri del gruppo ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) per ulteriori informazioni sull’assegnazione del ruolo **Proprietario business** all’amministratore di sistema.

1. Accedi a Cloud Manager all&#39;indirizzo [experiece.adobe.com](https://experience.adobe.com).
1. Nel raggruppamento Accesso rapido fare clic su **Experience Manager**.
1. Nel pannello laterale sinistro fare clic su **Cloud Manager**.

   ![Cloud Manager nella console](/help/journey-onboarding/assets/consol-cloud-manager.png)

Dopo aver effettuato l&#39;accesso come amministratore di sistema con il ruolo **Proprietario business**, puoi utilizzare Cloud Manager per gli altri utenti con ruolo **Proprietario business**. Non ricevi alcuna conferma o messaggio. È sufficiente effettuare l’accesso.

Fino a quando non accedi a Cloud Manager come amministratore di sistema con il ruolo **Proprietario business**, gli altri utenti con ruolo **Proprietario business** non possono creare programmi in Cloud Manager. Questa regola vale anche se sono stati assegnati i ruoli corretti.

## Passa a Cloud Manager {#navigate-cloud-manager}

Gli utenti con il ruolo **Proprietario business** ricevono un’e-mail di benvenuto con un collegamento per iniziare. Per accedere a Cloud Manager da questa e-mail di benvenuto, segui la procedura riportata di seguito.

1. Dall’e-mail di benvenuto, fai clic su **Inizia** come mostrato nella figura in basso.
   ![Esempio di e-mail](/help/journey-onboarding/assets/get-started-email.png)

1. Passa alla pagina **Programmi e prodotti** di Cloud Manager.

   >[!TIP]
   >
   >Puoi passare direttamente alla pagina di accesso di Cloud Manager dall’indirizzo `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Aggiungi un segnalibro a questa pagina per riferimenti futuri.

1. Si apre la pagina di destinazione di Cloud Manager.

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## Visualizza programmi {#viewing-programs}

Dopo aver effettuato correttamente l’accesso a Cloud Manager, gli elementi visualizzati dipendono dallo stato dei programmi, come descritto nelle sezioni seguenti.

### Se non esiste alcun programma {#no-programs}

Se nell’organizzazione non sono presenti programmi, la pagina di destinazione ti invita a creare il primo programma.

![Senza programmi](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### Quando i programmi esistono già {#programs-exist}

Se nell’organizzazione sono già presenti dei programmi, questi vengono visualizzati nella pagina di destinazione, insieme a un pulsante per aggiungerne di nuovi.

![Con programmi](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### Quando è presente un programma e si è un amministratore di sistema {#programs-exist-sysadmin}

Se nell’organizzazione sono già presenti dei programmi e disponi del ruolo di Amministratore di sistema, nella pagina di destinazione viene visualizzato il pulsante **Gestisci accesso** e l’opzione **Aggiungi programma**.

![Vista dell’amministratore di sistema](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## Verifica i ruoli utente {#verify-user-roles}

Dopo aver effettuato l&#39;accesso a Cloud Manager, è possibile verificare di aver ricevuto il profilo di prodotto **Proprietario business**.

1. Fai clic sull&#39;icona **Account** nell&#39;angolo superiore destro della pagina.

1. Fare clic su **Ruoli utente**.

   ![Ruoli utente](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. Nella finestra di dialogo **Ruoli utente**, verifica che l&#39;utente abbia il ruolo **Proprietario business**.

   ![Elenco dei ruoli utente](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

Hai effettuato correttamente l’accesso a Cloud Manager come Proprietario business. Se il tuo utente non è assegnato al ruolo **Proprietario business**, contatta l’amministratore di sistema.

## Passaggio successivo {#whats-next}

Ora che puoi accedere a Cloud Manager come amministratore di sistema, tutto è pronto per creare il primo programma.

Continua il tuo percorso di onboarding passando al documento [Creazione di un programma](create-program.md) per scoprire come farlo.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): scopri Cloud Manager, i suoi programmi e gli ambienti che offre.
* [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
