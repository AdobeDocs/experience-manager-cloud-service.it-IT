---
title: AEM Forms as a Cloud Service - Comunicazioni
description: Unisci automaticamente i dati con i modelli XDP e PDF o genera l’output nei formati PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 6b546f551957212614e8b7a383c38797cc21fba1
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# Utilizzare l’elaborazione sincrona {#sync-processing-introduction}

Le comunicazioni consentono di creare, assemblare e distribuire comunicazioni personalizzate e orientate al marchio, ad esempio corrispondenze aziendali, documenti, dichiarazioni, lettere di elaborazione delle richieste, note sui benefit, lettere di elaborazione delle richieste, fatture mensili e kit di benvenuto. È possibile utilizzare le API di comunicazione per combinare un modello (XFA o PDF) con i dati dei clienti per generare documenti nei formati PDF, PS, PCL, DPL, IPL e ZPL.

Considerare uno scenario in cui si dispone di uno o più modelli e più record di dati XML per ciascun modello. Puoi utilizzare le API di comunicazione per generare un documento di stampa per ogni record. <!-- You can also combine the records into a single document. --> Il risultato è un documento PDF non interattivo. Un documento PDF non interattivo non consente agli utenti di immettere dati nei campi.


Le comunicazioni forniscono API per la generazione di documenti on-demand e pianificati. Puoi utilizzare le API sincrone per le API on-demand e batch (API asincrone) per la generazione pianificata dei documenti:

* Le API sincrone sono adatte a casi d’uso on-demand, a bassa latenza e per la generazione di documenti a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento dopo la compilazione da parte dell’utente di un modulo.

* Le API Batch (API asincrone) sono adatte a casi d’uso pianificati di alta velocità per la generazione di documenti multipli. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, dichiarazioni con carta di credito e dichiarazioni con benefit generate ogni mese.

## Utilizzare le operazioni sincrone {#batch-operations}

Un&#39;operazione sincrona è un processo di generazione di documenti in modo lineare. Supporta due tipi di autenticazione:

* **Autenticazione di base**: L’autenticazione di base è un semplice schema di autenticazione integrato nel protocollo HTTP. Il client invia richieste HTTP con l&#39;intestazione Autorizzazione che contiene la parola Base seguita da uno spazio e da una stringa con codifica base64 username:password. Ad esempio, per autorizzare come amministratore / amministratore il client invia Basic [nome utente stringa codificato base64]: [password della stringa con codifica base64].

* **Autenticazione basata su token:** L’autenticazione basata su token utilizza un token di accesso (token di autenticazione portatore) per effettuare richieste ad Experience Manager as a Cloud Service. AEM Forms as a Cloud Service fornisce API per recuperare in modo sicuro il token di accesso. Per recuperare e utilizzare il token per autenticare una richiesta:

   1. [Recuperare le credenziali as a Cloud Service di Experience Manager dalla Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Installare le credenziali as a Cloud Service di Experience Manager nell’ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Application Server, Web Server o altri server non AEM) configurati per inviare richieste al servizio cloud (effettuare chiamate).
   1. [Generare un token JWT e scambiarlo con le API Adobe IMS per un token di accesso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Esegui l’API Experience Manager con il token di accesso come token di autenticazione portatore.
   1. [Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe consiglia di utilizzare l’autenticazione basata su token in un ambiente di produzione.

### Prerequisiti {#pre-requisites}

Per utilizzare le API sincrone, è necessario quanto segue:

* Modelli PDF o XDP
* [Dati da unire con i modelli](#form-data)
* Utenti con privilegi di amministratore di Experience Manager
* Caricare modelli e altre risorse nell’istanza di Cloud Service Experience Manager Forms

#### Carica modelli e altre risorse nell’istanza di Experience Manager

In genere, un&#39;organizzazione dispone di più modelli. Ad esempio, un modello per i rendiconti della carta di credito, i rendiconti benefici e le applicazioni di credito. Carica tutti i modelli XDP e PDF nella tua istanza Experience Manager. Per caricare un modello:

1. Apri l’istanza di Experience Manager .
1. Vai a Forms > Forms e documenti
1. Fai clic su Crea > Cartella e crea una cartella. Apri la cartella.
1. Fai clic su Crea > Carica file e carica i modelli.

### Utilizza l’API sincrona per generare documenti

Sono disponibili API separate per:

* Genera un documento di PDF da un modello e vi unisce i dati.
* Generare un documento PostScript (PS), PCL (Printer Command Language), Zebra Printing Language (ZPL) da un file XDP o da un documento PDF.

La [Documentazione di riferimento API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API è disponibile anche in formato .yaml. Puoi scaricare il file .yaml per [API sincrone](assets/sync.yaml) e caricalo su postman per verificare la funzionalità delle API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo i membri del gruppo utenti moduli possono accedere alle API di comunicazione.

