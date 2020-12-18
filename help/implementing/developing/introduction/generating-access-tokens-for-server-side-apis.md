---
title: Generazione di token di accesso per le API lato server
description: Scoprite come facilitare la comunicazione tra un server di terze parti e AEM come Cloud Service generando un token JWT protetto
translation-type: tm+mt
source-git-commit: 251f5de85d63f6afd730fc450fe2b5a06bc90c38
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Introduzione {#introduction}

>[!IMPORTANT]
>
>Questa funzione non è ancora disponibile. Per un elenco aggiornato delle funzioni, vedere le [Note sulla versione](/help/release-notes/release-notes-cloud/release-notes-current.md).

Alcune architetture si basano sull&#39;effettuazione di chiamate a AEM come Cloud Service da un&#39;applicazione ospitata su un server esterno all&#39;infrastruttura AEM. Ad esempio, un&#39;applicazione mobile che chiama un server, che quindi esegue richieste API da AEM come Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. Il AEM come Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare i token necessari per il processo di autenticazione.

## Flusso server {#the-server-to-server-flow}

Un utente con il ruolo di amministratore può generare un token JWT al portatore, che deve essere installato sul server e trattato attentamente come una chiave segreta. Il token JWT al portatore dovrebbe essere scambiato con IMS per un token di accesso, che dovrebbe essere incluso nella richiesta di AEM come Cloud Service.

Il flusso server-to-server comporta i seguenti passaggi:

* Generare il token JWT al portatore dalla console per sviluppatori
* Installare il token su un server non AEM che effettua chiamate a AEM
* Scambiare il token JWT al portatore per un token di accesso utilizzando  Adobi  API IMS
* Chiamata dell&#39;API AEM

### Generazione del token del portatore JWT {#generating-the-jwt-bearer-token}

Gli utenti con il ruolo di amministratore per un&#39;organizzazione visualizzeranno la scheda integrazioni nella console dello sviluppatore per un determinato ambiente, oltre a due pulsanti. Facendo clic sul pulsante **Ottieni credenziali servizio** verranno generate la chiave privata, il certificato e la configurazione per i livelli di creazione e pubblicazione dell&#39;ambiente, indipendentemente dalla selezione del contenitore.

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

### Installare il token su un server non AEM {#install-the-token-on-a-non-aem-server}

L&#39;applicazione che effettua chiamate a AEM non AEM deve installare il token JWT al portatore, trattandolo come un segreto.

### Scambio del token JWT per un token di accesso {#exchange-the-jwt-token-for-an-access-token}

Includete il token JWT in una chiamata al servizio  Adobe  IMS per recuperare un token di accesso, valido per 24 ore.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Eseguite le chiamate API server-to-server appropriate a un AEM come ambiente di Cloud Service, incluso il token di accesso nell&#39;intestazione. Quindi, per l&#39;intestazione &quot;Autorizzazione&quot;, utilizzate il valore `"Bearer <access_token>"`.

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

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

## Revoca token del portatore JWT {#jwt-bearer-token-revocation}

Se il token del portatore JWT deve essere revocato, invia una richiesta all&#39;assistenza clienti.