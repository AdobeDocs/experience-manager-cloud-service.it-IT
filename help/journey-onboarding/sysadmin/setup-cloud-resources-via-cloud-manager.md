---
title: Configurare le risorse Cloud tramite Cloud Manager
description: Scopri come utilizzare Cloud Manager per configurare e gestire le tue risorse cloud.
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 0db24518610fccf0d2ea5e0620a0c6a5f8009ea8
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---

# Configurare le risorse Cloud tramite Cloud Manager {#setup-cloud-resources}

Scopri come utilizzare Cloud Manager per configurare e gestire le tue risorse cloud.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come vengono create le risorse cloud e chi può crearle. Dopo aver letto questa sezione è necessario comprendere:

* Amministratore di sistema assegnato a **Proprietario business** Il ruolo deve essere il primo dell’organizzazione ad accedere e accedere a Cloud Manager.
* Creazione del programma e degli ambienti cloud.

## Introduzione {#introduction}

L’aggiunta delle risorse cloud viene eseguita tramite Cloud Manager dal membro del team assegnato a **Proprietario business** profilo di prodotto. Si tratta in genere di un utente che capisce le esigenze aziendali e che completa la configurazione iniziale di Cloud Manager.

Segui le sezioni seguenti per scoprire come creare [programmi di servizi cloud](#create-cloud-service-program) e [ambienti.](#create-cloud-environments)

### Prerequisiti {#prerequisites}

* Amministratore di sistema assegnato al **Proprietario business** il ruolo deve aver effettuato l’accesso a Cloud Manager prima di qualsiasi altro utente con **Proprietario business** tentativo di accesso a Cloud Manager per eseguire i passaggi descritti in questo documento.

   * Torna a [Assegnare membri del team ai profili di prodotto di Cloud Manager](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) documento di questo percorso per ulteriori informazioni.

* Dovete capire come fare [naviga e accedi a Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Devi avere familiarità con [Profili di prodotto di Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* È necessario comprendere i concetti di Cloud Manager [programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) e [ambienti.](/help/implementing/cloud-manager/manage-environments.md)

## Accesso a Cloud Manager come amministratore di sistema e proprietario business {#access-sysadmin-bo}

Prima dei membri del team assegnati al **Proprietario business** il ruolo può accedere a cloud manager e iniziare la creazione di risorse cloud; è necessario assegnare all’amministratore di sistema **Proprietario business** e accedi a Cloud Manager.

1. Assicurati, in qualità di amministratore di sistema, di disporre della **Proprietario business** ruolo assegnato.

   * Torna al passaggio precedente in questo percorso, [Assegnare membri del team ai profili di prodotto di Cloud Manager,](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) per ulteriori informazioni sull&#39;assegnazione di **Proprietario business** Se non lo hai già fatto, rivolgiti all&#39;amministratore di sistema.

1. Accedi a Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e devono essere presentate con la normale pagina di destinazione.

Effettuando l&#39;accesso come amministratore di sistema con **Proprietario business** , inizializza Cloud Manager per l’utilizzo da parte degli altri utenti con **Proprietario business** ruolo. Non riceverai una conferma di questo o di alcun messaggio. Basta accedere.

Fino a quando non accedi a Cloud Manager come amministratore di sistema con **Proprietario business** ruolo , altri utenti con **Proprietario business** Il ruolo non sarà in grado di creare programmi in Cloud Manager anche se gli sono stati assegnati i ruoli corretti.

## Passa a Cloud Manager {#navigate-cloud-manager}

L&#39;utente con **Proprietario business** Il ruolo riceverà un’e-mail di benvenuto con un collegamento per iniziare. Segui i passaggi riportati di seguito per accedere a Cloud Manager utilizzando questo messaggio e-mail di benvenuto.

1. Dal tuo messaggio e-mail di benvenuto clicca su **Introduzione**, come illustrato nella figura seguente.
   ![Esempio di e-mail](/help/journey-onboarding/assets/get-started-email.png)

1. Accedi a Cloud Manager’ **Programmi e prodotti** pagina.

   >[!TIP]
   >
   >Puoi anche accedere direttamente alla pagina di accesso di Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Aggiungi il segnalibro a questa pagina per riferimenti futuri.

1. Verrai indirizzato alla pagina di destinazione di Cloud Manager. Vedi [Visualizzazione dei programmi di Cloud Manager](#viewing-programs) per ulteriori dettagli.

Puoi anche accedere a Cloud Manager’s **Programmi e prodotti** dalla home page di Adobe Experience Cloud seguendo questi passaggi

1. Passa direttamente a [Adobe Experience Cloud](https://experience.adobe.com) e accedi utilizzando il tuo Adobe ID.

1. Dalla home page di Adobe Experience Cloud, seleziona **Experience Manager**.

   ![homepage di Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Verrà visualizzata la home page di AEM. Da qui, fai clic su **Launch** sulla **Cloud Manager** piastrelle.

   ![Pagina principale AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Dopo l’accesso, verrai indirizzato alla pagina di destinazione di Cloud Manager. Vedi [Visualizzazione dei programmi di Cloud Manager](#viewing-programs) per ulteriori dettagli.

La modalità di accesso ai programmi e ai prodotti tramite Cloud Manager dipende da te e non ha alcun effetto sulla modalità di utilizzo di Cloud Manager o sulla modalità di gestione dei programmi.

>[!NOTE]
>
>A seconda dei ruoli assegnati in [!UICONTROL Cloud Manager] e lo stato dell&#39;applicazione, visualizzerai schermate diverse durante l&#39;utilizzo [!UICONTROL Cloud Manager] Interfaccia utente.

### Visualizzazione dei programmi {#viewing-programs}

Una volta effettuato correttamente l’accesso a Cloud Manager, ciò che viene visualizzato dipenderà dallo stato dei programmi, come descritto nelle sezioni seguenti.

#### In assenza di programmi {#no-programs}

Se nell’organizzazione non sono presenti programmi, la pagina di destinazione ti invita a creare il primo programma.

![Nessun programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### Quando esistono già programmi {#programs-exist}

Se nell’organizzazione sono già presenti programmi, nella pagina di destinazione vengono visualizzati i programmi esistenti e viene inoltre offerto un pulsante per aggiungere altri programmi.

![I programmi esistono](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### Quando esiste un programma e si è amministratori di sistema {#programs-exist-sysadmin}

Se nell’organizzazione sono già presenti programmi e si è amministratori di sistema, viene visualizzata la pagina di destinazione **Gestisci accesso** insieme a **Aggiungi programma** opzione .

![Vista amministratore di sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verifica dei ruoli utente {#verify-user-roles}

Dopo aver effettuato l’accesso a Cloud Manager, puoi verificare di aver ricevuto l’assegnazione del **Proprietario business** profilo di prodotto.

1. Seleziona il tuo profilo dall’alto a destra della finestra.

   ![Profilo utente](/help/journey-onboarding/assets/setup-resources5.png)

1. Seleziona **Ruoli utente** per visualizzare i ruoli assegnati all’utente.

   ![Ruoli utente](/help/journey-onboarding/assets/setup-resources6.png)

1. Conferma che l’utente ha **Proprietario business** ruolo.

   ![Elenco di ruoli utente](/help/journey-onboarding/assets/setup-resources7.png)

Accesso a Cloud Manager come proprietario aziendale completato. Se non ti viene assegnata la **Proprietario business** , contatta l&#39;amministratore di sistema.

## Creare un programma di Cloud Service {#create-cloud-service-program}

Dopo aver garantito l&#39;accesso appropriato, puoi creare il tuo primo programma.

1. Passa alla pagina di destinazione di Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e accedi.

1. Nella pagina di destinazione di Cloud Manager, fai clic su **Aggiungi programma** per avviare la procedura guidata Aggiungi programma.

   ![Pagina di destinazione](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Per istruzioni dettagliate su come utilizzare la procedura guidata Aggiungi programma, fare riferimento al documento [Creazione di programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) o guarda questo [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) per scoprire come creare il programma AEM as a Cloud e per informazioni su importanti considerazioni prima di creare il programma.


1. Dopo aver creato correttamente il programma cloud, puoi passare al programma dalla pagina di destinazione di Cloud Manager per visualizzare il **Panoramica** della pagina del programma.

   ![Panoramica del programma](/help/journey-onboarding/assets/setup-resources8.png)

1. I membri assegnati al profilo di prodotto per sviluppatori possono accedere a Cloud Manager e gestire gli archivi Git di Cloud Manager.

   * Se non lo hai già fatto, è il momento di assegnare i membri al **Sviluppatore** nel team di Cloud Manager. Torna a [Assegnare membri del team ai profili di prodotto di Cloud Manager](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) documento di questo percorso per ulteriori informazioni.

Ora il programma viene creato correttamente e il tuo archivio Git di Cloud Manager è disponibile per i tuoi sviluppatori per accedere!

## Creare gli ambienti cloud {#create-cloud-environments}

Dopo aver creato correttamente il programma cloud, crea gli ambienti cloud.

1. Passa alla pagina di destinazione di Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona **Aggiungi** dalla scheda ambiente.

   ![Pulsante Aggiungi ambiente](/help/journey-onboarding/assets/setup-resources9.png)

1. Viene avviata la procedura guidata per l’aggiunta dell’ambiente. Aggiungi prima l’ambiente di sviluppo per acquisire familiarità con la procedura guidata.

   >[!TIP]
   >
   >Consulta il documento [Aggiunta di un ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-environments) per saperne di più o guardare [questa esercitazione video rapida](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) per scoprire gli ambienti di Cloud Manager e come aggiungerli al programma.

1. Membri assegnati al **Sviluppatore** il profilo di prodotto può accedere a Cloud Manager e gestire gli archivi Git di Cloud Manager.

Ora il tuo programma è stato creato correttamente e il tuo git di Cloud Manager è disponibile per i tuoi sviluppatori per accedere!

## Novità {#whats-next}

Ora che le risorse cloud sono state create e sono pronte per essere accessibili dal team, l’amministratore di sistema deve assegnare i membri del team a AEM profili di prodotto as a Cloud Service da Adobe Admin Console per accedere a tali risorse.

Continua il tuo percorso di onboarding esaminando il documento [Assegnazione di membri del team a AEM profili di prodotto as a Cloud Service](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) dove verrà illustrato come concedere ai membri del team i diritti necessari per accedere ai nuovi ambienti.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Tipi di programma e aggiunta di un programma](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Tipi di ambiente e aggiunta di un ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Gestione di Cloud Manager Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Configurazione dell’accesso a AEM as a Cloud Service dall’Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
