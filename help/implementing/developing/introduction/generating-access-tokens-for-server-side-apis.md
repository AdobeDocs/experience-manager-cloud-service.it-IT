---
title: Generazione di token di accesso per le API lato server
description: Scoprite come facilitare la comunicazione tra un server di terze parti e AEM come Cloud Service generando un token JWT protetto
translation-type: tm+mt
source-git-commit: 7ca7cd458ea5152d56754bf1e6a500b2c04d0039
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# Introduzione {#introduction}

>[!IMPORTANT]
>
>Questa funzione non è ancora disponibile. Per un elenco aggiornato delle funzioni, vedere le [Note sulla versione](/help/release-notes/release-notes-cloud/release-notes-current.md).

Alcune architetture si basano sull&#39;effettuazione di chiamate a AEM come Cloud Service da un&#39;applicazione ospitata su un server esterno all&#39;infrastruttura AEM. Ad esempio, un&#39;applicazione mobile che chiama un server, che quindi esegue richieste API da AEM come Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. Il AEM come Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare i token necessari per il processo di autenticazione.

## Flusso server {#the-server-to-server-flow}

Un utente con il ruolo di amministratore può generare un AEM come credenziale di Cloud Service, che deve essere installata sul server e trattata attentamente come una chiave segreta. Questo file di formato JSON contiene tutti i dati necessari per l&#39;integrazione con un AEM come API di Cloud Service. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con IMS per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione del portatore per effettuare richieste di AEM come Cloud Service.

Il flusso server-to-server comporta i seguenti passaggi:

* Recuperare il AEM come credenziali di Cloud Service dalla Developer Console
* Installare il AEM come credenziali di Cloud Service su un server non AEM che effettua chiamate a AEM
* Generare un token JWT e scambiarlo per un token di accesso utilizzando  Adobi  API IMS
* Chiamata dell&#39;API AEM con il token di accesso come token di autenticazione del portatore

### Recupera il AEM come credenziali Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti che hanno il ruolo di amministratore per un&#39;organizzazione IMS visualizzeranno la scheda integrazioni nella Developer Console per un determinato ambiente, oltre a due pulsanti. Facendo clic sul pulsante **Ottieni credenziali servizio** verranno generate le credenziali del servizio, che conterranno tutte le informazioni necessarie per il server non AEM, inclusi ID client, segreto client, chiave privata, certificato e configurazione per i livelli di creazione e pubblicazione dell&#39;ambiente, indipendentemente dalla selezione del contenitore.

![Generazione JWT](assets/JWTtoken3.png)

L&#39;output sarà simile al seguente:

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

### Installare AEM Credenziali del servizio su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L&#39;applicazione che effettua chiamate a AEM non AEM dovrebbe essere in grado di accedere al AEM come credenziali di Cloud Service, trattandolo come un segreto.

### Generare un token JWT e scambiarlo per un token di accesso{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilizzate le credenziali per creare un token JWT in una chiamata a  servizio  IMS per recuperare un token di accesso, valido per 24 ore.

Le credenziali AEM-CS Service possono essere scambiate per un token di accesso utilizzando le librerie client progettate a tal fine. Le librerie client sono disponibili da [ Adobe  repository GitHub pubblico](https://github.com/adobe/aemcs-api-client-lib), che contiene informazioni più dettagliate e informazioni più recenti.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

Lo stesso scambio può essere eseguito in qualsiasi lingua in grado di generare un token JWT firmato con il formato corretto e di chiamare le API di scambio token IMS.

Il token di accesso verrà definito alla scadenza, che in genere corrisponde a 12 ore. È presente un esempio di codice nel repository Git per gestire un token di accesso e aggiornarlo prima della scadenza.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Eseguite le chiamate API server-to-server appropriate a un AEM come ambiente di Cloud Service, incluso il token di accesso nell&#39;intestazione. Quindi, per l&#39;intestazione &quot;Autorizzazione&quot;, utilizzate il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

## Flusso sviluppatore {#developer-flow}

È probabile che gli sviluppatori desiderino eseguire il test utilizzando un&#39;istanza di sviluppo dell&#39;applicazione non AEM (in esecuzione sul laptop o in hosting) che esegue richieste a un AEM di sviluppo come ambiente di sviluppo Cloud Service. Tuttavia, poiché gli sviluppatori non dispongono necessariamente dell&#39;accesso al ruolo di amministratore per l&#39;AEM come ambiente di sviluppo Cloud Service, non è possibile supporre che possano generare il portatore JWT descritto nel normale flusso server-to-server. Forniamo quindi un meccanismo che consente a uno sviluppatore di generare direttamente un token di accesso da utilizzare nelle richieste di AEM come ambienti di Cloud Service a cui hanno accesso. Per informazioni sulle autorizzazioni necessarie per utilizzare il AEM come console per sviluppatori di Cloud Service, consultate la [Guida per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md).

>[!NOTE]
>
>Il token è valido per 24 ore dopo il quale deve essere rigenerato utilizzando lo stesso metodo.

Gli sviluppatori possono utilizzare questo token per effettuare chiamate dall&#39;applicazione di prova non AEM a un AEM come ambiente Cloud Service. In genere, lo sviluppatore utilizza questo token con l&#39;applicazione non AEM sul proprio computer portatile. Inoltre, il AEM come cloud è in genere un ambiente non di produzione.

Il flusso di sviluppo prevede i seguenti passaggi:

* Generare un token di accesso dalla console per sviluppatori
* Chiama l&#39;applicazione AEM con il token di accesso.

Gli sviluppatori possono inoltre effettuare chiamate API a un progetto AEM in esecuzione sul computer locale, nel qual caso non è necessario un token di accesso.

### Generazione del token di accesso {#generating-the-access-token}

Fate clic sul pulsante **Ottieni token di sviluppo locale** nella console per sviluppatori per generare un token di accesso.

### Chiama quindi AEM applicazione con un token di accesso {#call-the-aem-application-with-an-access-token}

Eseguite le chiamate API server-to-server appropriate dall&#39;applicazione non AEM a un AEM come ambiente Cloud Service, incluso il token di accesso nell&#39;intestazione. Quindi, per l&#39;intestazione &quot;Autorizzazione&quot;, utilizzate il valore `"Bearer <access_token>"`.

## Revoca credenziali di servizio {#service-credentials-revocation}

Se il token del portatore JWT deve essere revocato, invia una richiesta all&#39;assistenza clienti.