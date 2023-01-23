---
title: Generazione dei token di accesso per le API lato server
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT protetto
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 41458eb1fba12e8ef45a32d3bb6fc5dd732f78ec
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 1%

---

# Generazione dei token di accesso per le API lato server {#generating-access-tokens-for-server-side-apis}

>[!AVAILABILITY]
>
>L&#39;Adobe sta gradualmente estendendo le nuove funzionalità di revoca delle credenziali e delle credenziali multiple descritte in questo articolo. Se, controllando la scheda integrazioni nella console per sviluppatori AEM della tua organizzazione, noterai che la schermata è diversa dalle schermate sottostanti, significa che le nuove modifiche non sono ancora state implementate nell’organizzazione. In questo caso, si prega di fare riferimento al [documentazione legacy](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis-legacy.md).

Alcune architetture si basano sull&#39;effettuazione di chiamate a AEM as a Cloud Service da un&#39;applicazione ospitata su un server al di fuori dell&#39;infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e quindi invia richieste API a AEM as a Cloud Service.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. Il AEM as a Cloud Service [Console per sviluppatori](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare token necessari per il processo di autenticazione.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flusso server-to-server {#the-server-to-server-flow}

Un utente con un ruolo di amministratore organizzazione IMS e che è anche membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author può generare un set di credenziali as a Cloud Service, ciascuna delle quali è un payload JSON che include un certificato (la chiave pubblica), una chiave privata e un account tecnico costituito da un `clientId` e `clientSecret`. Tali credenziali possono essere successivamente recuperate da un utente con il ruolo di amministratore dell’ambiente as a Cloud Service AEM e devono essere installate su un server non AEM e trattate con attenzione come chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API as a Cloud Service AEM. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con Adobe Identity Management Services (IMS) per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione portatore per effettuare richieste a AEM as a Cloud Service. Il certificato nelle credenziali scade dopo un anno per impostazione predefinita, ma possono essere aggiornato quando necessario, come descritto [qui](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recupera le credenziali as a Cloud Service AEM da Developer Console
* Installa le AEM credenziali as a Cloud Service su un server non AEM che effettua chiamate a AEM
* Genera un token JWT e scambia tale token per un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell’API AEM con il token di accesso come token di autenticazione portatore
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla AEM console per sviluppatori as a Cloud Service visualizzeranno la scheda integrazioni in Developer Console per un determinato ambiente. Un utente con il AEM ruolo di amministratore dell&#39;ambiente as a Cloud Service può creare, visualizzare o gestire le credenziali.

Fai clic su **Crea nuovo account tecnico** verrà creato un nuovo set di credenziali che include ID client, segreto client, chiave privata, certificato e configurazione per i livelli di authoring e pubblicazione dell’ambiente, indipendentemente dalla selezione del pod.

![Creazione di un nuovo account tecnico](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Viene aperta una nuova scheda del browser in cui vengono visualizzate le credenziali. Per scaricare le credenziali, è possibile utilizzare questa visualizzazione premendo l&#39;icona di download accanto al titolo dello stato:

![Credenziali di download](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Dopo la creazione, le credenziali verranno visualizzate sotto la **Account tecnici** nella scheda **Integrazioni** sezione:

![Visualizza credenziali](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Gli utenti potranno quindi visualizzare le credenziali utilizzando l’azione Visualizza . Inoltre, come descritto più avanti nell’articolo, gli utenti possono modificare le credenziali per lo stesso account tecnico creando una nuova chiave privata o certificato, per i casi in cui il certificato deve essere rinnovato o revocato.

Gli utenti con il AEM ruolo di amministratore dell’ambiente as a Cloud Service possono successivamente creare nuove credenziali per account tecnici aggiuntivi. Questa funzione è utile quando le diverse API hanno requisiti di accesso diversi. Ad esempio, leggere e leggere-scrivere.

>[!NOTE]
>
>I clienti possono creare fino a 10 account tecnici, inclusi quelli che sono già stati eliminati.

>[!IMPORTANT]
>
>Un amministratore organizzazione IMS (in genere lo stesso utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager), che deve anche essere membro del AEM profilo di prodotto Utenti o Amministratori su AEM Author, deve prima accedere alla Console per sviluppatori e fare clic sul pulsante **Crea nuovo account tecnico** affinché le credenziali vengano generate e successivamente recuperate da un utente con autorizzazioni di amministratore nell’ambiente as a Cloud Service AEM. Se l’amministratore dell’organizzazione IMS non ha eseguito questa operazione, un messaggio li informa della necessità del ruolo di amministratore organizzazione IMS.

### Installare le credenziali del servizio AEM su un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L&#39;applicazione che effettua chiamate a AEM dovrebbe essere in grado di accedere alle credenziali as a Cloud Service AEM, trattandole come un segreto.

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

>[!NOTE]
>Se sono presenti più credenziali, assicurati di fare riferimento al file json appropriato per la chiamata API a AEM che verrà successivamente richiamata.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Effettua le chiamate API da server a server appropriate a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione . Quindi, per l’intestazione &quot;Autorizzazione&quot;, utilizza il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Imposta le autorizzazioni appropriate per l’utente dell’account tecnico in AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Innanzitutto, devi creare un nuovo profilo di prodotto in Adobe Admin Console. Per ottenere questo risultato, procedi come segue:

1. Vai a Adobe Admin Console all&#39;indirizzo [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. Premere **Gestisci** link sotto **Prodotti e servizi** a sinistra.
1. Seleziona **AEM as a Cloud Service**
1. Premere **Nuovo profilo** pulsante

   ![Nuovo profilo](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Denomina il profilo e premi **Salva**

   ![Salva profilo](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Seleziona il profilo appena creato dall’elenco dei profili
1. Premere **Aggiungi utente** pulsante

   ![Aggiungi utente](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Aggiungi l’account tecnico appena creato (in questo caso `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) e premere **Salva**

   ![Aggiungi account tecnico](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Attendi 10 minuti prima che le modifiche diventino effettive ed effettua una chiamata API a AEM con un token di accesso generato dalla nuova credenziale. Come comando cURL, viene rappresentato in modo simile a questo esempio:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Dopo aver effettuato la chiamata API, il profilo di prodotto verrà visualizzato come gruppo di utenti nell’istanza di authoring AEM as a Cloud Service, con l’account tecnico appropriato come membro di quel gruppo.

Per verificare questo, devi:

1. Accedi all’istanza di authoring
1. Vai a **Strumenti** - **Sicurezza** e fai clic su **Gruppi** scheda
1. Individua il nome del profilo creato nell’elenco dei gruppi e fai clic su di esso:

   ![Profilo gruppo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. Nella finestra seguente, passa a **Membri** seleziona e controlla se l’account tecnico è elencato correttamente:

   ![Scheda Membri](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


In alternativa, puoi anche verificare che l’account tecnico venga visualizzato nell’elenco degli utenti eseguendo i passaggi seguenti nell’istanza di authoring:

1. Vai a **Strumenti** - **Sicurezza** - **Utenti**
1. Verifica che il tuo account tecnico sia l’elenco degli utenti e fai clic su di esso
1. Fai clic sul pulsante **Gruppi** per verificare che l’utente faccia parte del gruppo corrispondente al tuo profilo di prodotto. Questo utente è anche membro di una manciata di altri gruppi, tra cui collaboratori:

   ![Iscrizione al gruppo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Prima di metà 2023, prima che fosse possibile creare più credenziali, i clienti non erano guidati a creare un profilo di prodotto in Adobe Admin Console e quindi l’account tecnico non era associato a un gruppo diverso da &quot;Collaboratori&quot; nell’istanza as a Cloud Service AEM. Per motivi di coerenza, si consiglia di creare per questo account tecnico un nuovo profilo di prodotto in Adobe Admin Console come descritto in precedenza e di aggiungere l’account tecnico esistente a tale gruppo.

<u>**Impostare le autorizzazioni del gruppo appropriato**</u>

Infine, configura il gruppo con le autorizzazioni appropriate necessarie a per richiamare o bloccare in modo appropriato le API. Per farlo, segui questi passaggi:

1. Accedere all’istanza di authoring appropriata e andare a **Impostazioni** - **Sicurezza** - **Autorizzazioni**
1. Cerca il nome del gruppo corrispondente al profilo di prodotto nel riquadro a sinistra (in questo caso API di sola lettura) e fai clic su di esso:

   ![Cerca gruppo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Fai clic sul pulsante Modifica nella finestra seguente:

   ![Autorizzazioni di modifica](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifica le autorizzazioni in modo appropriato e fai clic su **Salva**

   ![Conferma la modifica delle autorizzazioni](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Ulteriori informazioni su Adobe Identity Management System (IMS) e AEM utenti e gruppi consultando il [documentazione](/help/security/ims-support.md).

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

1. Vai a **Token locale** sotto **Integrazioni**
1. Fai clic sul pulsante **Ottieni token di sviluppo locale** in Developer Console per generare un token di accesso.

### Chiama l&#39;applicazione AEM con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettua le chiamate API da server a server appropriate dall’applicazione non AEM a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Autorizzazione&quot;, utilizza il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali as a Cloud Service AEM scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori hanno la possibilità di aggiornare le credenziali, estendendone la disponibilità per un ulteriore anno.

A questo scopo, puoi:

* Utilizza la **Aggiungi certificato** pulsante sotto **Integrazioni** - **Account tecnici** in Developer Console, come illustrato di seguito

   ![Aggiornamento credenziali](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Dopo aver premuto il pulsante , verrà generato un set di credenziali che include un nuovo certificato. Installa le nuove credenziali sul server off-AEM e assicurati che la connettività sia come previsto, senza rimuovere le vecchie credenziali 
* Assicurati che le nuove credenziali siano utilizzate al posto delle vecchie quando generi il token di accesso
* Facoltativamente, revoca (e quindi elimina) il certificato precedente in modo che non possa più essere utilizzato per l’autenticazione con AEM as a Cloud Service.

## Revoca credenziali {#credentials-revocation}

Se la chiave privata è compromessa, devi creare le credenziali con un nuovo certificato e una nuova chiave privata. Dopo che l’applicazione utilizza le nuove credenziali per generare i token di accesso, puoi revocare ed eliminare i vecchi certificati.

Puoi eseguire questa operazione seguendo questi passaggi:

1. Innanzitutto, aggiungi la nuova chiave. In questo modo verranno generate le credenziali con una nuova chiave privata e un nuovo certificato. La nuova chiave privata verrà contrassegnata nell’interfaccia utente come **attuale** e sarà quindi utilizzato per tutte le nuove credenziali per questo account tecnico in futuro. Le credenziali associate alle chiavi private precedenti rimarranno valide fino alla revoca. Per ottenere questo, premere i tre punti (**...**) nell&#39;account tecnico corrente e premere **Aggiungi nuova chiave privata**:

   ![Aggiungi nuova chiave privata](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Press **Aggiungi** al prompt che segue:

   ![Conferma aggiunta nuova chiave privata](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Viene aperta una nuova scheda con le nuove credenziali e l’interfaccia utente viene aggiornata per mostrare entrambe le chiavi private, con la nuova scheda contrassegnata come **attuale**:

   ![Tasti privati nell’interfaccia utente](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Installa le nuove credenziali sul server non AEM e assicurati che la connettività funzioni come previsto. Consulta la sezione [Sezione Flusso server-to-server](#the-server-to-server-flow) per informazioni dettagliate su come eseguire questa operazione
1. Revoca il vecchio certificato. Per farlo, seleziona i tre punti (**...** a destra del certificato e premendo **Revoca**:

   ![Revoca certificato](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Quindi, confermare la revoca nel seguente prompt premendo il pulsante **Revoca** pulsante:

   ![Revoca della conferma del certificato](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Infine, elimina il certificato compromesso.
