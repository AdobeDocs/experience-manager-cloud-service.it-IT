---
title: AEM Forms as a Cloud Service - Comunicazioni
description: Unisci automaticamente i dati con i modelli XDP e PDF o genera l’output nei formati PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# Utilizzare l’elaborazione sincrona {#sync-processing-introduction}

Forms as a Cloud Service - Le API per le comunicazioni consentono di creare, assemblare e distribuire comunicazioni personalizzate e orientate al marchio, ad esempio corrispondenze aziendali, documenti, dichiarazioni, lettere di elaborazione delle richieste, note sui benefit, lettere di elaborazione delle richieste, fatture mensili e kit di benvenuto. È possibile utilizzare le API di comunicazione per combinare un modello (XFA o PDF) con i dati dei clienti per generare documenti nei formati PDF, PS, PCL, DPL, IPL e ZPL.

Considerare uno scenario in cui si dispone di uno o più modelli e più record di dati XML per ciascun modello. Puoi utilizzare le API di comunicazione per generare un documento di stampa per ogni record. <!-- You can also combine the records into a single document. --> Il risultato è un documento PDF non interattivo. Un documento PDF non interattivo non consente agli utenti di immettere dati nei campi.

Forms as a Cloud Service - Communications fornisce API on-demand e batch (API asincrone) per la generazione pianificata di documenti:

* Le API sincrone sono adatte a casi d’uso on-demand, a bassa latenza e per la generazione di documenti a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento dopo la compilazione da parte dell’utente di un modulo.

* Le API Batch (API asincrone) sono adatte a casi d’uso pianificati di alta velocità per la generazione di documenti multipli. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, dichiarazioni con carta di credito e dichiarazioni con benefit generate ogni mese.

## Utilizzare le operazioni sincrone {#batch-operations}

Un&#39;operazione sincrona è un processo di generazione di documenti in modo lineare. Queste API sono classificate come API tenant singolo e API multi-tenant:

### API a tenant singolo

* API per la generazione di documenti
* API di manipolazione documenti

### API multi-tenant

* API di Document Utility

### Autenticazione di un’API con un solo tenant

Le operazioni API a tenant singolo supportano due tipi di autenticazione:

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

### Autenticazione di un’API multi-tenant

#### Intestazioni di autenticazione

Ogni chiamata API HTTP in entrata all’API Cloud Manager deve contenere le seguenti tre intestazioni:

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

I valori che devono essere inviati nel `x-api-key` e `x-gw-ims-org-id` le intestazioni sono fornite nella schermata Dettagli credenziali nella [Console Adobe Developer](https://developer.adobe.com/console). Il valore del `x-api-key` l’intestazione è l’ID client e il valore per `x-gw-ims-org-id` header è l&#39;ID organizzazione.

#### Configurare la console Adobe Developer per generare un token di accesso

Per impostare le API di autenticazione, crea un progetto nella console Adobe Developer e aggiungi le API di comunicazione al progetto nella console Adobe Developer. L’integrazione genera Chiave API, Segreto client, Payload (JWT):

1. Contatta l’amministratore della console Adobe Developer. Chiedi all’amministratore di aggiungere come sviluppatore.
1. Accedi a `https://developer.adobe.com/console/`. Utilizza il tuo account sviluppatore per cui il tuo amministratore ha effettuato il provisioning per accedere ad Adobe Developer Console.
1. Seleziona la tua organizzazione dall’angolo in alto a destra. Se non sai qual è la tua organizzazione, contatta l’amministratore.
1. Tocca **[!UICONTROL Crea nuovo progetto]**. Viene visualizzata una schermata per iniziare a utilizzare il nuovo progetto. Tocca **[!UICONTROL Aggiungi API]**. Viene visualizzata una schermata con l’elenco di tutte le API abilitate per il tuo account.
1. Seleziona **[!UICONTROL AEM Forms - Comunicazioni]** e toccare **[!UICONTROL Successivo]**. Viene visualizzata una schermata per configurare l’API.
1. Seleziona **[!UICONTROL OPZIONE 1 Genera una coppia di chiavi]** e toccare **[!UICONTROL Genera coppia di chiavi]**. Crea e scarica il file di configurazione. Il file di configurazione scaricato contiene tutte le impostazioni dell&#39;app, insieme all&#39;unica copia della chiave privata. L&#39;Adobe non registra la tua chiave privata, assicurati di memorizzare in modo sicuro il file scaricato. Tocca **[!UICONTROL Successivo]**.
1. Seleziona **[!UICONTROL Integrazioni - Cloud Service]** e toccare **[!UICONTROL Salva API configurata]**. Tocca **[!UICONTROL Account di servizio (JWT)]** per visualizzare la chiave API, il segreto client e altre informazioni necessarie per accedere alle API. Imposta l’utilizzo del token per accedere alle API.

#### Generare e utilizzare programmaticamente un token di accesso

Per generare programmaticamente un token di accesso, genera un token Web JSON (JWT) e scambialo con Adobe Identity Management Service (IMS) per un token di accesso.

Utilizzare le seguenti chiavi, denominate attestazioni, per costruire l&#39;oggetto JWT JSON:

* `exp`- la scadenza richiesta del token di accesso, espressa in numero di secondi dal 1° gennaio 1970 GMT. Per la maggior parte dei casi d’uso, si tratta di un valore relativamente piccolo. Ad esempio, 5 minuti, per cinque minuti a partire da ora, questo valore deve essere 1670923791.
* `iss` - l’ID organizzazione dal progetto Adobe Developer Console nel formato org_ident@AdobeOrg.
* `sub` - l’ID account tecnico dell’integrazione della console Adobe Developer, nel formato: id@techacct.adobe.com.
* `aud` : l’ID client dell’integrazione della console Adobe Developer è preceduto da `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - impostato sul valore letterale `true`

Questo oggetto JSON deve quindi essere codificato in base64 e firmato utilizzando la chiave privata del progetto. Infine, il valore codificato viene inviato nel corpo di una richiesta POST a `https://ims-na1.adobelogin.com/ims/exchange/jwt` insieme all’ID client e al segreto client per il progetto.

##### Esempio

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### Supporto linguistico per JWT

Anche se è possibile eseguire l&#39;intero processo di generazione e scambio JWT nel codice personalizzato, è più comune utilizzare una libreria di livello superiore per farlo. Una serie di tali librerie sono elencate nella [Documentazione Adobe I/O JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

### (Solo per le API di generazione dei documenti) Configura risorse e autorizzazioni

Per utilizzare le API sincrone, è necessario quanto segue:

* Utenti con privilegi di amministratore di Experience Manager
* Caricare modelli e altre risorse nell’istanza di Cloud Service Experience Manager Forms

### (Solo per le API di generazione dei documenti) Carica modelli e altre risorse nell’istanza di Experience Manager

In genere, un&#39;organizzazione dispone di più modelli. Ad esempio, un modello per i rendiconti della carta di credito, i rendiconti benefici e le applicazioni di credito. Carica tutti i modelli XDP e PDF nella tua istanza Experience Manager. Per caricare un modello:

1. Apri l’istanza di Experience Manager .
1. Vai a Forms > Forms e documenti
1. Fai clic su Crea > Cartella e crea una cartella. Apri la cartella.
1. Fai clic su Crea > Carica file e carica i modelli.

### Richiamare un’API

La [Documentazione di riferimento API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API fornisce anche il file di definizione API in formato .yaml. Puoi scaricare il file .yaml e caricarlo in [Postman](https://www.postman.com/) per verificare la funzionalità delle API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo i membri del gruppo utenti moduli possono accedere alle API di comunicazione.
