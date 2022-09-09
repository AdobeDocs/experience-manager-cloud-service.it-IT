---
title: Gestione degli ambienti
description: Scopri i tipi di ambienti che puoi creare e come crearli per il progetto Cloud Manager.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 7174b398040acbf9b18b5ac2aa20fdba4f98ca78
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 2%

---

# Gestione degli ambienti {#managing-environments}

Scopri i tipi di ambienti che puoi creare e come crearli per il progetto Cloud Manager.

## Tipi di ambiente {#environment-types}

Un utente con le autorizzazioni necessarie può creare i seguenti tipi di ambiente (entro i limiti di ciò che è disponibile per il tenant specifico).

* **Produzione e stage** - Gli ambienti di produzione e di staging sono disponibili come coppia e sono utilizzati rispettivamente a scopo di produzione e di test.

* **Sviluppo** - È possibile creare un ambiente di sviluppo a scopo di sviluppo e test e associarlo solo alle pipeline non di produzione.


Le funzionalità dei singoli ambienti dipendono dalle soluzioni abilitate nel contenitore [programma.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/home.md)

>[!NOTE]
>
>Gli ambienti di produzione e di staging vengono creati solo come coppia. Non è possibile creare solo un ambiente di staging o solo un ambiente di produzione.

## Aggiunta di un ambiente {#adding-environments}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma per il quale desideri aggiungere un ambiente.

1. Da **Panoramica del programma** pagina, fai clic su **Aggiungi ambiente** sulla **Ambienti** per aggiungere un ambiente.

   ![Scheda Ambienti](assets/no-environments.png)

   * La **Aggiungi ambiente** è disponibile anche nella **Ambienti** scheda .

      ![Scheda Ambienti](assets/environments-tab.png)

   * La **Aggiungi ambiente** L’opzione può essere disabilitata a causa di autorizzazioni insufficienti o a seconda delle risorse concesse in licenza.

1. In **Aggiungi ambiente** finestra di dialogo visualizzata:

   * Seleziona un **Tipo di ambiente**.
      * Il numero di ambienti disponibili/utilizzati viene visualizzato tra parentesi dietro il tipo di ambiente di sviluppo.
   * Fornisci un **Nome dell&#39;ambiente**.
   * Fornisci un **Descrizione dell&#39;ambiente**.
   * Seleziona una **Area cloud**.

   ![Finestra di dialogo Aggiungi ambiente](assets/add-environment2.png)

1. Fai clic su **Salva** per aggiungere l&#39;ambiente specificato.

La **Panoramica** ora visualizza il nuovo ambiente nel **Ambienti** il Card. Ora puoi impostare le pipeline per il nuovo ambiente.

## Dettagli dell&#39;ambiente {#viewing-environment}

È possibile utilizzare **Ambienti** nella pagina della panoramica per accedere ai dettagli di un ambiente in due modi.

1. Da **Panoramica** fai clic su **Ambienti** nella parte superiore dello schermo.

   ![Scheda Ambienti](assets/environments-tab2.png)

   * In alternativa, fai clic sul pulsante **Mostra tutto** pulsante **Ambienti** scheda per saltare direttamente al **Ambienti** scheda .

      ![Mostra tutte le opzioni](assets/environment-showall.png)

1. La **Ambienti** apre ed elenca tutti gli ambienti per il programma.

   ![Scheda Ambienti](assets/environment-view-2.png)

