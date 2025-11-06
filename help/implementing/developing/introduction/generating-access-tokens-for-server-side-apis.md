---
title: Generazione dei token di accesso per le API lato server
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT sicuro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---

# Generazione dei token di accesso per le API lato server {#generating-access-tokens-for-server-side-apis}

Alcune architetture si basano sull’esecuzione di chiamate ad AEM as a Cloud Service da un’applicazione ospitata su un server al di fuori dell’infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e quindi invia richieste API ad AEM as a Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare i token necessari per il processo di autenticazione.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=it#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flusso server-to-server {#the-server-to-server-flow}

Gli utenti con ruolo di amministratore dell’organizzazione IMS e che sono membri del profilo di prodotto Utenti di AEM o Amministratori di AEM nell’istanza Autore di AEM possono generare un set di credenziali da AEM as a Cloud Service. Ogni credenziale è un payload JSON che include un certificato (la chiave pubblica), una chiave privata e un account tecnico costituito da `clientId` e `clientSecret`. Tali credenziali possono essere recuperate in seguito da un utente con il ruolo di amministratore dell’ambiente AEM as a Cloud Service e devono essere installate in un server non AEM e trattate con attenzione come chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API AEM as a Cloud Service. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con Adobe Identity Management Services (IMS) per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione Bearer per effettuare richieste ad AEM as a Cloud Service. Per impostazione predefinita, il certificato nelle credenziali scade dopo un anno, ma può essere aggiornato quando necessario. Vedere [Aggiorna credenziali](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recuperare le credenziali su AEM as a Cloud Service da Developer Console
* Installare le credenziali per AEM as a Cloud Service su un server non AEM effettuando chiamate ad AEM
* Generare un token JWT e scambiarlo con un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell&#39;API AEM con il token di accesso come token di autenticazione Bearer
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali di AEM as a Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla Console per sviluppatori di AEM as a Cloud Service possono visualizzare la scheda integrazioni in Developer Console per un determinato ambiente. L’utente con il ruolo di amministratore dell’ambiente AEM as a Cloud Service può creare, visualizzare o gestire le credenziali.

Facendo clic su **Crea nuovo account tecnico**, viene creato un set di credenziali che include ID client, segreto client, chiave privata, certificato e configurazione per i livelli di authoring e pubblicazione dell&#39;ambiente, indipendentemente dalla selezione del pod.

![Creazione di un nuovo account tecnico](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Viene visualizzata una nuova scheda del browser con le credenziali. È possibile utilizzare questa visualizzazione per scaricare le credenziali premendo l&#39;icona di download accanto al titolo dello stato:

![Scarica credenziali](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Dopo la creazione, le credenziali verranno visualizzate nella scheda **Account tecnici** della sezione **Integrazioni**:

![Visualizza credenziali](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Gli utenti possono visualizzare le credenziali in un secondo momento utilizzando l’azione Visualizza. Inoltre, come descritto più avanti nell’articolo, gli utenti possono modificare le credenziali per lo stesso account tecnico. Questa operazione viene eseguita creando una chiave privata o un certificato, nei casi in cui il certificato debba essere rinnovato o revocato.

Gli utenti con il ruolo Amministratore dell’ambiente AEM as a Cloud Service possono in seguito creare credenziali per account tecnici aggiuntivi. Questa funzionalità è utile quando diverse API hanno requisiti di accesso diversi. Ad esempio, lettura e scrittura.

>[!NOTE]
>
>I clienti possono creare fino a dieci account tecnici, inclusi quelli già eliminati.

>[!IMPORTANT]
>
>Un amministratore dell’organizzazione IMS (in genere lo stesso utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager), che è anche membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author, deve prima accedere a Developer Console. Quindi, fai clic su **Crea nuovo account tecnico** per le credenziali da generare e recuperare in seguito da un utente con autorizzazioni di amministratore per l&#39;ambiente AEM as a Cloud Service. Se l’amministratore dell’organizzazione IMS non ha ancora creato l’account tecnico, viene visualizzato un messaggio per informare che è necessario il ruolo di amministratore dell’organizzazione IMS.

### Installare le credenziali del servizio AEM su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L’applicazione che effettua chiamate ad AEM dovrebbe essere in grado di accedere alle credenziali per AEM as a Cloud Service, trattandole come un segreto.

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

>[!NOTE]
>Se sono presenti più credenziali, assicurati di fare riferimento al file json appropriato per la chiamata API ad AEM che viene successivamente richiamata.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Effettua le chiamate API server-to-server appropriate a un ambiente AEM as a Cloud Service, incluso il token di accesso nell’intestazione. Per l&#39;intestazione &quot;Authorization&quot;, utilizzare il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Impostare le autorizzazioni appropriate per l’utente dell’account tecnico in AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Innanzitutto, è necessario creare un nuovo profilo di prodotto in Adobe Admin Console.

1. Vai al Adobe Admin Console all&#39;indirizzo [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. Premi il collegamento **Gestisci** nella colonna **Prodotti e servizi** a sinistra.
1. Seleziona **AEM as a Cloud Service**.
1. Premere il pulsante **Nuovo profilo**.

   ![Nuovo profilo](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Denomina il profilo e premi **Salva**.

   ![Salva profilo](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Selezionare il profilo creato dall&#39;elenco dei profili.
1. Selezionare **Aggiungi utente**.

   ![Aggiungi utente](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Aggiungi l&#39;account tecnico creato (in questo caso `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) e fai clic su **Salva**.

   ![Aggiungi account tecnico](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Attendi 10 minuti per rendere effettive le modifiche ed effettua una chiamata API ad AEM con un token di accesso generato dalle nuove credenziali. Come comando cURL, verrebbe rappresentato in modo simile a questo esempio:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Dopo aver eseguito la chiamata API, il profilo di prodotto viene visualizzato come gruppo di utenti nell’istanza di authoring di AEM as a Cloud Service, con l’account tecnico appropriato come membro di tale gruppo.

Per verificare queste informazioni, eseguire le operazioni seguenti:

1. Accedi all’istanza di authoring.
1. Vai a **Strumenti** > **Sicurezza**, quindi fai clic sulla scheda **Gruppi**.
1. Individua il nome del profilo creato nell’elenco dei gruppi e fai clic su di esso:

   ![Profilo gruppo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. Nella finestra seguente, passa alla scheda **Membri** e verifica che l&#39;account tecnico sia elencato correttamente:

   ![Scheda Membri](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


In alternativa, puoi anche verificare che l’account tecnico sia presente nell’elenco dell’utente eseguendo i passaggi seguenti sull’istanza di authoring:

1. Vai a **Strumenti** > **Sicurezza** > **Utenti**.
1. Controlla che l’account tecnico sia l’elenco degli utenti e selezionalo.
1. Fai clic sulla scheda **Gruppi** per verificare che l&#39;utente appartenga al gruppo corrispondente al tuo profilo di prodotto. Questo utente è anche membro di una manciata di altri gruppi, inclusi i collaboratori:

   ![Appartenenza al gruppo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Prima della metà del 2023, prima che fosse possibile creare più credenziali, i clienti non venivano guidati a creare un profilo di prodotto in Adobe Admin Console. Di conseguenza, l’account tecnico non era associato a un gruppo diverso da &quot;Collaboratori&quot; nell’istanza di AEM as a Cloud Service. Per motivi di coerenza, è consigliabile creare un profilo di prodotto in Adobe Admin Console come descritto in precedenza per questo account tecnico e aggiungere l’account tecnico esistente a tale gruppo.

<u>**Impostare le autorizzazioni di gruppo appropriate**</u>

Infine, configura il gruppo con le autorizzazioni appropriate necessarie in modo da poter richiamare o bloccare le API in modo appropriato.

1. Accedi all&#39;istanza di authoring appropriata e passa a **Impostazioni** > **Sicurezza** > **Autorizzazioni**
1. Cerca il nome del gruppo corrispondente al profilo di prodotto nel riquadro a sinistra (in questo caso, API di sola lettura) e selezionalo:

   ![Cerca gruppo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Fare clic sul pulsante Modifica nella finestra seguente:

   ![Modifica autorizzazioni](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifica le autorizzazioni in modo appropriato e fai clic su **Salva**

   ![Conferma modifica autorizzazioni](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Scopri di più su Adobe Identity Management System (IMS) e gli utenti e i gruppi di AEM. Consulta la [documentazione](/help/security/ims-support.md).

## Flusso per sviluppatori {#developer-flow}

È probabile che gli sviluppatori desiderino eseguire il test utilizzando un’istanza di sviluppo della loro applicazione non AEM (in esecuzione sul laptop o in hosting) che invia richieste a un ambiente di sviluppo AEM as a Cloud Service. Tuttavia, poiché gli sviluppatori non dispongono necessariamente delle autorizzazioni per il ruolo di amministratore IMS, Adobe non può presumere che possano generare il Bearer JWT descritto nel normale flusso server-to-server. Pertanto, Adobe fornisce a uno sviluppatore un meccanismo che consente di generare direttamente un token di accesso che può essere utilizzato nelle richieste inviate agli ambienti su AEM as a Cloud Service a cui ha accesso.

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

1. Vai a **Token locale** in **Integrazioni**
1. Fai clic su **Ottieni token di sviluppo locale** in Developer Console per generare un token di accesso.

### Chiamare l’applicazione AEM con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettua le chiamate API server-to-server appropriate dall’applicazione non AEM a un ambiente AEM as a Cloud Service, incluso il token di accesso nell’intestazione. Per l&#39;intestazione &quot;Authorization&quot;, utilizzare il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali su AEM as a Cloud Service scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori possono aggiornare le credenziali ed estenderne la disponibilità per un altro anno.

Per ottenere questa estensione di aggiornamento, effettua le seguenti operazioni:

* Utilizza il pulsante **Aggiungi certificato** in **Integrazioni** - **Account tecnici** in Developer Console, come illustrato di seguito

  ![Aggiornamento credenziali](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Dopo aver premuto il pulsante, viene generato un set di credenziali che include un nuovo certificato. Installa le nuove credenziali sul server off-AEM e assicurati che la connettività sia come previsto, senza rimuovere le vecchie credenziali.
* Assicurati che vengano utilizzate le nuove credenziali invece di quelle precedenti durante la generazione del token di accesso.
* Facoltativamente, revoca (e quindi elimina) il certificato precedente in modo che non possa più essere utilizzato per l’autenticazione con AEM as a Cloud Service.

## Revoca credenziali {#credentials-revocation}

Se la chiave privata è compromessa, è necessario creare le credenziali con un nuovo certificato e una nuova chiave privata. Dopo che l&#39;applicazione utilizza le nuove credenziali per generare i token di accesso, è possibile revocare ed eliminare i vecchi certificati eseguendo le operazioni seguenti:

1. Aggiungi innanzitutto la nuova chiave. Questa chiave genera le credenziali con una nuova chiave privata e un nuovo certificato. La nuova chiave privata è contrassegnata nell&#39;interfaccia utente come **corrente** ed è quindi utilizzata per tutte le nuove credenziali per questo account tecnico in futuro. Le credenziali associate alle chiavi private precedenti sono ancora valide fino alla revoca. Per ottenere questa revoca, seleziona i tre punti (**...**) nell&#39;account tecnico corrente, quindi seleziona **Aggiungi nuova chiave privata**:

   ![Aggiungi nuova chiave privata](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Seleziona **Aggiungi** al prompt seguente:

   ![Conferma l&#39;aggiunta della nuova chiave privata](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Viene aperta una nuova scheda Sfoglia con le nuove credenziali e l&#39;interfaccia utente viene aggiornata per mostrare entrambe le chiavi private con la nuova contrassegnata come **corrente**:

   ![Chiavi private nell&#39;interfaccia utente](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Installa le nuove credenziali sul server non AEM e assicurati che la connettività funzioni come previsto. Per informazioni dettagliate, vedere la [sezione Flusso da server a server](#the-server-to-server-flow).
1. Revocare il certificato precedente selezionando i tre punti (**...**) a destra del certificato e selezionando **Revoca**:

   ![Revoca certificato](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Quindi, confermare la revoca nel seguente prompt premendo il pulsante **Revoca**:

   ![Revoca conferma certificato](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Infine, elimina il certificato compromesso.
