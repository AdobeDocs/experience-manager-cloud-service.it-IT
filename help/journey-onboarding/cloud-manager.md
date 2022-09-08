---
title: Accesso a Cloud Manager
description: Scopri come accedere a Cloud Manager per configurare le risorse del progetto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 1%

---

# Accesso a Cloud Manager {#cloud-resources}

In questa parte del [percorso di bordo,](overview.md) scopri come accedere a Cloud Manager per configurare le risorse del progetto.

## Obiettivo {#objective}

Nell&#39;articolo precedente di questo percorso di onboarding, [Assegnazione di membri del team ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) hai assegnato i ruoli appropriati al tuo team AEMaaCS. Ora scopri come accedere a Cloud Manager per configurare le risorse di progetto che il tuo team utilizzerà.

Dal momento che hai completato il passaggio precedente in questo percorso, il tuo team può accedere a Cloud Manager. Cloud Manager viene utilizzato per creare e gestire le risorse del progetto, ad esempio programmi e ambienti.

Dopo aver letto questo documento è necessario comprendere:

* Un amministratore di sistema assegnato a **Proprietario business** Il ruolo deve essere il primo dell’organizzazione ad accedere e accedere a Cloud Manager.
* Come accedere a Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager è un componente essenziale di AEM as a Cloud Service e funge da punto di ingresso unico per il tuo team. Supporta i clienti con configurazioni di sviluppo aziendale con le pipeline CI/CD appositamente progettate, che sono dotate per garantire test approfonditi e la massima qualità del codice per fornire esperienze eccezionali. Cloud Manager offre tutto il necessario per iniziare a utilizzare i servizi self-service, inclusa la possibilità di creare risorse e ambienti cloud.

In genere, un membro del team assegnato a **Proprietario business** il profilo di prodotto è responsabile dell’aggiunta delle risorse cloud, ad esempio programmi e ambienti. Questo individuo comprende le esigenze aziendali e completa la configurazione iniziale di Cloud Manager.

Ai fini di questo percorso di onboarding, l&#39;utente, in qualità di amministratore di sistema, si è già assegnato al gruppo **Proprietario business** profilo di prodotto e configurerà le risorse cloud. A seconda dei requisiti effettivi del progetto, i proprietari aziendali possono essere o meno uguali all&#39;amministratore di sistema.

>[!NOTE]
>
>Per impostazione predefinita, un utente con accesso a un ambiente AEM avrà anche il ruolo Utente di Cloud >Manager . Questo ruolo in e di per sé è insufficiente per consentire all&#39;utente di accedere alla visualizzazione dei dettagli del programma. Un utente con solo il ruolo utente di Cloud Manager può navigare tramite le opzioni del menu di programma fino all’URL dell’autore dell’ambiente AEM (se esistono ambienti). Gli utenti devono contattare il proprio amministratore se desiderano ottenere l&#39;accesso a livello di programma.

## Accesso a Cloud Manager come amministratore di sistema e proprietario business {#access-sysadmin-bo}

Prima dei membri del team assegnati al **Proprietario business** il ruolo può accedere a cloud manager e iniziare la creazione di risorse cloud; all’amministratore di sistema deve essere assegnato il **Proprietario business** e accedi a Cloud Manager come nel passaggio precedente in questo percorso di onboarding.

1. Assicurati, in qualità di amministratore di sistema, di disporre della **Proprietario business** ruolo assegnato.

   * Torna al passaggio precedente in questo percorso, [Assegnare membri del team ai profili di prodotto di Cloud Manager,](assign-profiles-cloud-manager.md) per ulteriori informazioni sull&#39;assegnazione di **Proprietario business** Se non lo hai già fatto, rivolgiti all’amministratore di sistema.

1. Accedi a Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e devono essere presentate con la normale pagina di destinazione.

Effettuando l&#39;accesso come amministratore di sistema con **Proprietario business** , inizializza Cloud Manager per l’utilizzo da parte degli altri utenti con **Proprietario business** ruolo. Non riceverai una conferma di questo o di alcun messaggio. Basta accedere.

Fino a quando non accedi a Cloud Manager come amministratore di sistema con **Proprietario business** ruolo , altri utenti con **Proprietario business** Il ruolo non sarà in grado di creare programmi in Cloud Manager anche se gli sono stati assegnati i ruoli corretti.