1. Fai clic su un ambiente nell’elenco per visualizzarne i dettagli.

   ![Dettagli dell&#39;ambiente](assets/environ-preview1.png)

In alternativa, fare clic sul pulsante con i puntini di sospensione dell&#39;ambiente desiderato, quindi selezionare **Visualizza dettagli**.

![Visualizzare i dettagli dell’ambiente](assets/view-environment-details.png)

>[!NOTE]
>
>La **Ambienti** la scheda elenca solo tre ambienti. Fai clic sul pulsante **Mostra tutto** come descritto in precedenza per visualizzare tutti gli ambienti del programma.

### Accesso al servizio di anteprima {#access-preview-service}

Cloud Manager fornisce un servizio di anteprima (fornito come servizio di pubblicazione aggiuntivo) per ogni ambiente AEM as a Cloud Service.

Con il servizio puoi visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione effettivo ed è disponibile al pubblico.

Al momento della creazione, al servizio di anteprima verrà applicato un elenco consentiti IP predefinito, etichettato `Preview Default [<envId>]`, che blocca tutto il traffico al servizio di anteprima. Per abilitare l’accesso, devi annullare attivamente l’applicazione dell’elenco consentiti IP predefinito dal servizio di anteprima.

![Anteprima del servizio e del relativo elenco consentiti](assets/preview-ip-allow.png)

Un utente con le autorizzazioni necessarie deve completare i passaggi delle seguenti opzioni prima di condividere l’URL del servizio di anteprima con uno dei tuoi team, al fine di garantire l’accesso all’URL di anteprima.

1. Crea un elenco consentiti IP appropriato, applicalo al servizio di anteprima e annulla immediatamente l’applicazione del `Preview Default [<envId>]` elenco consentiti.

   * Fare riferimento al documento [Applicazione e annullamento dell’applicazione di Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) per ulteriori dettagli.

1. Utilizzare l&#39;aggiornamento **ELENCO CONSENTITI IP** per rimuovere l’IP predefinito e aggiungere gli IP appropriati. Fai riferimento a [Gestione degli Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) per saperne di più.

Una volta sbloccato l’accesso al servizio di anteprima, l’icona a forma di lucchetto davanti al nome del servizio di anteprima non verrà più visualizzata.

Una volta attivato, puoi pubblicare il contenuto nel servizio di anteprima utilizzando l’interfaccia utente Gestisci pubblicazione in AEM. Fare riferimento al documento [Anteprima del contenuto](/help/sites-cloud/authoring/fundamentals/previewing-content.md) per ulteriori dettagli.

>[!NOTE]
>
>L&#39;ambiente deve essere in versione AEM `2021.05.5368.20210529T101701Z` o più recente. Per eseguire questa operazione, assicurati che nell’ambiente sia stata eseguita correttamente una pipeline di aggiornamento.

## Aggiornamento degli ambienti {#updating-dev-environment}

In qualità di servizio nativo per il cloud, gli aggiornamenti degli ambienti di staging e produzione all’interno dei programmi di produzione vengono gestiti automaticamente da Adobe.

Tuttavia, gli aggiornamenti agli ambienti di sviluppo e agli ambienti nei programmi sandbox vengono gestiti all’interno dei programmi. Se tale ambiente non esegue l&#39;ultima versione disponibile al pubblico AEM, lo stato **Ambienti** scheda **Panoramica** la schermata del programma **Aggiornamento disponibile**.

![Stato dell’aggiornamento dell’ambiente](assets/environ-update.png)

### Aggiornamenti e pipeline {#updates-pipelines}

Le tubazioni sono l&#39;unico modo per [distribuisci il codice negli ambienti di AEM as a Cloud Service.](deploy-code.md) Per questo motivo, ogni pipeline è associata a una particolare versione AEM.

Se Cloud Manager rileva che è disponibile una versione più recente di AEM rispetto a quella distribuita per l’ultima volta con la pipeline, mostra la variabile **Aggiornamento disponibile** per l&#39;ambiente.

Il processo di aggiornamento è quindi articolato in due fasi:

1. Aggiornamento della pipeline con l’ultima versione AEM
1. Esecuzione della pipeline per distribuire la nuova versione di AEM in un ambiente

### Aggiornamento degli ambienti {#updating-your-environments}

La **Aggiorna** è disponibile nella **Ambienti** scheda per ambienti e ambienti di sviluppo nei programmi sandbox facendo clic sul pulsante con i puntini di sospensione dell’ambiente.

![Opzione di aggiornamento dalla scheda Ambienti](assets/environ-update2.png)

Questa opzione è disponibile anche facendo clic sul pulsante **Ambienti** scheda del programma e quindi selezionare il pulsante di sospensione dell&#39;ambiente.

![Opzione Aggiorna dalla scheda Ambienti](assets/environ-update3.png)

Un utente con **Gestione distribuzione** Questo ruolo può utilizzare questa opzione per aggiornare la pipeline associata a questo ambiente alla versione più recente AEM.

Una volta aggiornata la versione della pipeline all’ultima versione AEM disponibile al pubblico, all’utente viene richiesto di eseguire la pipeline associata per distribuire l’ultima versione nell’ambiente.

![Richiedi di eseguire la pipeline per aggiornare l’ambiente](assets/update-run-pipeline.png)

La **Aggiorna** il comportamento dell&#39;opzione varia a seconda della configurazione e dello stato corrente del programma.

* Se la pipeline è già stata aggiornata, la **Aggiorna** richiede all’utente di eseguire la pipeline.
* Se la pipeline è già in fase di aggiornamento, la **Aggiorna** informa l&#39;utente che è già in esecuzione un aggiornamento.
* Se una pipeline appropriata non esce, la **Aggiorna** richiede all&#39;utente di crearne uno.

## Eliminazione di ambienti di sviluppo {#deleting-environment}

L&#39;utente con le autorizzazioni necessarie potrà eliminare un ambiente di sviluppo.

Da **Panoramica** schermo del programma **Ambienti** fare clic sul pulsante con i puntini di sospensione dell&#39;ambiente di sviluppo che si desidera eliminare.

![Opzione Elimina](assets/environ-delete.png)

L’opzione Elimina è disponibile anche nella **Ambienti** della scheda **Panoramica** finestra del programma. Fai clic sul pulsante con i puntini di sospensione dell’ambiente e seleziona **Elimina**.

![Opzione Elimina dalla scheda Ambienti](assets/environ-delete2.png)

>[!NOTE]
>
>* Non è possibile eliminare gli ambienti di produzione e di staging creati in un programma di produzione.
>* È possibile eliminare gli ambienti di produzione e di staging in un programma sandbox.


## Gestione dell&#39;accesso {#managing-access}

Seleziona **Gestisci accesso** dal menu dei puntini di sospensione dell&#39;ambiente nel **Ambienti** il Card. Puoi passare direttamente all’istanza di authoring e gestire l’accesso per il tuo ambiente.

![Opzione Gestisci accesso](assets/environ-access.png)

## Accesso alla Console per sviluppatori {#accessing-developer-console}

Seleziona **Console per sviluppatori** dal menu dei puntini di sospensione dell&#39;ambiente nel **Ambienti** il Card. Verrà aperta una nuova scheda nel browser con la pagina di accesso al **Console per sviluppatori**.

![](assets/environ-devconsole.png)

Solo un utente con **Sviluppatore** il ruolo avrà accesso al **Console per sviluppatori**. Tuttavia, per i programmi sandbox, qualsiasi utente con accesso al programma sandbox avrà accesso a **Console per sviluppatori**.

Fare riferimento al documento [Ambienti Sandbox sospensione e disattivazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) per ulteriori dettagli.

Questa opzione è disponibile anche nel **Ambiente** della scheda **Panoramica** quando si fa clic sul menu dei puntini di sospensione di un singolo ambiente.

## Accesso locale {#login-locally}

Seleziona **Accesso locale** dal menu dei puntini di sospensione dell&#39;ambiente nel **Ambienti** scheda per accedere localmente ad Adobe Experience Manager.

![Accesso locale](assets/environ-login-locally.png)

Inoltre, puoi effettuare l’accesso localmente dal **Ambienti** della scheda **Panoramica** pagina.

![Accedi localmente dalla scheda Ambienti](assets/environ-login-locally-2.png)

## Gestione dei nomi di dominio personalizzati {#manage-cdn}

I nomi di dominio personalizzati sono supportati in Cloud Manager per i programmi Sites sia per i servizi di pubblicazione che per quelli di anteprima. Ogni ambiente Cloud Manager può ospitare fino a un massimo di 250 domini personalizzati.

Per configurare i nomi di dominio personalizzati, passa alla **Ambienti** e fai clic su un ambiente per visualizzare i dettagli dell’ambiente.

![Dettagli dell&#39;ambiente](assets/domain-names.png)

È possibile eseguire le azioni seguenti sul servizio di pubblicazione per il tuo ambiente.

* [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Controllo dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) o [Certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Gestione degli Elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Gestione degli Elenchi IP consentiti {#manage-ip-allow-lists}

Gli elenchi consentiti IP sono supportati in Cloud Manager per i servizi di authoring, pubblicazione e anteprima per i programmi Sites.

Per gestire gli elenchi consentiti IP, passa alla **Ambienti** della scheda **Panoramica** della pagina del programma. Fai clic su un singolo ambiente per gestirne i dettagli.

### Applicazione di un elenco IP consentiti {#apply-ip-allow-list}

L’applicazione di un elenco consentiti IP associa tutti gli intervalli IP inclusi nella definizione dell’elenco consentiti a un servizio di authoring o pubblicazione in un ambiente. Un utente nel **Proprietario business** o **Gestione distribuzione** per poter applicare un elenco consentiti IP, è necessario aver effettuato l’accesso al ruolo .

L’elenco consentiti IP deve esistere in Cloud Manager per applicarlo a un ambiente. Per ulteriori informazioni sugli elenchi consentiti IP in Cloud Manager, consulta il documento[Introduzione agli Elenchi consentiti IP in Cloud Manager.](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

Segui questi passaggi per applicare un elenco consentiti IP.

1. Passa all’ambiente specifico dal **Ambienti** scheda del programma **Panoramica** e passa alla **ELENCHI CONSENTITI IP** tabella.
1. Utilizza i campi di input nella parte superiore della tabella dell’elenco consentiti IP per selezionare l’elenco consentiti IP e il servizio di authoring o pubblicazione a cui desideri applicarlo.
1. Fai clic su **Applica** e confermare l&#39;invio.

### Annullamento dell’applicazione di un Elenco consentiti IP {#unapply-ip-allow-list}

L’annullamento dell’applicazione di un elenco consentiti IP disassocia tutti gli intervalli IP inclusi nella definizione dell’elenco consentiti da un servizio di authoring o pubblicazione in un ambiente. Un utente nel **Proprietario business** o **Gestione distribuzione** per poter annullare l’applicazione di un elenco consentiti IP, è necessario aver effettuato l’accesso al ruolo .

Segui questi passaggi per annullare l’applicazione di un elenco consentiti IP.

1. Passa all’ambiente specifico dal **Ambienti** scheda del programma **Panoramica** e passa alla **ELENCHI CONSENTITI IP** tabella.
1. Identifica la riga in cui è elencata la regola dell’elenco consentiti IP che desideri annullare l’applicazione.
1. Selezionare il pulsante di sospensione dalla fine della riga.
1. Seleziona **Non applicare** e confermare l&#39;invio.
