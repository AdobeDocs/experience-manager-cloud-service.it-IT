---
title: Come integrare Marketo Engage con AEM Forms?
description: Scopri come integrare la tua istanza di Marketo Engage con AEM Forms.
keywords: Come si collega un’istanza di Marketo al modulo? , Collega un modulo a Marketo, Integra un modulo con Marketo Engage, Integra un modulo adattivo con un’istanza Marketo.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 5%

---

# Integrare Marketo Engage con AEM Forms

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

L&#39;integrazione di AEM Forms con [Adobe Marketo Engage](https://experienceleague.adobe.com/it/docs/marketo/using/home) consente agli utenti di sfruttare le funzionalità di Marketo Engage per creare regole business dai dati acquisiti e automatizzare i flussi di lavoro, incluse le campagne intelligenti e l&#39;automazione delle e-mail. Il modulo configurato può inviare i dati acquisiti a Marketo Engage per l’elaborazione.

## Vantaggi dell’integrazione di Marketo Engage con Forms

Di seguito sono riportati alcuni vantaggi della connessione di un modulo AEM a Adobe Marketo Engage:

* **Integrazione semplificata**: la connessione dei moduli con Marketo Engage elimina la necessità di creare un modello dati separato. Il processo di integrazione è semplice e intuitivo.
* **Acquisizione automatizzata dei dati**: consente di acquisire automaticamente i moduli inviati e di memorizzarli in Marketo, eliminando l&#39;immissione manuale dei dati e riducendo gli errori.

* **Gestione dei lead**: semplifica i processi di gestione dei lead integrando l&#39;invio dei moduli direttamente nel database di marketing, consentendo un migliore tracciamento e sviluppo dei lead.

* **Prestazioni campagne migliorate**: utilizza i dati dei moduli per analizzare e ottimizzare le campagne di marketing, migliorando le prestazioni complessive e il ritorno sull&#39;investimento (ROI).

* **Analisi e reporting**: consente di accedere a strumenti di analisi e reporting affidabili, come Munchkin, in Marketo per misurare l&#39;efficacia di moduli e campagne.

* **Automazione del follow-up**: consente di automatizzare le e-mail e i flussi di lavoro di follow-up attivati dall&#39;invio dei moduli, garantendo una comunicazione tempestiva con i lead.

## Vantaggi chiave dell’utilizzo di AEM Forms rispetto a soluzioni Forms alternative

La tabella seguente illustra i pochi motivi per cui si è scelto AEM Forms rispetto ad altre soluzioni alternative basate su moduli:

| **Funzione** | **AEM Forms** | **Altre soluzioni per moduli** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **Personalizzazioni** | Consente di aggiungere funzioni personalizzate specifiche, modificare le azioni dei moduli e modificare i comportamenti dei campi per migliorare le interazioni dei moduli e i flussi di lavoro complessi | Nessun supporto per la personalizzazione |
| **Editor di regole** | Supporta un editor di regole integrato per aggiungere logica e condizioni. | Nessun supporto per l’editor di regole |
| **Opzioni di layout** | Supporta più opzioni di layout | Opzioni di layout limitate |
| **Servizio preriempimento** | Offre un servizio di precompilazione per compilare automaticamente i dati del modulo. | Nessun servizio di preriempimento disponibile |
| **Incorporazione in Sites** | Può essere incorporato in Sites utilizzando iFrame | Non può essere incorporato in Sites utilizzando iFrame |
| **Facilità di integrazione con Sites** | Nessun apprendimento aggiuntivo richiesto; AEM Forms utilizza le stesse competenze di Sites | Potrebbe essere necessario un ulteriore apprendimento |
| **Invio dati** | Può inviare dati a varie piattaforme e offre più connettori, ad esempio Connetti a SharePoint, Connetti a OneDrive, Connetti a Salesforce e altro ancora. | Può inviare dati a connettori limitati, ad esempio a Salesforce |

## Considerazioni sull’integrazione di Marketo Engage con Forms

Alcune considerazioni sull’integrazione di Marketo Engage con AEM Forms:

* AEM supporta solo il database People(Leads) tra i vari database Marketo.
* Marketo consente la [creazione di 10 oggetti personalizzati](https://experienceleague.adobe.com/it/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) come oggetti definiti dall&#39;utente per memorizzare dati specializzati oltre i campi standard in Lead, supportando esigenze aziendali univoche.
* AEM può accedere agli oggetti personalizzati solo se sono associati al database Lead

## Prerequisiti per l’integrazione di Marketo Engage con Forms

Di seguito sono riportati i prerequisiti per connettere Marketo Engage ad AEM Forms:

* Una licenza Adobe Marketo Engage valida
* Un&#39;istanza funzionante di Marketo Engage per [recuperare l&#39;ID client e il segreto client](https://experienceleague.adobe.com/it/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) per creare una configurazione cloud.

## Creare una configurazione del servizio cloud per collegare AEM Forms (Adaptive Forms) a Marketo Engage

![Flusso di lavoro](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span> Questo video è applicabile solo ai Componenti core. Per i componenti UE/Foundation, fare riferimento all&#39;articolo.</span>

La configurazione Cloud collega l’istanza Experience Manager all’istanza Adobe Marketo Engage. Per creare una configurazione cloud di Marketo Engage, effettua le seguenti operazioni:

1. Vai a **Strumenti** > **Servizi cloud** > **Marketo Engage**.

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

Ora puoi utilizzare la configurazione del servizio cloud creata per collegare l’origine dati Marketo Engage a un modulo adattivo.

## Passaggio successivo

Hai creato la configurazione del servizio cloud per integrare Adobe Marketo Engage con AEM Forms. Ora è possibile integrare:

* [Nuovo modulo adattivo con Marketo Engage](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Modulo adattivo esistente con Marketo Engage](/help/forms/use-marketo-engage-data-source-in-form.md)

## Articoli correlati

{{af-submit-action}}

## Consulta anche

{{marketo-engage-see-also}}
