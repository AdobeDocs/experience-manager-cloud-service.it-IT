---
title: Generazione dei token di accesso per le API lato server
description: Scopri come facilitare la comunicazione tra un server di terze parti e AEM as a Cloud Service generando un token JWT sicuro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 1%

---

# Generazione dei token di accesso per le API lato server {#generating-access-tokens-for-server-side-apis}

Alcune architetture si basano sull&#39;effettuare chiamate all&#39;AEM as a Cloud Service da un&#39;applicazione ospitata su un server al di fuori dell&#39;infrastruttura AEM. Ad esempio, un’app mobile che chiama un server e che quindi rende as a Cloud Service le richieste API all’AEM.

Il flusso server-to-server è descritto di seguito, insieme a un flusso semplificato per lo sviluppo. L&#39;AEM as a Cloud Service [Console per sviluppatori](development-guidelines.md#crxde-lite-and-developer-console) viene utilizzato per generare i token necessari per il processo di autenticazione.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Flusso server-to-server {#the-server-to-server-flow}

Un utente con ruolo di amministratore dell’organizzazione IMS e che è anche membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author può generare un set di credenziali AEM as a Cloud Service, ciascuna delle quali è un payload JSON che include un certificato (chiave pubblica), una chiave privata e un account tecnico costituito da un `clientId` e `clientSecret`. Tali credenziali possono essere successivamente recuperate da un utente con il ruolo di amministratore dell’ambiente as a Cloud Service dell’AEM e devono essere installate su un server non AEM e trattate con attenzione come chiave segreta. Questo file in formato JSON contiene tutti i dati necessari per l’integrazione con un’API as a Cloud Service per AEM. I dati vengono utilizzati per creare un token JWT firmato, che viene scambiato con l’Adobe Identity Management Services (IMS) per un token di accesso IMS. Questo token di accesso può quindi essere utilizzato come token di autenticazione Bearer per rendere as a Cloud Service le richieste all’AEM. Per impostazione predefinita, il certificato nelle credenziali scade dopo un anno, ma può essere aggiornato quando necessario, come descritto [qui](#refresh-credentials).

Il flusso server-to-server prevede i seguenti passaggi:

* Recupera le credenziali as a Cloud Service dell’AEM da Console sviluppatori
* Installare le credenziali as a Cloud Service AEM su un server non AEM che effettua chiamate all’AEM
* Generare un token JWT e scambiarlo con un token di accesso utilizzando le API IMS di Adobe
* Chiamata dell&#39;API AEM con il token di accesso come token di autenticazione Bearer
* Impostare le autorizzazioni appropriate per l’utente dell’account tecnico nell’ambiente AEM

### Recupera le credenziali as a Cloud Service dell’AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Gli utenti con accesso alla Console per sviluppatori as a Cloud Service all’AEM visualizzeranno la scheda integrazioni nella Console per sviluppatori per un determinato ambiente. L’utente con il ruolo di amministratore dell’ambiente as a Cloud Service dall’AEM può creare, visualizzare o gestire le credenziali.

Facendo clic su **Crea nuovo account tecnico** , viene creato un nuovo set di credenziali che include id client, segreto client, chiave privata, certificato e configurazione per i livelli Author e Publish dell’ambiente, indipendentemente dalla selezione del pod.

![Creazione di un nuovo account tecnico](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Viene aperta una nuova scheda del browser con le credenziali visualizzate. È possibile utilizzare questa visualizzazione per scaricare le credenziali premendo l&#39;icona di download accanto al titolo dello stato:

![Scarica credenziali](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Dopo la creazione, le credenziali verranno visualizzate nella sezione **Account tecnici** scheda in **Integrazioni** sezione:

![Visualizza credenziali](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Gli utenti possono visualizzare le credenziali in un secondo momento utilizzando l’azione Visualizza. Inoltre, come descritto più avanti nell’articolo, gli utenti possono modificare le credenziali per lo stesso account tecnico creando una nuova chiave privata o un nuovo certificato, nei casi in cui il certificato debba essere rinnovato o revocato.

Gli utenti con il ruolo Amministratore dell’ambiente as a Cloud Service dall’AEM possono in seguito creare nuove credenziali per account tecnici aggiuntivi. Questo è utile quando diverse API hanno requisiti di accesso diversi. Ad esempio, lettura e scrittura.

>[!NOTE]
>
>I clienti possono creare fino a 10 account tecnici, inclusi quelli già eliminati.

>[!IMPORTANT]
>
>Un amministratore dell’organizzazione IMS (in genere lo stesso utente che ha eseguito il provisioning dell’ambiente tramite Cloud Manager), che deve anche essere membro del profilo di prodotto Utenti AEM o Amministratori AEM su AEM Author, deve prima accedere a Console sviluppatori e fare clic su **Crea nuovo account tecnico** affinché le credenziali possano essere generate e successivamente recuperate da un utente con autorizzazioni di amministratore per l’ambiente AEM as a Cloud Service. Se l’amministratore dell’organizzazione IMS non lo ha fatto, viene visualizzato un messaggio per informare che è necessario il ruolo di amministratore dell’organizzazione IMS.

### Installare le credenziali del servizio AEM in un server non AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

L’applicazione che effettua chiamate all’AEM dovrebbe poter accedere alle credenziali as a Cloud Service dell’AEM, trattandole come un segreto.

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

Il token di accesso definisce il momento della scadenza, che in genere è di 24 ore. Nell’archivio Git è presente un codice di esempio per gestire un token di accesso e aggiornarlo prima della scadenza.

>[!NOTE]
>Se sono presenti più credenziali, assicurati di fare riferimento al file json appropriato per la chiamata API all’AEM che verrà successivamente richiamata.

### Chiamata dell&#39;API AEM {#calling-the-aem-api}

Effettua le chiamate API server-to-server appropriate a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Authorization&quot;, utilizza il valore `"Bearer <access_token>"`. Ad esempio, utilizzando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Impostare le autorizzazioni appropriate per l’utente dell’account tecnico in AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Innanzitutto, è necessario creare un nuovo profilo di prodotto in Adobe Admin Console. Per farlo, segui questi passaggi:

1. Vai a Adobe Admin Console all’indirizzo [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. Premere il tasto **Gestisci** collegamento sotto **Prodotti e servizi** a sinistra.
1. Seleziona **AEM as a Cloud Service**
1. Premere il tasto **Nuovo profilo** pulsante

   ![Nuovo profilo](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Denomina il profilo e premi **Salva**

   ![Salva profilo](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Seleziona il profilo appena creato dall’elenco dei profili
1. Premere il tasto **Aggiungi utente** pulsante

   ![Aggiungi utente](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Aggiungi l’account tecnico appena creato (in questo caso `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) e premere **Salva**

   ![Aggiungi account tecnico](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Attendi 10 minuti per rendere effettive le modifiche ed effettua una chiamata API all’AEM con un token di accesso generato dalle nuove credenziali. Come comando cURL, verrebbe rappresentato in modo simile a questo esempio:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Dopo aver effettuato la chiamata API, il profilo di prodotto verrà visualizzato come gruppo di utenti nell’istanza di authoring as a Cloud Service dell’AEM, con l’account tecnico appropriato come membro di tale gruppo.

Per eseguire questa operazione, è necessario:

1. Accedi all’istanza di authoring
1. Vai a **Strumenti** - **Sicurezza** e fai clic su **Gruppi** scheda
1. Individua il nome del profilo creato nell’elenco dei gruppi e fai clic su di esso:

   ![Profilo gruppo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. Nella finestra seguente, passa a **Membri** e verificare se l’account tecnico è elencato correttamente:

   ![Scheda Membri](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


In alternativa, puoi anche verificare che l’account tecnico venga visualizzato nell’elenco degli utenti eseguendo i passaggi seguenti sull’istanza di authoring:

1. Vai a **Strumenti** - **Sicurezza** - **Utenti**
1. Controlla che il tuo account tecnico sia l’elenco degli utenti e fai clic su di esso
1. Fai clic sul pulsante **Gruppi** per verificare che l’utente faccia parte del gruppo che corrisponde al tuo profilo di prodotto. Questo utente è anche membro di una manciata di altri gruppi, inclusi i collaboratori:

   ![Iscrizione al gruppo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Prima della metà del 2023, prima che fosse possibile creare più credenziali, i clienti non erano guidati a creare un profilo di prodotto nell’Admin Console di Adobe e quindi l’account tecnico non era associato a un gruppo diverso da &quot;Collaboratori&quot; nell’istanza as a Cloud Service dell’AEM. Per motivi di coerenza, si consiglia di creare un nuovo profilo di prodotto in Adobe Admin Console come descritto in precedenza e di aggiungere al gruppo l’account tecnico esistente.

<u>**Impostare le autorizzazioni del gruppo appropriato**</u>

Infine, configura il gruppo con le autorizzazioni appropriate necessarie per richiamare o bloccare le API in modo appropriato. Per farlo, segui questi passaggi:

1. Accesso all’istanza di authoring appropriata e accesso a **Impostazioni** - **Sicurezza** - **Autorizzazioni**
1. Cerca il nome del gruppo corrispondente al profilo di prodotto nel riquadro a sinistra (in questo caso API di sola lettura) e fai clic su di esso:

   ![Cerca gruppo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Fare clic sul pulsante Modifica nella finestra seguente:

   ![Autorizzazioni di modifica](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifica le autorizzazioni in modo appropriato e fai clic su **Salva**

   ![Conferma la modifica delle autorizzazioni](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Adobe Ulteriori informazioni su Identity Management System (IMS) e sugli utenti e i gruppi AEM consultando il [documentazione](/help/security/ims-support.md).

## Flusso per sviluppatori {#developer-flow}

È probabile che gli sviluppatori desiderino testare utilizzando un’istanza di sviluppo della loro applicazione non AEM (in esecuzione sul loro laptop o ospitata) che effettua richieste a un ambiente di sviluppo as a Cloud Service AEM di sviluppo. Tuttavia, poiché gli sviluppatori non dispongono necessariamente delle autorizzazioni per il ruolo di amministratore IMS, non si può presumere che possano generare il Bearer JWT descritto nel normale flusso server-to-server. Pertanto, forniamo a uno sviluppatore un meccanismo che consente di generare direttamente un token di accesso che può essere utilizzato nelle richieste agli ambienti AEM as a Cloud Service a cui ha accesso.

Consulta la [Documentazione sulle linee guida per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) per informazioni sulle autorizzazioni necessarie per utilizzare la console per sviluppatori AEM as a Cloud Service.

>[!NOTE]
>
>Il token di accesso per lo sviluppo locale è valido per un massimo di 24 ore, al termine delle quali deve essere rigenerato con lo stesso metodo.

Gli sviluppatori possono utilizzare questo token per effettuare chiamate dall’applicazione di test non AEM a un ambiente as a Cloud Service AEM. In genere, lo sviluppatore utilizza questo token con l’applicazione non AEM sul proprio laptop. Inoltre, AEM as a Cloud è in genere un ambiente non di produzione.

Il flusso per sviluppatori prevede i seguenti passaggi:

* Generare un token di accesso da Developer Console
* Chiama l’applicazione AEM con il token di accesso.

Gli sviluppatori possono anche effettuare chiamate API a un progetto AEM in esecuzione sul proprio computer locale, nel qual caso non è necessario un token di accesso.

### Generazione del token di accesso {#generating-the-access-token}

1. Vai a **Token locale** in **Integrazioni**
1. Fai clic su **Ottieni token di sviluppo locale** nella Console per sviluppatori per generare un token di accesso.

### Chiamare l’applicazione AEM con un token di accesso {#call-the-aem-application-with-an-access-token}

Effettuare le chiamate API server-to-server appropriate dall’applicazione non AEM a un ambiente as a Cloud Service AEM, incluso il token di accesso nell’intestazione. Quindi, per l’intestazione &quot;Authorization&quot;, utilizza il valore `"Bearer <access_token>"`.

## Aggiorna credenziali {#refresh-credentials}

Per impostazione predefinita, le credenziali as a Cloud Service dell&#39;AEM scadono dopo un anno. Per garantire la continuità del servizio, gli sviluppatori possono aggiornare le credenziali ed estenderne la disponibilità per un altro anno.

A questo scopo, puoi:

* Utilizza il **Aggiungi certificato** pulsante sotto **Integrazioni** - **Account tecnici** nella Console per sviluppatori, come illustrato di seguito

  ![Aggiornamento credenziali](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Dopo aver premuto il pulsante, viene generato un set di credenziali che include un nuovo certificato. Installa le nuove credenziali sul server off-AEM e assicurati che la connettività sia come previsto, senza rimuovere le vecchie credenziali 
* Assicurati di utilizzare le nuove credenziali invece di quelle precedenti durante la generazione del token di accesso
* Facoltativamente, revocare (e quindi eliminare) il certificato precedente in modo che non possa più essere utilizzato per l’autenticazione con AEM as a Cloud Service.

## Revoca credenziali {#credentials-revocation}

Se la chiave privata è compromessa, devi creare le credenziali con un nuovo certificato e una nuova chiave privata. Dopo che l&#39;applicazione utilizza le nuove credenziali per generare i token di accesso, è possibile revocare ed eliminare i vecchi certificati.

Puoi eseguire questa operazione seguendo questi passaggi:

1. Aggiungi innanzitutto la nuova chiave. Questa chiave genera le credenziali con una nuova chiave privata e un nuovo certificato. La nuova chiave privata è contrassegnata nell’interfaccia utente come **corrente** e verranno quindi utilizzate per tutte le nuove credenziali di questo account tecnico in futuro. Le credenziali associate alle chiavi private precedenti rimarranno valide fino alla revoca. Per ottenere questo risultato, premere i tre punti (**...**) con il tuo account tecnico corrente e premi **Aggiungi nuova chiave privata**:

   ![Aggiungi nuova chiave privata](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Premi **Aggiungi** al prompt seguente:

   ![Conferma aggiunta nuova chiave privata](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Viene visualizzata una nuova scheda Sfoglia con le nuove credenziali e l’interfaccia utente viene aggiornata per mostrare entrambe le chiavi private con la nuova contrassegnata come **corrente**:

   ![Chiavi private nell’interfaccia utente](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Installa le nuove credenziali sul server non AEM e assicurati che la connettività funzioni come previsto. Consulta la [Sezione Flusso da server a server](#the-server-to-server-flow) per informazioni dettagliate su come eseguire questa operazione
1. Revoca il certificato precedente. A tale scopo, seleziona i tre punti (**...**) a destra del certificato e premere **Revoca**:

   ![Revoca certificato](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Quindi, confermare la revoca nel seguente prompt premendo il tasto **Revoca** pulsante:

   ![Revoca conferma certificato](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Infine, elimina il certificato compromesso.
