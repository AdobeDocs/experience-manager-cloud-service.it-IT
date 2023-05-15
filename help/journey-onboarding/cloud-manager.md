---
title: Accesso a Cloud Manager
description: Scopri come accedere a Cloud Manager per configurare le risorse del progetto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# Accesso a Cloud Manager {#cloud-resources}

In questa parte del [percorso di bordo,](overview.md) scopri come accedere a Cloud Manager per configurare le risorse del progetto.

## Obiettivo {#objective}

Nell’articolo precedente di questo percorso di onboarding, [Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) hai assegnato i ruoli appropriati ai membri del gruppo AEMaaCS. Ora scopri come accedere a Cloud Manager per configurare le risorse di progetto utilizzate dal tuo team.

Ora che hai completato il passaggio precedente in questo percorso, il team può accedere a Cloud Manager. Cloud Manager consente di creare e gestire le risorse del progetto, come ad esempio programmi e ambienti.

Dopo aver letto questo documento, è necessario comprendere quanto segue:

* Un amministratore di sistema assegnato a **Proprietario business** Il ruolo deve essere il primo dell’organizzazione ad accedere a Cloud Manager.
* Come accedere a Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso singolo per il team. Supporta i clienti con configurazioni di sviluppo di livello Enterprise e pipeline CI/CD appositamente progettate per garantire test approfonditi e la massima qualità del codice, in modo da poter offrire esperienze eccezionali. Cloud Manager offre tutti gli strumenti necessari per iniziare a lavorare in autonomia, inclusa la possibilità di creare risorse e ambienti cloud.

In genere chi è assegnato al profilo di prodotto **Proprietario business** è responsabile dell’aggiunta delle risorse cloud, ad esempio programmi e ambienti. Si tratta della persona che, in base alle esigenze aziendali, completa la configurazione iniziale di Cloud Manager.

Ai fini di questo percorso di onboarding, l&#39;utente, in qualità di amministratore di sistema, si è già assegnato al gruppo **Proprietario business** profilo di prodotto e può impostare le risorse cloud. A seconda dei requisiti effettivi del progetto, i proprietari dell&#39;azienda possono o meno essere gli stessi dell&#39;amministratore di sistema.

## Accesso a Cloud Manager come Amministratore di sistema e Proprietario business {#access-sysadmin-bo}

Prima dei membri del team assegnati al **Proprietario business** il ruolo può accedere a cloud manager e iniziare la creazione di risorse cloud; all’amministratore di sistema deve essere assegnato il **Proprietario business** ruolo. Devono anche accedere a Cloud Manager come nel passaggio precedente in questo percorso di onboarding.

1. Come amministratore di sistema, assicurati di aver assegnato il tuo utente al ruolo **Proprietario business**.

   * Torna al passaggio precedente in questo percorso, [Assegnare membri del team ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) per ulteriori informazioni sull&#39;assegnazione di **Proprietario business** all&#39;amministratore di sistema.

1. Accedi a Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) per visualizzare la normale pagina di destinazione.

Dopo aver effettuato l’accesso come amministratore di sistema con il ruolo **Proprietario business**, hai inizializzato Cloud Manager per l’uso da parte di altri utenti con il ruolo **Proprietario business**. Non riceverai alcuna conferma o messaggio. È sufficiente accedere.

Fino a quando non accedi a Cloud Manager come amministratore di sistema con **Proprietario business** ruolo , altri utenti con **Proprietario business** Impossibile creare programmi in Cloud Manager. Questa regola è vera anche se gli sono stati assegnati i ruoli corretti.

## Accesso a Cloud Manager {#navigate-cloud-manager}

Utenti con **Proprietario business** ruolo ricevi un’e-mail di benvenuto con un collegamento per iniziare. Per accedere a Cloud Manager da questa e-mail di benvenuto, segui la procedura riportata di seguito.

