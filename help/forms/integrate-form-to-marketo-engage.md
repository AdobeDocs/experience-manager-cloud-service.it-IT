---
Title: How to Integrate Marketo Engage with AEM Forms?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---


# Integrare il Marketo Engage con AEM Forms

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

L&#39;integrazione di AEM Forms con [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) consente agli utenti di sfruttare le funzionalità del Marketo Engage per creare regole business dai dati acquisiti e automatizzare i flussi di lavoro, incluse le campagne intelligenti e l&#39;automazione delle e-mail. Il modulo configurato può inviare i dati acquisiti al Marketo Engage per l&#39;elaborazione.

## Vantaggi dell’integrazione di Marketo Engage con Forms

Di seguito sono riportati alcuni vantaggi della connessione di un modulo AEM con Adobe Marketo Engage:

* **Integrazione semplificata**: la connessione dei moduli con il Marketo Engage elimina la necessità di creare un modello dati del modulo separato. Il processo di integrazione è semplice e intuitivo.
* **Acquisizione automatizzata dei dati**: consente di acquisire automaticamente i moduli inviati e di memorizzarli in Marketo, eliminando l&#39;immissione manuale dei dati e riducendo gli errori.

* **Gestione dei lead**: semplifica i processi di gestione dei lead integrando l&#39;invio dei moduli direttamente nel database di marketing, consentendo un migliore tracciamento e sviluppo dei lead.

* **Prestazioni campagne migliorate**: utilizza i dati dei moduli per analizzare e ottimizzare le campagne di marketing, migliorando le prestazioni complessive e il ritorno sull&#39;investimento (ROI).

* **Analisi e reporting**: consente di accedere a strumenti di analisi e reporting affidabili, come Munchkin, in Marketo per misurare l&#39;efficacia di moduli e campagne.

* **Automazione del follow-up**: consente di automatizzare le e-mail e i flussi di lavoro di follow-up attivati dall&#39;invio dei moduli, garantendo una comunicazione tempestiva con i lead.

## Vantaggi chiave dell’utilizzo di AEM Forms rispetto a soluzioni Forms alternative

La tabella seguente illustra i pochi motivi per cui si è scelto AEM Forms rispetto ad altre soluzioni alternative basate su moduli:

| **Funzionalità** | **AEM Forms** | **Altre soluzioni per moduli** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **Personalizzazioni** | Consente di aggiungere funzioni personalizzate specifiche, modificare le azioni dei moduli e modificare i comportamenti dei campi per migliorare le interazioni dei moduli e i flussi di lavoro complessi | Nessun supporto per la personalizzazione |
| **Editor regole** | Supporta un editor di regole integrato per aggiungere logica e condizioni. | Nessun supporto per l’editor di regole |
| **Opzioni di layout** | Supporta più opzioni di layout | Opzioni di layout limitate |
| **Servizio preriempimento** | Offre un servizio di precompilazione per compilare automaticamente i dati del modulo. | Nessun servizio di preriempimento disponibile |
| **Incorporazione in Sites** | Può essere incorporato in Sites utilizzando iFrame | Non può essere incorporato in Sites utilizzando iFrame |
| **Facilità di integrazione con Sites** | Nessun apprendimento aggiuntivo richiesto; AEM Forms utilizza le stesse competenze di Sites | Potrebbe essere necessario un ulteriore apprendimento |
| **Invio dati** | Può inviare dati a varie piattaforme e offre più connettori, ad esempio Connetti a SharePoint, Connetti a OneDrive, Connetti a Salesforce e altro ancora. | Può inviare dati a connettori limitati, ad esempio a Salesforce |

## Considerazioni sull’integrazione di Marketo Engage con Forms

Alcune considerazioni sull’integrazione del Marketo Engage con AEM Forms:

* AEM supporta solo il database People(Leads) tra i vari database Marketo.
* Marketo consente la [creazione di 10 oggetti personalizzati](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) come oggetti definiti dall&#39;utente per memorizzare dati specializzati oltre i campi standard in Lead, supportando esigenze aziendali univoche.
* L&#39;AEM può accedere agli oggetti personalizzati solo se sono associati al database Lead

## Prerequisiti per l’integrazione di Marketo Engage con Forms

Di seguito sono riportati i prerequisiti per connettere il Marketo Engage ad AEM Forms:

* Una licenza Adobe Marketo Engage valida
* Un&#39;istanza di lavoro del Marketo Engage per [recuperare l&#39;ID client e il segreto client](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) per creare una configurazione cloud.

## Crea una configurazione del servizio cloud per collegare AEM Forms (Adaptive Forms) al Marketo Engage

![Flusso di lavoro](/help/forms/assets/workflow-marketo-1.png)

La configurazione Cloud collega l’istanza Experience Manager all’istanza Adobe Marketo Engage. Per creare una configurazione cloud di Marketo Engage, effettua le seguenti operazioni:

1. Vai a **Strumenti** > **Cloud Service** > **Marketo Engage**.

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

1. Apri una cartella per ospitare la configurazione e fai clic su **Crea**. Viene visualizzata la finestra **Crea configurazione Marketo Engage**.

   >[!NOTE]
   >
   > È inoltre possibile [configurare la cartella per le configurazioni del servizio cloud](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations).

1. Specifica il **Titolo** della configurazione e le credenziali per la connessione al servizio. Puoi recuperare le credenziali di autenticazione dal dashboard di Adobe Marketo Engage:
   * **ID client** e **Segreto client** sono disponibili in **Amministratore** > **Integrazione** > **LaunchPoint** selezionando il servizio personalizzato e facendo clic su **Visualizza dettagli**.
   * **L&#39;URL identità** è disponibile in **Admin** > **Integration** > **Web Services** come **Identity** nella sezione **REST API**.

1. Fai clic su **Connetti**.  Se la connessione ha esito positivo, viene visualizzato il messaggio `Authentication Successful`.
1. Fai clic su **[!UICONTROL Crea]** per salvare le impostazioni di configurazione cloud.

![Configurazione cloud Marketo Engage](/help/forms/assets/marketo-engage-cloud-configuration.png)

Ora puoi utilizzare la configurazione del servizio cloud creata per collegare l’origine dati del Marketo Engage a un modulo adattivo.

## Passaggio successivo

Hai creato la configurazione del servizio cloud per integrare Adobe Marketo Engage con AEM Forms. Ora è possibile integrare:
* [Nuovo modulo adattivo con Marketo Engage](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Modulo adattivo esistente con Marketo Engage](/help/forms/use-marketo-engage-data-source-in-form.md)

## Articoli correlati

{{af-submit-action}}

## Consulta anche

{{marketo-engage-see-also}}



