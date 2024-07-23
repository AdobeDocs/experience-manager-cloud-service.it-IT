---
title: Limitare la consegna di risorse in Experience Manager
description: Scopri come limitare la consegna delle risorse in [!DNL Experience Manager].
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 16b313a4fb79f915613044d12d29e618209113ec
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Limita l&#39;accesso alle risorse in [!DNL Experience Manager] {#restrict-access-to-assets}

La governance centrale delle risorse in Experience Manager consente all’amministratore DAM o ai Brand Manager di gestire l’accesso alle risorse. Possono limitare l’accesso configurando i ruoli per le risorse approvate sul lato authoring, in particolare sull’istanza di authoring di AEM as a Cloud Service.

Gli utenti che [cercano](search-assets-api.md) o utilizzano [gli URL di consegna](deliver-assets-apis.md) possono accedere alle risorse con restrizioni dopo aver completato correttamente il processo di autorizzazione.

![Accesso limitato alle risorse](/help/assets/assets/restricted-access.png)

## Consegna limitata tramite un token IMS {#restrict-delivery-ims-token}

In Experience Manager Assets, la consegna limitata tramite IMS prevede due fasi chiave:

* Authoring
* Distribuzione

### Authoring {#authoring}

È possibile limitare la consegna di risorse all&#39;interno di [!DNL Experience Manager] in base ai ruoli. Per configurare i ruoli, esegui i seguenti passaggi:

1. Vai a [!DNL Experience Manager] come amministratore DAM.
1. Seleziona la risorsa per la quale devi configurare il ruolo.
1. Passa a **[!UICONTROL Proprietà]** > **[!UICONTROL Avanzate]** e assicurati che il campo **[!UICONTROL Ruoli]** esista nella scheda [!UICONTROL Metadati avanzati].

   ![Metadati ruoli](/help/assets/assets/roles_metadata.jpg)
Se il campo non è disponibile, procedi come segue per aggiungerlo:

   1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
   1. Selezionare lo schema metadati e fare clic su **[!UICONTROL Modifica _(e)_]**.
   1. Aggiungi un campo **[!UICONTROL Testo con più valori]** dalla sezione **[!UICONTROL Genera modulo]** a destra alla sezione Metadati nel modulo.
   1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel pannello **[!UICONTROL Impostazioni]**:
      1. Cambia l&#39;etichetta **[!UICONTROL Campo]** in _Ruoli_.
      1. Aggiorna **[!UICONTROL Mappa sulla proprietà]** in _./jcr:content/metadata/dam:roles_.

1. Ottieni i gruppi IMS da aggiungere nei metadati dei ruoli della risorsa. Per recuperare i gruppi IMS, effettua le seguenti operazioni:
   1. Accedi a `https://adminconsole.adobe.com/.`
   1. Vai alla tua rispettiva organizzazione e passa a **[!UICONTROL Gruppi di utenti]**.
   1. Seleziona il **[!UICONTROL gruppo utenti]** da aggiungere ed estrai **[!UICONTROL orgID]** e **[!UICONTROL userGroupID]** dall&#39;URL oppure utilizza l&#39;ID organizzazione, ad esempio `{orgID}@AdobeOrg:{usergroupID}`.

1. Aggiungi l&#39;ID gruppo al campo **[!UICONTROL Ruoli]** delle proprietà della risorsa. <br>
Gli ID gruppo definiti nel campo **[!UICONTROL Ruoli]** sono gli unici utenti che possono accedere alla risorsa. Puoi anche aggiungere l&#39;ID client IMS e l&#39;ID profilo IMS nel campo **[!UICONTROL Ruoli]**. Esempio: `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >Per la nuova visualizzazione Assets, puoi concedere l’accesso solo fino al livello della cartella e esclusivamente ai gruppi anziché ai singoli utenti. Ulteriori informazioni sulla [gestione delle autorizzazioni in Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Limita la consegna delle risorse utilizzando data e ora di attivazione e disattivazione {#restrict-delivery-assets-date-time}

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



### Consegna di risorse limitate {#delivery-restricted-assets}

La distribuzione di risorse con restrizioni si basa sull’autorizzazione ad accedere alle risorse. L’autorizzazione si basa su un token IMS se la richiesta viene inviata da un’istanza di authoring AEM o da Asset Selector oppure su un cookie speciale se hai dei provider di identità personalizzati impostati nell’istanza di Publish o Anteprima.

#### Consegna per richieste di authoring AEM o Selettore risorse {#delivery-aem-author-asset-selector}

Per abilitare la consegna di risorse con restrizioni nel caso in cui la richiesta venga inviata dall’istanza di authoring AEM o dal selettore di risorse, è essenziale un token IMS valido. Segui questi passaggi:

1. [Generare un token di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Accedi alla Console per sviluppatori del tuo ambiente AEM as a Cloud Service.

   * Passa a **[!UICONTROL Ambiente]** > **[!UICONTROL Integrazioni]** > **[!UICONTROL Token locale]** > **[!UICONTROL Ottieni token di sviluppo locale]** > **[!UICONTROL Copia valore accessToken]**. Ulteriori informazioni su [come accedere al token e agli aspetti correlati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integra il token di accesso ottenuto nell&#39;intestazione **[!UICONTROL Authorization]**, assicurandoti che il relativo valore abbia il prefisso **[!UICONTROL Bearer]**.

1. Convalida la funzionalità del token di accesso avviando una richiesta. Dovrebbe generare un errore 404 nei casi in cui non sia presente alcun token di accesso IMS o il token di accesso fornito non presenti gli stessi utenti/gruppi/ruoli aggiunti nei metadati della risorsa.

#### Consegna per i provider di identità personalizzati nell’istanza Publish {#delivery-custom-identity-provider}

Nel caso di un provider di identità personalizzato configurato nell&#39;istanza di Publish o Anteprima, è possibile indicare il gruppo che deve avere accesso alle risorse protette nell&#39;attributo `groupMembership` durante il processo di configurazione. Quando si accede al provider di identità personalizzato tramite l&#39;[integrazione SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), l&#39;attributo `groupMembership` viene letto e utilizzato per creare un cookie, che viene inviato in tutte le richieste di autenticazione, simile a un token IMS in caso di richiesta dell&#39;autore AEM o del selettore di risorse.

Quando una risorsa protetta è disponibile in una pagina e viene effettuata una richiesta all’URL di consegna per eseguire il rendering della risorsa, AEM controlla i ruoli presenti nel cookie o nel token IMS e li confronta con `dam:roles property` applicati durante la creazione della risorsa. Se viene trovata una corrispondenza, la risorsa viene visualizzata.

>[!NOTE]
>
> Nel [ticket di supporto per attivare Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), indica la consegna con restrizioni nel caso di utilizzo. Il team ingegneristico Adobe fornirà i chiarimenti necessari e/o definirà la procedura per la consegna limitata.