## Passa a Cloud Manager {#navigate-cloud-manager}

Utenti con **Proprietario business** Il ruolo riceverà un’e-mail di benvenuto con un collegamento per iniziare. Segui i passaggi riportati di seguito per accedere a Cloud Manager utilizzando questo messaggio e-mail di benvenuto.

1. Dal tuo messaggio e-mail di benvenuto clicca su **Introduzione**, come illustrato nella figura seguente.
   ![Esempio di e-mail](/help/journey-onboarding/assets/get-started-email.png)

1. Accedi a Cloud Manager’ **Programmi e prodotti** pagina.

   >[!TIP]
   >
   >Puoi anche accedere direttamente alla pagina di accesso di Cloud Manager da `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Aggiungi il segnalibro a questa pagina per riferimenti futuri.

1. Verrai indirizzato alla pagina di destinazione di Cloud Manager.

In alternativa, puoi anche passare a Cloud Manager’s **Programmi e prodotti** dalla home page di Adobe Experience Cloud seguendo questi passaggi

1. Passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com) e accedi utilizzando il tuo Adobe ID.

1. Dalla home page di Adobe Experience Cloud, seleziona **Experience Manager**.

   ![homepage di Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Verrà visualizzata la home page di AEM. Da qui, fai clic su **Launch** sulla **Cloud Manager** piastrelle.

   ![Pagina principale AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Dopo l’accesso, verrai indirizzato alla pagina di destinazione di Cloud Manager. Vedi [Visualizzazione dei programmi di Cloud Manager](#viewing-programs) per ulteriori dettagli.

La modalità di accesso ai programmi e ai prodotti tramite Cloud Manager dipende da te e non ha alcun effetto sulla modalità di utilizzo di Cloud Manager o sulla modalità di gestione dei programmi.

>[!NOTE]
>
>A seconda dei ruoli assegnati in Cloud Manager e dello stato dell’applicazione, durante l’utilizzo dell’interfaccia utente di Cloud Manager vengono visualizzate diverse schermate.

## Visualizzazione dei programmi {#viewing-programs}

Una volta effettuato correttamente l’accesso a Cloud Manager, ciò che viene visualizzato dipenderà dallo stato dei programmi, come descritto nelle sezioni seguenti.

### In assenza di programmi {#no-programs}

Se nell’organizzazione non sono presenti programmi, la pagina di destinazione ti invita a creare il primo programma.

![Nessun programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### Quando esistono già programmi {#programs-exist}

Se nell’organizzazione sono già presenti programmi, nella pagina di destinazione vengono visualizzati i programmi esistenti e viene inoltre offerto un pulsante per aggiungere altri programmi.

![I programmi esistono](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### Quando esiste un programma e si è amministratori di sistema {#programs-exist-sysadmin}

Se nell’organizzazione sono già presenti programmi e sei un amministratore di sistema, viene visualizzata la pagina di destinazione **Gestisci accesso** insieme a **Aggiungi programma** opzione .

![Vista amministratore di sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verifica dei ruoli utente {#verify-user-roles}

Dopo aver effettuato l’accesso a Cloud Manager, puoi verificare di aver ricevuto l’assegnazione del **Proprietario business** profilo di prodotto.

1. Seleziona il tuo profilo dall’alto a destra della finestra.

   ![Profilo utente](/help/journey-onboarding/assets/setup-resources5.png)

1. Seleziona **Ruoli utente** per visualizzare i ruoli assegnati all’utente.

   ![Ruoli utente](/help/journey-onboarding/assets/setup-resources6.png)

1. La finestra di dialogo deve confermare che l’utente ha la **Proprietario business** ruolo.

   ![Elenco di ruoli utente](/help/journey-onboarding/assets/setup-resources7.png)

Accesso a Cloud Manager come proprietario aziendale completato. Se non ti viene assegnata la **Proprietario business** , contatta l&#39;amministratore di sistema.

## Novità {#whats-next}

Ora che puoi accedere a Cloud Manager come amministratore di sistema, puoi creare il tuo primo programma.

Continua il tuo percorso di onboarding esaminando il documento [Creare un programma](create-program.md) dove imparerai come farlo.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Informazioni su Cloud Manager, i programmi e gli ambienti Cloud Manager.
