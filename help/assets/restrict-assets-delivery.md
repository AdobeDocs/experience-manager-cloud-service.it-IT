---
title: Limitare la distribuzione delle risorse con Dynamic Media con funzionalità OpenAPI
description: Scopri come limitare la consegna delle risorse con le funzionalità OpenAPI.
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---

# Limitare la distribuzione delle risorse con Dynamic Media con funzionalità OpenAPI {#restrict-access-to-assets}

La governance centrale delle risorse in Experience Manager consente all’amministratore DAM o ai Brand Manager di gestire l’accesso alle risorse disponibili tramite Dynamic Media con funzionalità OpenAPI. Possono limitare la consegna di risorse approvate (fino a una singola risorsa) all&#39;[utente o ai gruppi Adobe Identity Management System (IMS) selezionati](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy) configurando alcuni metadati sulle risorse nel servizio AEM as a Cloud Service Author.

Una volta che una risorsa è limitata tramite Dynamic Media con OpenAPI, solo gli utenti (integrati in Adobe IMS) autorizzati ad accedere a tale risorsa possono accedervi. Per accedere alla risorsa, l&#39;utente deve sfruttare le funzionalità [Search](search-assets-api.md) e [Delivery](deliver-assets-apis.md) di Dynamic Media con OpenAPI.

![Accesso limitato alle risorse](/help/assets/assets/restricted-access.png)

In Experience Manager Assets, la consegna limitata tramite IMS prevede due fasi chiave:

* Authoring
* Distribuzione

## Authoring {#authoring}

### Consegna limitata tramite un token Bearer IMS {#restrict-delivery-ims-token}

È possibile limitare la consegna di risorse in [!DNL Experience Manager] in base alle identità dell&#39;utente e del gruppo IMS .

