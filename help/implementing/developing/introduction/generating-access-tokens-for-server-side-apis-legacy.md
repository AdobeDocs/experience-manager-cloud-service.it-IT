---
title: Generazione dei token di accesso per le API lato server (legacy)
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT sicuro
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Generazione dei token di accesso per le API lato server (legacy) {#generating-access-tokens-for-server-side-apis-legacy}

Alcune architetture si basano sull&#39;effettuare chiamate all&#39;AEM as a Cloud Service da un&#39;applicazione ospitata su un server al di fuori dell&#39;infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e che quindi rende as a Cloud Service le richieste API all’AEM.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. L&#39;AEM as a Cloud Service [Console per sviluppatori](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare i token necessari per il processo di autenticazione.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flusso server-to-server {#the-server-to-server-flow}

Un utente con ruolo di amministratore dell’organizzazione IMS e che è anche membro del profilo di prodotto Utenti AEM o Amministratori AEM in AEM Author può generare una credenziale AEM as a Cloud Service. Tali credenziali possono essere recuperate in seguito da un utente con il ruolo di amministratore dell’ambiente as a Cloud Service dell’AEM e devono essere installate sul server e trattate con attenzione come chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API as a Cloud Service per AEM. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con IMS per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione Bearer per rendere as a Cloud Service le richieste all’AEM. Le credenziali scadono dopo un anno per impostazione predefinita, ma possono essere aggiornate quando necessario, come descritto [qui](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recupera le credenziali per AEM as a Cloud Service da Developer Console
* Installare le credenziali per AEM as a Cloud Service su un server non AEM che effettua chiamate all&#39;AEM
* Generare un token JWT e scambiarlo con un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell&#39;API AEM con il token di accesso come token di autenticazione Bearer
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali as a Cloud Service dell’AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla Console per sviluppatori as a Cloud Service all’AEM possono visualizzare la scheda integrazioni nella Console per sviluppatori per un determinato ambiente e due pulsanti. L’utente con il ruolo di amministratore dell’ambiente as a Cloud Service dell’AEM può fare clic sul pulsante **Genera credenziali servizio** per generare e visualizzare il codice json delle credenziali del servizio. Il codice JSON contiene tutte le informazioni necessarie per il server non AEM, inclusi l’ID client, il segreto client, la chiave privata, il certificato e la configurazione per i livelli di authoring e pubblicazione dell’ambiente, indipendentemente dalla selezione del pod.

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

Una volta generate, le credenziali possono essere recuperate in un secondo momento premendo il tasto **Ottieni credenziali servizio** nella stessa posizione.

>[!IMPORTANT]
>
>Un amministratore dell’organizzazione IMS, in genere l’utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager, che deve anche essere membro del profilo di prodotto Utenti AEM o Amministratori AEM in AEM Author, accede a Console sviluppatori. Quindi devono fare clic su **Genera credenziali servizio** affinché le credenziali vengano generate e successivamente recuperate da un utente con autorizzazioni di amministratore per l’ambiente as a Cloud Service dell’AEM. Se l’amministratore dell’organizzazione IMS non ha eseguito questa attività, un messaggio informa che è necessario il ruolo di amministratore dell’organizzazione IMS.

### Installare le credenziali del servizio AEM su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L&#39;applicazione non AEM che effettua chiamate all&#39;AEM dovrebbe essere in grado di accedere alle credenziali dell&#39;AEM as a Cloud Service, trattandolo come un segreto.

### Generare un token JWT e scambiarlo con un token di accesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Utilizza le credenziali per creare un token JWT in una chiamata al servizio IMS di Adobe per recuperare un token di accesso, valido per 24 ore.

Le credenziali del servizio CS AEM possono essere scambiate con un token di accesso utilizzando le librerie client progettate a questo scopo. Le librerie client sono disponibili da [Archivio GitHub pubblico di Adobe](https://github.com/adobe/aemcs-api-client-lib), che contiene orientamenti più dettagliati e informazioni aggiornate.

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

Lo stesso scambio può essere eseguito in qualsiasi lingua in grado di generare un token JWT firmato con il formato corretto e di chiamare le API di scambio di token IMS.

Il token di accesso definisce quando scade, in genere 24 ore. Nell’archivio Git è presente un codice di esempio per gestire un token di accesso e aggiornarlo prima della scadenza.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Effettua le chiamate API server-to-server appropriate a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Authorization&quot;, utilizza il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Impostare le autorizzazioni appropriate per l’utente dell’account tecnico in AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Dopo che l’utente dell’account tecnico è stato creato in AEM (si verifica dopo la prima richiesta con il token di accesso corrispondente), deve disporre delle autorizzazioni appropriate **in** AEM.

Per impostazione predefinita, nel servizio AEM Author l’utente dell’account tecnico viene aggiunto al gruppo di utenti Collaboratori, che fornisce accesso in lettura all’AEM.

Questo utente account tecnico in AEM può essere ulteriormente fornito con autorizzazioni utilizzando i metodi usuali.

## Flusso per sviluppatori {#developer-flow}

Gli sviluppatori devono testare utilizzando un’istanza di sviluppo della loro applicazione non AEM (in esecuzione sul loro laptop o in hosting) che invia richieste a un ambiente di sviluppo as a Cloud Service AEM per lo sviluppo. Tuttavia, poiché gli sviluppatori non dispongono necessariamente delle autorizzazioni per il ruolo di amministratore IMS, Adobe non può presumere che possano generare il Bearer JWT descritto nel normale flusso server-to-server. Così, Adobe fornisce un meccanismo che consente a uno sviluppatore di generare direttamente un token di accesso che può essere utilizzato nelle richieste a un ambiente as a Cloud Service AEM a cui ha accesso.

Consulta la [Documentazione sulle linee guida per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) per informazioni sulle autorizzazioni necessarie per utilizzare la console per sviluppatori AEM as a Cloud Service.

>[!NOTE]
Il token di accesso per lo sviluppo locale è valido per un massimo di 24 ore, al termine delle quali deve essere rigenerato con lo stesso metodo.

Gli sviluppatori possono utilizzare questo token per effettuare chiamate dall’applicazione di test non AEM a un ambiente as a Cloud Service AEM. In genere, lo sviluppatore utilizza questo token con l’applicazione non AEM sul proprio laptop. Inoltre, AEM as a Cloud è in genere un ambiente non di produzione.

Il flusso per sviluppatori prevede i seguenti passaggi:

* Generare un token di accesso da Developer Console
* Chiama l’applicazione AEM con il token di accesso.

Gli sviluppatori possono anche effettuare chiamate API a un progetto AEM in esecuzione sul proprio computer locale, nel qual caso non è necessario un token di accesso.

### Generazione del token di accesso {#generating-the-access-token}

Per generare un token di accesso, nella Console per sviluppatori fai clic su **Ottieni token di sviluppo locale**.

### Chiama l’applicazione AEM con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettuare le chiamate API server-to-server appropriate dall’applicazione non AEM a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Authorization&quot;, utilizza il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali sull&#39;as a Cloud Service AEM scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori possono aggiornare le credenziali ed estenderne la disponibilità per un altro anno. Utilizzare **Aggiorna credenziali servizio** dal **Integrazioni** nella Console per sviluppatori, come illustrato di seguito.

![Aggiornamento credenziali](assets/credential-refresh.png)

Dopo aver premuto il pulsante, verrà generato un nuovo set di credenziali. Puoi aggiornare l’archiviazione segreta con le nuove credenziali e verificare che funzionino correttamente.

>[!NOTE]
Dopo aver fatto clic su **Aggiorna credenziali servizio** , le vecchie credenziali rimangono registrate fino alla scadenza, ma solo il set più recente è disponibile per essere visualizzato da Console sviluppatori in qualsiasi momento.

## Revoca credenziali del servizio {#service-credentials-revocation}

Se le credenziali devono essere revocate, è necessario inviare una richiesta all’assistenza clienti seguendo la procedura riportata di seguito:

1. Disattiva l’utente dell’account tecnico per Adobe Admin Console nell’interfaccia utente:
   * In Cloud Manager, premi **...** accanto all’ambiente. Questa azione apre la pagina dei profili di prodotto
   * A questo punto, fai clic su **Utenti AEM** per visualizzare un elenco degli utenti
   * Fai clic su **Credenziali API** , quindi individuare l&#39;utente dell&#39;account tecnico appropriato ed eliminarlo
2. Contatta l’Assistenza clienti e richiedi l’eliminazione delle credenziali del servizio per tale ambiente specifico
3. Infine, puoi generare nuovamente le credenziali, come descritto in questa documentazione. Inoltre, accertati che il nuovo utente dell’account tecnico creato disponga delle autorizzazioni appropriate.
