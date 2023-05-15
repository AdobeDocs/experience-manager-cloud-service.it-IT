---
title: Generazione di token di accesso per API lato server (legacy)
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT protetto
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Generazione di token di accesso per API lato server (legacy) {#generating-access-tokens-for-server-side-apis-legacy}

Alcune architetture si basano sull&#39;effettuazione di chiamate a AEM as a Cloud Service da un&#39;applicazione ospitata su un server al di fuori dell&#39;infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e quindi invia richieste API a AEM as a Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. Il AEM as a Cloud Service [Console per sviluppatori](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare token necessari per il processo di autenticazione.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flusso server-to-server {#the-server-to-server-flow}

Un utente con un ruolo di amministratore organizzazione IMS e che è anche membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author può generare una credenziale as a Cloud Service AEM. Tale credenziale può essere successivamente recuperata da un utente con il ruolo di amministratore dell’ambiente as a Cloud Service AEM e deve essere installata sul server e deve essere trattata con attenzione come una chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API as a Cloud Service AEM. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con IMS per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione portatore per effettuare richieste a AEM as a Cloud Service. Le credenziali scadono dopo un anno per impostazione predefinita, ma possono essere aggiornate quando necessario, come descritto [qui](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recupera le credenziali per AEM as a Cloud Service da Developer Console
* Installa le credenziali per AEM as a Cloud Service su un server non AEM che effettua chiamate a AEM
* Genera un token JWT e scambia tale token per un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell’API AEM con il token di accesso come token di autenticazione portatore
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla AEM console per sviluppatori as a Cloud Service visualizzano la scheda integrazioni nella Console per sviluppatori per un determinato ambiente e due pulsanti. Un utente con il AEM ruolo di amministratore dell’ambiente as a Cloud Service può fare clic sul pulsante **Genera credenziali del servizio** per generare e visualizzare il json delle credenziali del servizio. Il json contiene tutte le informazioni necessarie per il server non AEM, inclusi ID client, segreto client, chiave privata, certificato e configurazione per i livelli di authoring e pubblicazione dell’ambiente, indipendentemente dalla selezione del pod.

![Generazione JWT](assets/JWTtoken3.png)

L&#39;output è simile al seguente:

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

Dopo la generazione, è possibile recuperare le credenziali in un secondo momento premendo il pulsante **Ottieni credenziali servizio** nella stessa posizione.

>[!IMPORTANT]
>
>Un amministratore organizzazione IMS, in genere l’utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager, che deve anche essere membro del profilo di prodotto Utenti AEM o Amministratori su AEM Author, accede alla Console per sviluppatori. Quindi devono fare clic sul pulsante **Genera credenziali del servizio** in modo che le credenziali vengano generate e successivamente recuperate da un utente con autorizzazioni di amministratore per l’ambiente AEM as a Cloud Service. Se l’amministratore organizzazione IMS non ha eseguito questa operazione, un messaggio li informa che è necessario il ruolo Amministratore organizzazione IMS.

### Installare le credenziali del servizio AEM su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L&#39;applicazione non AEM che effettua chiamate a AEM dovrebbe essere in grado di accedere alle credenziali di AEM as a Cloud Service, trattandole come un segreto.

### Generare un token JWT e sostituirlo con un token di accesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilizza le credenziali per creare un token JWT in una chiamata al servizio IMS di Adobe per recuperare un token di accesso, valido per 24 ore.

Le credenziali AEM del servizio CS possono essere scambiate per un token di accesso utilizzando le librerie client progettate a tal fine. Le librerie client sono disponibili da [Archivio GitHub pubblico di Adobe](https://github.com/adobe/aemcs-api-client-lib), che contiene informazioni più dettagliate e informazioni più aggiornate.

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

Il token di accesso definisce quando scade, che in genere dura 24 ore. Nell’archivio Git è presente un codice di esempio per gestire un token di accesso e aggiornarlo prima della scadenza.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Effettua le chiamate API da server a server appropriate a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione . Quindi, per l’intestazione &quot;Autorizzazione&quot;, utilizza il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Imposta le autorizzazioni appropriate per l’utente dell’account tecnico in AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Dopo che l’utente dell’account tecnico è stato creato in AEM (si verifica dopo la prima richiesta con il token di accesso corrispondente), l’utente dell’account tecnico deve essere autorizzato correttamente **in** AEM.

Per impostazione predefinita, nel servizio AEM Author, l’utente dell’account tecnico viene aggiunto al gruppo di utenti Collaboratori , che fornisce AEM di accesso in lettura.

Questo utente tecnico dell’account in AEM può essere ulteriormente dotato di autorizzazioni utilizzando i metodi consueti.

## Flusso degli sviluppatori {#developer-flow}

Gli sviluppatori devono eseguire il test utilizzando un&#39;istanza di sviluppo della propria applicazione non AEM (in esecuzione sul proprio laptop o in hosting) che effettua richieste a un ambiente di sviluppo AEM ambiente di sviluppo as a Cloud Service. Tuttavia, poiché gli sviluppatori non dispongono necessariamente delle autorizzazioni per il ruolo di amministratore IMS, l’Adobe non può presumere che possano generare il portatore JWT descritto nel flusso regolare da server a server. Pertanto, Adobe fornisce a uno sviluppatore un meccanismo per generare direttamente un token di accesso che può essere utilizzato nelle richieste a un ambiente as a Cloud Service AEM a cui ha accesso.

Consulta la sezione [Documentazione sulle linee guida per gli sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) per informazioni sulle autorizzazioni necessarie per utilizzare la AEM console per sviluppatori as a Cloud Service.

>[!NOTE]
Il token di accesso allo sviluppo locale è valido per un massimo di 24 ore dopo il quale deve essere rigenerato utilizzando lo stesso metodo.

Gli sviluppatori possono utilizzare questo token per effettuare chiamate dalla propria applicazione di test non AEM a un ambiente as a Cloud Service AEM. In genere, lo sviluppatore utilizza questo token con l’applicazione non AEM sul proprio laptop. Inoltre, il AEM as a Cloud è in genere un ambiente non di produzione.

Il flusso per gli sviluppatori prevede i seguenti passaggi:

* Generare un token di accesso dalla Console per sviluppatori
* Chiama l&#39;applicazione AEM con il token di accesso.

Gli sviluppatori possono anche effettuare chiamate API a un progetto AEM in esecuzione sul computer locale, nel qual caso non è necessario un token di accesso.

### Generazione del token di accesso {#generating-the-access-token}

Per generare un token di accesso, nella Console per sviluppatori, fai clic su **Ottieni token di sviluppo locale**.

### Chiama quindi AEM applicazione con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettua le chiamate API da server a server appropriate dall’applicazione non AEM a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Autorizzazione&quot;, utilizza il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali in AEM as a Cloud Service scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori hanno la possibilità di aggiornare le credenziali, estendendone la disponibilità per un ulteriore anno. Utilizzo **Aggiorna credenziali del servizio** dal **Integrazioni** in Developer Console, come illustrato di seguito.

![Aggiornamento credenziali](assets/credential-refresh.png)

Dopo aver premuto il pulsante, verrà generato un nuovo set di credenziali. È possibile aggiornare l&#39;archiviazione segreta con le nuove credenziali e verificare che funzionino come dovrebbero.

>[!NOTE]
Dopo aver fatto clic sul pulsante **Aggiorna credenziali del servizio** le vecchie credenziali rimangono registrate fino alla scadenza, ma è disponibile solo il set più recente da visualizzare in qualsiasi momento dalla Console per sviluppatori.

## Revoca delle credenziali del servizio {#service-credentials-revocation}

Se le credenziali devono essere revocate, è necessario inviare una richiesta all’assistenza clienti seguendo questi passaggi:

1. Disattiva l&#39;utente dell&#39;account tecnico per Adobe Admin Console nell&#39;interfaccia utente:
   * In Cloud Manager, premi il pulsante **...** accanto all’ambiente. Questa azione apre la pagina dei profili di prodotto
   * Ora fai clic sul pulsante **Utenti AEM** per visualizzare un elenco degli utenti
   * Fai clic sul pulsante **Credenziali API** , quindi trova l’utente dell’account tecnico appropriato ed eliminalo
2. Contatta l’assistenza clienti e richiedi l’eliminazione delle credenziali del servizio per l’ambiente specifico
3. Infine, puoi generare nuovamente le credenziali, come descritto in questa documentazione. Assicurati anche che il nuovo utente dell’account tecnico creato disponga delle autorizzazioni appropriate.
