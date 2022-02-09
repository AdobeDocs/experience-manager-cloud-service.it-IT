---
title: Generazione dei token di accesso per le API lato server
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT protetto
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: c4f4ce968c17db1f1185ce7be9cad833eaf0b91b
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 0%

---

# Introduzione {#introduction}

Alcune architetture si basano sull&#39;effettuazione di chiamate a AEM as a Cloud Service da un&#39;applicazione ospitata su un server al di fuori dell&#39;infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e quindi invia richieste API a AEM as a Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. Il AEM as a Cloud Service [Console per sviluppatori](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare token necessari per il processo di autenticazione.

>[!NOTE]
>
>Oltre a questa documentazione, puoi anche consultare l’esercitazione su [Autenticazione basata su token per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

## Flusso server-to-server {#the-server-to-server-flow}

Un utente con un ruolo di amministratore organizzazione IMS e che è anche membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author può generare una credenziale as a Cloud Service AEM. Tale credenziale può essere successivamente recuperata da un utente con il ruolo di amministratore dell&#39;ambiente as a Cloud Service AEM e deve essere installata sul server e deve essere trattata con attenzione come una chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API as a Cloud Service AEM. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con IMS per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione portatore per effettuare richieste a AEM as a Cloud Service. Le credenziali scadono dopo un anno per impostazione predefinita, ma possono essere aggiornate quando necessario, come descritto [qui](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recupera le credenziali as a Cloud Service AEM da Developer Console
* Installa le AEM credenziali as a Cloud Service su un server non AEM che effettua chiamate a AEM
* Genera un token JWT e scambia tale token per un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell’API AEM con il token di accesso come token di autenticazione portatore
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla AEM console per sviluppatori as a Cloud Service visualizzeranno la scheda integrazioni nella Console per sviluppatori per un determinato ambiente, nonché due pulsanti. Un utente con il AEM ruolo di amministratore dell’ambiente as a Cloud Service può fare clic sul pulsante **Genera credenziali del servizio** pulsante per generare e visualizzare il json delle credenziali del servizio, che conterrà tutte le informazioni necessarie per il server non AEM, inclusi ID client, segreto client, chiave privata, certificato e configurazione per i livelli di authoring e pubblicazione dell’ambiente, indipendentemente dalla selezione del pod.

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

Dopo la generazione, è possibile recuperare le credenziali in un secondo momento premendo il pulsante **Ottieni credenziali servizio** nella stessa posizione.

>[!IMPORTANT]
>
>Un amministratore organizzazione IMS (in genere lo stesso utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager), che deve anche essere membro del AEM profilo di prodotto Utenti o Amministratori su AEM Author, deve prima accedere alla Console per sviluppatori e fare clic sul pulsante **Genera credenziali del servizio** affinché le credenziali vengano generate e successivamente recuperate da un utente con autorizzazioni di amministratore nell’ambiente as a Cloud Service AEM. Se l’amministratore dell’organizzazione IMS non ha eseguito questa operazione, un messaggio li informa della necessità del ruolo di amministratore organizzazione IMS.

### Installare le credenziali del servizio AEM su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L&#39;applicazione non AEM che effettua chiamate a AEM dovrebbe essere in grado di accedere alle credenziali as a Cloud Service AEM, trattandole come un segreto.

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

Una volta creato in AEM l’utente dell’account tecnico (questo si verifica dopo la prima richiesta con il token di accesso corrispondente), l’utente dell’account tecnico deve essere autorizzato correttamente **in** AEM.

Per impostazione predefinita, nel servizio AEM Author l’utente dell’account tecnico viene aggiunto al gruppo di utenti Collaboratori , che fornisce AEM di accesso in lettura.

Questo utente tecnico dell’account in AEM può essere ulteriormente dotato di autorizzazioni utilizzando i metodi consueti.

## Flusso degli sviluppatori {#developer-flow}

È probabile che gli sviluppatori desiderino eseguire il test utilizzando un&#39;istanza di sviluppo della propria applicazione non AEM (in esecuzione sul proprio laptop o in hosting) che effettua richieste a uno sviluppo AEM ambiente di sviluppo as a Cloud Service. Tuttavia, poiché gli sviluppatori non dispongono necessariamente delle autorizzazioni per il ruolo di amministratore IMS, non possiamo presumere che possano generare il portatore JWT descritto nel flusso regolare da server a server. Forniamo quindi un meccanismo affinché uno sviluppatore generi direttamente un token di accesso che può essere utilizzato nelle richieste per AEM gli ambienti as a Cloud Service a cui ha accesso.

Consulta la sezione [Documentazione sulle linee guida per gli sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) per informazioni sulle autorizzazioni necessarie per utilizzare la AEM console per sviluppatori as a Cloud Service.

>[!NOTE]
>
>Il token di accesso allo sviluppo locale è valido per un massimo di 24 ore dopo il quale deve essere rigenerato utilizzando lo stesso metodo.

Gli sviluppatori possono utilizzare questo token per effettuare chiamate dalla propria applicazione di test non AEM a un ambiente as a Cloud Service AEM. In genere, lo sviluppatore utilizza questo token con l’applicazione non AEM sul proprio laptop. Inoltre, il AEM as a Cloud è in genere un ambiente non di produzione.

Il flusso per gli sviluppatori prevede i seguenti passaggi:

* Generare un token di accesso dalla Console per sviluppatori
* Chiama l&#39;applicazione AEM con il token di accesso.

Gli sviluppatori possono anche effettuare chiamate API a un progetto AEM in esecuzione sul computer locale, nel qual caso non è necessario un token di accesso.

### Generazione del token di accesso {#generating-the-access-token}

Fai clic sul pulsante **Ottieni token di sviluppo locale** in Developer Console per generare un token di accesso.

### Chiama quindi AEM applicazione con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettua le chiamate API da server a server appropriate dall’applicazione non AEM a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Autorizzazione&quot;, utilizza il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali as a Cloud Service AEM scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori hanno la possibilità di aggiornare le credenziali, estendendone la disponibilità per un ulteriore anno.

A questo scopo, puoi utilizzare la funzione **Aggiorna credenziali del servizio** dal pulsante **Integrazioni** in Developer Console, come illustrato di seguito.

![Aggiornamento credenziali](assets/credential-refresh.png)

Dopo aver premuto il pulsante, verrà generato un nuovo set di credenziali. È possibile aggiornare l&#39;archiviazione segreta con le nuove credenziali e verificare che funzionino come dovrebbero.

>[!NOTE]
>
> Dopo aver fatto clic sul pulsante **Aggiorna credenziali del servizio** le vecchie credenziali rimangono registrate fino alla scadenza, ma è disponibile solo il set più recente da visualizzare in qualsiasi momento dalla Console per sviluppatori.

## Revoca delle credenziali del servizio {#service-credentials-revocation}

Se le credenziali devono essere revocate, è necessario inviare una richiesta all’assistenza clienti seguendo questi passaggi:

1. Disattiva l&#39;utente dell&#39;account tecnico per Adobe Admin Console nell&#39;interfaccia utente:
   * In Cloud Manager, premi il pulsante **...** accanto all’ambiente. Viene aperta la pagina dei profili di prodotto
   * Ora fai clic sul pulsante **Utenti AEM** per visualizzare un elenco degli utenti
   * Fai clic sul pulsante **Credenziali API** , quindi trova l’utente dell’account tecnico appropriato ed eliminalo
2. Contatta l’assistenza clienti e richiedi l’eliminazione delle credenziali del servizio per l’ambiente specifico
3. Infine, puoi generare nuovamente le credenziali, come descritto in questa documentazione. Assicurati anche che il nuovo utente dell’account tecnico creato disponga delle autorizzazioni appropriate.