1. Dal messaggio e-mail di benvenuto, fai clic su **Introduzione**, come illustrato nella figura seguente.
   ![Esempio di e-mail](/help/journey-onboarding/assets/get-started-email.png)

1. Passa a Cloud Manager’s **Programmi e prodotti** pagina.

   >[!TIP]
   >
   >Puoi passare direttamente alla pagina di accesso di Cloud Manager dall’indirizzo `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Aggiungi ai segnalibri questa pagina per riferimenti futuri.

1. Ti indirizzano alla pagina di destinazione di Cloud Manager.

In alternativa, segui questa procedura per accedere alla pagina **Programmi e prodotti** di Cloud Manager dalla pagina Home di Adobe Experience Cloud.

1. Passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com) e accedi con il tuo Adobe ID.

1. Dalla home page di Adobe Experience Cloud, seleziona **Experience Manager** per aprire la home page di AEM.

   ![Pagina Home di Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Sulla **Cloud Manager** riquadro, seleziona **Launch**.

   ![Pagina Home di AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Dopo l’accesso, vieni indirizzato alla pagina di destinazione di Cloud Manager. Vedi [Visualizzazione dei programmi di Cloud Manager](#viewing-programs) per ulteriori dettagli.

La modalità di accesso a programmi e prodotti tramite Cloud Manager è a tua discrezione e non ha alcun effetto su come utilizzi Cloud Manager o come gestisci i programmi.

>[!NOTE]
>
>A seconda dei ruoli assegnati in Cloud Manager e dello stato dell’applicazione, durante l’utilizzo dell’interfaccia utente di Cloud Manager vengono visualizzate schermate diverse.

## Visualizzazione dei programmi {#viewing-programs}

Dopo aver effettuato l’accesso a Cloud Manager, ciò che viene visualizzato dipende dallo stato dei programmi, come descritto nelle sezioni seguenti.

### In assenza di programmi {#no-programs}

Se nell’organizzazione non sono presenti programmi, la pagina di destinazione ti invita a creare il primo programma.

![Senza programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### In presenza di programmi {#programs-exist}

Se nell’organizzazione sono presenti programmi, nella pagina di destinazione vengono visualizzati i programmi esistenti e viene inoltre offerto un pulsante per aggiungere altri programmi.

![Con programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### In presenza di programmi e con il ruolo di amministratore di sistema {#programs-exist-sysadmin}

Se nell’organizzazione sono presenti programmi e sei un amministratore di sistema, viene visualizzata la pagina di destinazione **Gestisci accesso** insieme a **Aggiungi programma** opzione .

![Vista dell’amministratore di sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifica dei ruoli utente {#verify-user-roles}

Dopo aver effettuato l’accesso a Cloud Manager, puoi verificare che il tuo utente sia stato correttamente assegnato al profilo di prodotto **Proprietario business**.

1. Seleziona il tuo profilo nella parte in alto a destra della finestra.

   ![Profilo utente](/help/journey-onboarding/assets/setup-resources5.png)

1. Per visualizzare i ruoli assegnati all’utente, seleziona **Ruoli utente**.

   ![Ruoli utente](/help/journey-onboarding/assets/setup-resources6.png)

1. La finestra di dialogo deve confermare che ti è stato assegnato il ruolo **Proprietario business**.

   ![Elenco dei ruoli utente](/help/journey-onboarding/assets/setup-resources7.png)

Hai completato correttamente l’accesso a Cloud Manager come Proprietario business. Se il tuo utente non è assegnato al ruolo **Proprietario business**, contatta l’amministratore di sistema.

## Passaggio successivo {#whats-next}

Ora che puoi accedere a Cloud Manager come amministratore di sistema, tutto è pronto per creare il primo programma.

Continua il tuo percorso di onboarding passando alla prossima revisione del documento [Creare un programma](create-program.md) dove si impara a farlo.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori risorse facoltative, se desideri andare oltre il contenuto del percorso di onboarding.

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): scopri Cloud Manager, i suoi programmi e gli ambienti che offre.
* [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
