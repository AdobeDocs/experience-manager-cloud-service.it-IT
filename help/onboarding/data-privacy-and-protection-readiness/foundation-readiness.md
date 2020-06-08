---
title: Regole sulla protezione dei dati e sulla privacy dei dati - Adobe Experience Manager come servizio cloud
description: 'Scopri Adobe Experience Manager come supporto di Cloud Service Foundation per le varie normative sulla protezione dei dati e la privacy dei dati; incluso il Regolamento generale sulla protezione dei dati (GDPR) dell''UE, il California Consumer Privacy Act e le modalità per conformarsi all''implementazione di un nuovo AEM come progetto di servizio cloud. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---


# Adobe Experience Manager come servizio cloud per la protezione dei dati e le normative sulla privacy {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto del presente documento non costituisce consulenza giuridica e non è inteso come sostituto della consulenza legale.
>
>Consulta l&#39;ufficio legale della tua azienda per consigli in merito alle normative sulla protezione dei dati e sulla privacy dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta di Adobe ai problemi di privacy e sul significato che questo comporta per voi in quanto clienti Adobe, consultate il Centro [per la privacy di](https://www.adobe.com/privacy.html)Adobe.

## Supporto per la privacy e la protezione dei dati di AEM Foundation {#aem-foundation-data-privacy-and-protection-support}

A livello di AEM Foundation, i Dati personali memorizzati sono memorizzati nel profilo utente. Pertanto, le informazioni contenute in questo articolo riguardano principalmente come accedere ai profili utente ed eliminarli, rispettivamente per soddisfare le richieste di accesso ed eliminazione.

## Accesso a un profilo utente {#accessing-a-user-profile}

### Passaggi manuali {#manual-steps}

1. Aprite la console Amministrazione utente, accedendo a **[!UICONTROL Strumenti - Protezione - Utenti]** o sfogliando direttamente il pulsante `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. Quindi, cercate l’utente in questione digitando il nome nella barra di ricerca nella parte superiore della pagina:

   ![ricerca account](assets/dpp-foundation-01.png)

1. Infine, aprite il profilo utente facendo clic su di esso, quindi selezionate nella scheda **[!UICONTROL Dettagli]** .

   ![profilo utente](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

Come già detto, Adobe fornisce API per l&#39;accesso ai dati utente, al fine di facilitare l&#39;automazione. Esistono diversi tipi di API che potete utilizzare:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

**Individuazione della home page dell&#39;utente:**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Recupero dei dati utente:**

Utilizzando il percorso del nodo dalla proprietà home del payload JSON restituito dal comando precedente:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Disattivazione di un utente ed eliminazione dei profili associati {#disabling-a-user-and-deleting-the-associated-profiles}

### Disattiva utente {#disable-user}

1. Aprite la console Amministrazione utente ed effettuate la ricerca dell’utente in questione, come descritto sopra.
2. Passate il puntatore del mouse sull’utente e fate clic sull’icona di selezione. Il profilo diventa grigio e indica che è selezionato.

3. Premere il pulsante **Disattiva** nel menu superiore per disattivare l&#39;utente:

   ![disable account](assets/dpp-foundation-03.png)

4. Infine, confermate l&#39;azione.

   L&#39;interfaccia utente indica quindi che l&#39;account utente è stato disattivato disattivando la visualizzazione in grigio e aggiungendo un blocco alla scheda del profilo:

   ![account disattivato](assets/dpp-foundation-04.png)

### Elimina informazioni profilo utente {#delete-user-profile-information}

>[!NOTE]
>
> Per AEM come servizio cloud non è disponibile alcuna procedura manuale dall’interfaccia utente per l’eliminazione di un profilo utente, in quanto CRXDE non è accessibile.

### HTTP API {#http-api-1}

Le procedure seguenti utilizzano lo `curl`strumento della riga di comando per illustrare come disabilitare l’utente con **[!UICONTROL cavery]** `userId` ed eliminare i profili disponibili nel percorso predefinito.

**Individuazione della home page dell&#39;utente:**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Disattivazione dell’utente:**

Utilizzando il percorso del nodo dalla proprietà home del payload JSON restituito dal comando precedente:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**Eliminazione dei profili utente**

Utilizzando il percorso del nodo dalla proprietà home del payload JSON restituito dal comando di individuazione dell&#39;account e dalle posizioni note del nodo del profilo casella:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
