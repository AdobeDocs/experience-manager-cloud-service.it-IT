---
title: Generazione dei token di accesso per le API lato server (legacy)
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT sicuro
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Generazione dei token di accesso per le API lato server (legacy) {#generating-access-tokens-for-server-side-apis-legacy}

Alcune architetture si basano sull’esecuzione di chiamate ad AEM as a Cloud Service da un’applicazione ospitata su un server al di fuori dell’infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e quindi invia richieste API ad AEM as a Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare i token necessari per il processo di autenticazione.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=it#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flusso server-to-server {#the-server-to-server-flow}

Un utente con ruolo di amministratore dell’organizzazione IMS e che è anche membro del profilo di prodotto Utenti di AEM o Amministratori di AEM nell’istanza di authoring di AEM può generare una credenziale AEM as a Cloud Service. Tali credenziali possono essere recuperate in seguito da un utente con il ruolo di amministratore dell’ambiente AEM as a Cloud Service e devono essere installate sul server e trattate con attenzione come chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API AEM as a Cloud Service. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con IMS per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione Bearer per effettuare richieste ad AEM as a Cloud Service. Le credenziali scadono dopo un anno per impostazione predefinita, ma possono essere aggiornate quando necessario. Vedere [Aggiorna credenziali](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recuperare le credenziali per AEM as a Cloud Service da Developer Console
* Installare le credenziali per AEM as a Cloud Service su un server non AEM effettuando chiamate ad AEM
* Generare un token JWT e scambiarlo con un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell&#39;API AEM con il token di accesso come token di autenticazione Bearer
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali di AEM as a Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla Console per sviluppatori di AEM as a Cloud Service possono visualizzare la scheda integrazioni in Developer Console per un determinato ambiente e due pulsanti. Un utente con il ruolo di amministratore dell&#39;ambiente AEM as a Cloud Service può fare clic sul pulsante **Genera credenziali del servizio** per generare e visualizzare il codice JSON delle credenziali del servizio. Il codice JSON contiene tutte le informazioni necessarie per il server non AEM, inclusi l’ID client, il segreto client, la chiave privata, il certificato e la configurazione per i livelli di authoring e pubblicazione dell’ambiente, indipendentemente dalla selezione del pod.

![Generazione JWT](assets/JWTtoken3.png)

L’output è simile al seguente:

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

Dopo la generazione, le credenziali possono essere recuperate in un secondo momento premendo il pulsante **Ottieni credenziali servizio** nella stessa posizione.

>[!IMPORTANT]
>
>Un amministratore dell’organizzazione IMS, in genere l’utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager, che deve anche essere membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author, accede a Developer Console. Quindi devono fare clic sul pulsante **Genera credenziali del servizio** in modo che le credenziali vengano generate e successivamente recuperate da un utente con autorizzazioni di amministratore per l&#39;ambiente AEM as a Cloud Service. Se l’amministratore dell’organizzazione IMS non ha eseguito questa attività, un messaggio informa che è necessario il ruolo di amministratore dell’organizzazione IMS.

### Installare le credenziali del servizio AEM su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L’applicazione non AEM che effettua chiamate ad AEM dovrebbe essere in grado di accedere alle credenziali di AEM as a Cloud Service, trattandola come un segreto.

### Generare un token JWT e scambiarlo con un token di accesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilizza le credenziali per creare un token JWT in una chiamata al servizio IMS di Adobe per recuperare un token di accesso, valido per 24 ore.

È possibile scambiare le credenziali del servizio AEM CS con un token di accesso utilizzando esempi di codice progettati a tale scopo. Il codice di esempio è disponibile dall&#39;[archivio GitHub pubblico di Adobe](https://github.com/adobe/aemcs-api-client-lib), che contiene esempi di codice che è possibile copiare e adattare per i propri progetti. Questo archivio contiene un codice di esempio da usare come riferimento e non viene mantenuto come dipendenza dalla libreria pronta per la produzione.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
// Sample code adapted from Adobe's GitHub repository
const exchange = require("./your-local-aemcs-client"); // Copy and adapt the code from the GitHub repository

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

Lo stesso scambio può essere eseguito in qualsiasi lingua in grado di generare un token JWT firmato con il formato corretto e di chiamare le API di scambio di token IMS.

Il token di accesso definisce quando scade, in genere 24 ore. Nell’archivio Git è presente un codice di esempio per gestire un token di accesso e aggiornarlo prima della scadenza.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Effettua le chiamate API server-to-server appropriate a un ambiente AEM as a Cloud Service, incluso il token di accesso nell’intestazione. Per l&#39;intestazione &quot;Authorization&quot;, utilizzare il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Impostare le autorizzazioni appropriate per l’utente dell’account tecnico in AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Dopo aver creato l&#39;utente dell&#39;account tecnico in AEM (si verifica dopo la prima richiesta con il token di accesso corrispondente), l&#39;utente dell&#39;account tecnico deve disporre delle autorizzazioni appropriate per **in** AEM.

Per impostazione predefinita, nel servizio AEM Author l’utente dell’account tecnico viene aggiunto al gruppo di utenti Collaboratori, che fornisce l’accesso in lettura ad AEM.

Questo utente account tecnico in AEM può essere ulteriormente fornito con autorizzazioni utilizzando i metodi usuali.

## Flusso per sviluppatori {#developer-flow}

Gli sviluppatori devono testare utilizzando un’istanza di sviluppo della loro applicazione non AEM (in esecuzione sul loro laptop o in hosting) che invia richieste a un ambiente di sviluppo AEM as a Cloud Service. Tuttavia, poiché gli sviluppatori non dispongono necessariamente delle autorizzazioni per il ruolo di amministratore IMS, Adobe non può presumere che possano generare il Bearer JWT descritto nel normale flusso server-to-server. Pertanto, Adobe fornisce a uno sviluppatore un meccanismo che consente di generare direttamente un token di accesso che può essere utilizzato nelle richieste inviate a un ambiente AEM as a Cloud Service a cui ha accesso.

Per informazioni sulle autorizzazioni necessarie per utilizzare la console per sviluppatori di AEM as a Cloud Service, consulta la [documentazione sulle linee guida per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

>[!NOTE]
>
>Il token di accesso per lo sviluppo locale è valido per un massimo di 24 ore, al termine delle quali deve essere rigenerato con lo stesso metodo.

Gli sviluppatori possono utilizzare questo token per effettuare chiamate dall’applicazione di test non AEM a un ambiente AEM as a Cloud Service. In genere, lo sviluppatore utilizza questo token con l’applicazione non AEM sul proprio laptop. Inoltre, AEM as a Cloud è in genere un ambiente non di produzione.

Il flusso per sviluppatori prevede i seguenti passaggi:

* Generare un token di accesso da Developer Console
* Chiama l’applicazione AEM con il token di accesso.

Gli sviluppatori possono anche effettuare chiamate API a un progetto AEM in esecuzione sul proprio computer locale, nel qual caso non è necessario un token di accesso.

### Generazione del token di accesso {#generating-the-access-token}

Per generare un token di accesso, in Developer Console fare clic su **Ottieni token di sviluppo locale**.

### Chiama l’applicazione AEM con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettua le chiamate API server-to-server appropriate dall’applicazione non AEM a un ambiente AEM as a Cloud Service, incluso il token di accesso nell’intestazione. Per l&#39;intestazione &quot;Authorization&quot;, utilizzare il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali in AEM as a Cloud Service scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori possono aggiornare le credenziali ed estenderne la disponibilità per un altro anno. Utilizza **Aggiorna credenziali servizio** dalla scheda **Integrazioni** in Developer Console, come illustrato di seguito.

![Aggiornamento credenziali](assets/credential-refresh.png)

Dopo aver premuto il pulsante, viene generato un nuovo set di credenziali. Puoi aggiornare l’archiviazione segreta con le nuove credenziali e verificare che funzionino correttamente.

>[!NOTE]
>
> Dopo aver fatto clic sul pulsante **Aggiorna credenziali del servizio**, le vecchie credenziali rimangono registrate fino alla scadenza, ma solo il set più recente è disponibile per essere visualizzato da Developer Console in qualsiasi momento.

## Revoca credenziali del servizio {#service-credentials-revocation}

Se le credenziali devono essere revocate, è necessario inviare una richiesta all’assistenza clienti seguendo la procedura riportata di seguito:

1. Disattiva l’utente dell’account tecnico per Adobe Admin Console nell’interfaccia utente:
   * In Cloud Manager, premi il pulsante **...** accanto al tuo ambiente. Questa azione apre la pagina dei profili di prodotto
   * Ora fai clic sul profilo **Utenti AEM** per visualizzare un elenco degli utenti
   * Fai clic sulla scheda **Credenziali API**, quindi individua l&#39;utente dell&#39;account tecnico appropriato ed eliminalo
2. Contatta l’Assistenza clienti e richiedi l’eliminazione delle credenziali del servizio per tale ambiente specifico
3. Infine, puoi generare nuovamente le credenziali, come descritto in questa documentazione. Inoltre, accertati che il nuovo utente dell’account tecnico creato disponga delle autorizzazioni appropriate.