>[!NOTE]
>
> Questa funzionalità non è attualmente self-service. Per limitare la consegna delle risorse per [Utenti](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html) e [Gruppi](https://helpx.adobe.com/in/enterprise/using/user-groups.html) IMS, rivolgiti al team di supporto Enterprise per informazioni su come recuperare le informazioni necessarie per limitare l&#39;accesso dal portale [Adobe Admin Console](https://adminconsole.adobe.com/) e su come configurare l&#39;accesso nel servizio di authoring di AEM as a Cloud Service.

### Limita la consegna delle risorse utilizzando data e ora di attivazione e disattivazione {#restrict-delivery-assets-date-time}

Gli autori DAM possono inoltre limitare la consegna delle risorse definendo un orario di attivazione o disattivazione disponibile nelle proprietà delle risorse.

Se definisci un Nei tempi di attivazione di una risorsa, viene generato un URL di consegna per la risorsa al momento definito. La risorsa rimane inattiva prima dell’ora definita. Analogamente, se definisci un’ora di disattivazione per una risorsa, la risorsa viene disattivata all’ora definita e l’URL di consegna della risorsa non la visualizza più.

Esegui la procedura seguente per impostare l’ora di attivazione e disattivazione della risorsa:

1. Seleziona la risorsa e fai clic su **[!UICONTROL Proprietà]**.

1. Nella sezione **[!UICONTROL Attivazione pianificata]** della scheda **[!UICONTROL Base]**, definisci l&#39;Ora di attivazione o l&#39;Ora di disattivazione in base alle tue esigenze.

Analogamente, nella vista Assets, puoi selezionare la risorsa e fare clic su **[!UICONTROL Dettagli]** per visualizzare le proprietà della risorsa e definire l&#39;ora di attivazione e l&#39;ora di disattivazione.

Il campo è disponibile nel modulo metadati predefinito. Se la risorsa non è basata sullo schema metadati predefinito e i campi Ora di attivazione e Ora di disattivazione non sono disponibili nelle proprietà della risorsa, effettua le seguenti operazioni in visualizzazione Amministratore:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona lo schema metadati e fai clic su **[!UICONTROL Modifica]**.
1. Aggiungi un campo **[!UICONTROL Data]** dalla sezione **[!UICONTROL Genera modulo]** a destra alla sezione Metadati nel modulo.
1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel pannello **[!UICONTROL Impostazioni]**:
   1. Cambia l&#39;**[!UICONTROL Etichetta campo]** in **Ora di attivazione** o **Ora di disattivazione**.
   1. Aggiorna **[!UICONTROL Mappa sulla proprietà]** in _./jcr:content/onTime_ per il campo **On Time** e _./jcr:content/offTime_ per il campo **Off Time**.
1. Fai clic su **[!UICONTROL Salva]**.

Allo stesso modo, per la vista Assets, se la risorsa non è basata sullo schema di metadati predefinito e i campi Ora di attivazione e Ora di disattivazione non sono disponibili nelle proprietà della risorsa, esegui i seguenti passaggi:

1. Fare clic su **[!UICONTROL Forms metadati]** nella sezione **[!UICONTROL Impostazioni]**.
1. Seleziona il modulo metadati e fai clic su **[!UICONTROL Modifica]**.
1. Aggiungi al modulo un campo **[!UICONTROL Data]** dalla sezione **[!UICONTROL Componenti]** nel riquadro a sinistra.
1. Fai clic sul campo appena aggiunto e modifica **[!UICONTROL Etichetta]** in **Ora di attivazione** o **Ora di disattivazione**.
1. Aggiornare la proprietà **[!UICONTROL Metadata]** in _./jcr:content/onTime_ per il campo **On Time** e _./jcr:content/offTime_ per il campo **Off Time**.
1. Fai clic su **[!UICONTROL Salva]**.



## Consegna di risorse limitate {#delivery-restricted-assets}

La distribuzione di risorse con restrizioni si basa sull’autorizzazione ad accedere alle risorse. L&#39;autorizzazione può essere concessa tramite [token Bearer IMS](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/) (applicazione per richieste avviate da [AEM Asset Selector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)) o tramite un cookie protetto (se sono stati impostati provider di identità personalizzati nei servizi di pubblicazione/anteprima di AEM e sono state impostate la creazione e l&#39;inclusione dei cookie nelle pagine).

### Consegna per richieste di authoring o selettore risorse di AEM {#delivery-aem-author-asset-selector}

Per abilitare la consegna di risorse con restrizioni nel caso in cui la richiesta venga inviata dal servizio di authoring di AEM o dal selettore delle risorse di AEM, è essenziale un token IMS Bearer valido.\
Nei servizi di authoring di AEM Cloud Service e in Selettore risorse, il token Bearer IMS viene generato e utilizzato automaticamente per le richieste dopo un accesso riuscito.

>[!NOTE]
>
>Per ulteriori informazioni su come abilitare l’autenticazione IMS sulle integrazioni basate su AEM Asset Selector, contatta il supporto Enterprise

1. Per esperienze non basate su Asset Selector, AEM as a Cloud Service e Dynamic Media con funzionalità OpenAPI supportano attualmente integrazioni API lato server e possono generare token IMS Bearer.
   * Segui le istruzioni [qui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow) per eseguire integrazioni API da servizio a server in grado di recuperare i token Bearer IMS tramite [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)
   * Per un periodo limitato, è possibile generare token Bearer IMS di breve durata per l&#39;utente autenticato in [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) per l&#39;accesso sviluppatore locale (non destinato ai casi di utilizzo in produzione) seguendo le istruzioni [qui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)

1. Durante l&#39;esecuzione di [richieste API Search](search-assets-api.md) e [Delivery](deliver-assets-apis.md), aggiungere il token IMS Bearer ottenuto all&#39;intestazione **[!UICONTROL Authorization]** della richiesta HTTP (assicurarsi che il relativo valore sia preceduto da **[!UICONTROL Bearer]**).

1. Per convalidare la restrizione di accesso, avvia una richiesta API di consegna con e senza l&#39;intestazione **[!UICONTROL Authorization]**.
   * La risposta restituirà un codice di stato di errore `404` nei casi in cui non sia presente alcun token Bearer IMS o il token Bearer IMS fornito non appartiene all’utente a cui è stato concesso l’accesso alla risorsa (direttamente o tramite l’iscrizione al gruppo).
   * La risposta restituirà un codice di stato di successo `200` con il contenuto binario della risorsa, se il token IMS Bearer è uno degli utenti o dei gruppi a cui è stato concesso l’accesso alla risorsa.

### Consegna per i provider di identità personalizzati nel servizio di pubblicazione {#delivery-custom-identity-provider}

AEM Sites, AEM Assets e Dynamic Media con licenze OpenAPI possono essere utilizzati insieme, consentendo la distribuzione limitata delle risorse da configurare sui siti web ospitati sul servizio di pubblicazione o anteprima di AEM. Il flusso di consegna sicuro sfrutta i cookie del browser per stabilire l’accesso dell’utente e l’esistenza di un dominio personalizzato per il livello di consegna che sia un sottodominio del dominio di pubblicazione è un prerequisito per l’implementazione di questo caso d’uso. Se i servizi di pubblicazione e anteprima di AEM Sites sono configurati per l&#39;utilizzo di un [provider di identità personalizzato (IdP)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), è necessario impostare un nuovo cookie denominato `delivery-token` che incapsula l&#39;appartenenza al gruppo dell&#39;utente durante l&#39;autenticazione dell&#39;utente del post di dominio di pubblicazione. Il livello di consegna estrae il materiale di autorizzazione dal cookie protetto e convalida l’accesso. Registra un [ticket di supporto Enterprise](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities) per ulteriori dettagli.
