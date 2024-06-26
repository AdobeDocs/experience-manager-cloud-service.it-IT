---
title: Limitare la consegna di risorse in Experience Manager
description: Scopri come limitare la consegna delle risorse in [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Limitare l’accesso alle risorse in [!DNL Experience Manager] {#restrict-access-to-assets}

La governance centrale delle risorse in Experience Manager consente all’amministratore DAM o ai Brand Manager di gestire l’accesso alle risorse. Possono limitare l’accesso configurando i ruoli per le risorse approvate sul lato authoring, in particolare sull’istanza di authoring di AEM as a Cloud Service.

Utenti [ricerca](search-assets-api.md) o utilizzando [URL di consegna](deliver-assets-apis.md) può accedere alle risorse con restrizioni una volta superato il processo di autorizzazione.

![Accesso limitato alle risorse](/help/assets/assets/restricted-access.png)

## Consegna limitata tramite un token IMS {#restrict-delivery-ims-token}

Ad Experience Manager, la consegna limitata tramite IMS prevede due fasi chiave:

* Authoring
* Distribuzione

### Authoring {#authoring}

Puoi limitare la consegna delle risorse in [!DNL Experience Manager] in base ai ruoli. Per configurare i ruoli, esegui i seguenti passaggi:

1. Vai a [!DNL Experience Manager] come amministratore DAM.
1. Seleziona la risorsa per la quale devi configurare il ruolo.
1. Accedi a **[!UICONTROL Proprietà]** > **[!UICONTROL Avanzate]** e garantire che **[!UICONTROL Ruoli]** il campo esiste in [!UICONTROL Metadati avanzati] scheda.

   ![Metadati dei ruoli](/help/assets/assets/roles_metadata.jpg)
Se il campo non è disponibile, procedi come segue per aggiungerlo:

   1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
   1. Seleziona lo schema metadati e fai clic su **[!UICONTROL Modifica _e)_]**.
   1. Aggiungi un **[!UICONTROL Testo con più valori]** campo da **[!UICONTROL Genera modulo]** sezione a destra della sezione Metadati nel modulo.
   1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel  **[!UICONTROL Impostazioni]** pannello:
      1. Modificare il **[!UICONTROL Etichetta campo]** a _Ruoli_.
      1. Aggiornare il **[!UICONTROL Mappa su proprietà]** a _./jcr:content/metadata/dam:roles_.

1. Ottieni i gruppi IMS da aggiungere nei metadati dei ruoli della risorsa. Per recuperare i gruppi IMS, effettua le seguenti operazioni:
   1. Accedi a https://adminconsole.adobe.com/.
   1. Vai alla tua rispettiva organizzazione e passa a **[!UICONTROL Gruppi di utenti]**.
   1. Seleziona la **[!UICONTROL Gruppo utenti]** è necessario aggiungere ed estrarre **[!UICONTROL orgID]** e **[!UICONTROL userGroupID]** dall’URL o utilizza il tuo ID organizzazione, ad esempio `{orgID}@AdobeOrg:{usergroupID}`.

1. Aggiungi l&#39;ID gruppo al **[!UICONTROL Ruoli]** campo delle proprietà della risorsa. <br>
Gli ID gruppo definiti nella sezione **[!UICONTROL Ruoli]** sono gli unici utenti che possono accedere alla risorsa. Puoi anche aggiungere l’ID client IMS e l’ID profilo IMS nella sezione **[!UICONTROL Ruoli]** campo. Esempio: `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >Per la nuova visualizzazione Assets, puoi concedere l’accesso solo fino al livello della cartella e esclusivamente ai gruppi anziché ai singoli utenti. Ulteriori informazioni su [gestione delle autorizzazioni in Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Limita la consegna delle risorse utilizzando data e ora di attivazione e disattivazione {#restrict-delivery-assets-date-time}

Gli autori DAM possono inoltre limitare la consegna delle risorse definendo un orario di attivazione o disattivazione disponibile nelle proprietà delle risorse.

Se definisci un Nei tempi di attivazione di una risorsa, viene generato un URL di consegna per la risorsa al momento definito. La risorsa rimane inattiva prima dell’ora definita. Analogamente, se definisci un’ora di disattivazione per una risorsa, la risorsa viene disattivata all’ora definita e l’URL di consegna della risorsa non la visualizza più.

Esegui la procedura seguente per impostare l’ora di attivazione e disattivazione della risorsa:

1. Seleziona la risorsa e fai clic su **[!UICONTROL Proprietà]**.

1. In **[!UICONTROL Attivazione pianificata (de)]** sezione del **[!UICONTROL Base]** , definire l&#39;Ora di attivazione o l&#39;Ora di disattivazione in base alle proprie esigenze.

Allo stesso modo, nella vista Assets, puoi selezionare la risorsa e fare clic su **[!UICONTROL Dettagli]** per visualizzare le proprietà della risorsa e definire le ore di attivazione e di disattivazione.

Il campo è disponibile nel modulo metadati predefinito. Se la risorsa non è basata sullo schema metadati predefinito e i campi Ora di attivazione e Ora di disattivazione non sono disponibili nelle proprietà della risorsa, effettua le seguenti operazioni in visualizzazione Amministratore:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona lo schema metadati e fai clic su **[!UICONTROL Modifica]**.
1. Aggiungi un **[!UICONTROL Data]** campo da **[!UICONTROL Genera modulo]** sezione a destra della sezione Metadati nel modulo.
1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel  **[!UICONTROL Impostazioni]** pannello:
   1. Modificare il **[!UICONTROL Etichetta campo]** a **Ora di attivazione** o **Ora di disattivazione**.
   1. Aggiornare il **[!UICONTROL Mappa su proprietà]** a _./jcr:content/onTime_ per **Ora di attivazione** campo e _./jcr:content/offTime_ per **Ora di disattivazione** campo.
1. Fai clic su **[!UICONTROL Salva]**.

Allo stesso modo, per la vista Assets, se la risorsa non è basata sullo schema di metadati predefinito e i campi Ora di attivazione e Ora di disattivazione non sono disponibili nelle proprietà della risorsa, esegui i seguenti passaggi:

1. Clic **[!UICONTROL Forms metadati]** nel **[!UICONTROL Impostazioni]** sezione.
1. Seleziona il modulo metadati e fai clic su **[!UICONTROL Modifica]**.
1. Aggiungi un **[!UICONTROL Data]** campo da **[!UICONTROL Componenti]** nel riquadro sinistro al modulo.
1. Fai clic sul campo appena aggiunto e modifica il **[!UICONTROL Etichetta]** a **Ora di attivazione** o **Ora di disattivazione**.
1. Aggiornare il **[!UICONTROL Proprietà metadati]** a _./jcr:content/onTime_ per **Ora di attivazione** campo e _./jcr:content/offTime_ per **Ora di disattivazione** campo.
1. Fai clic su **[!UICONTROL Salva]**.



### Consegna di risorse limitate {#delivery-restricted-assets}

La distribuzione di risorse con restrizioni si basa sull’autorizzazione ad accedere alle risorse. L’autorizzazione si basa su un token IMS se la richiesta viene inviata da un’istanza di authoring AEM o da Asset Selector oppure su un cookie speciale se hai dei provider di identità personalizzati impostati nell’istanza di Publish o Anteprima.

#### Consegna per richieste di authoring AEM o Selettore risorse {#delivery-aem-author-asset-selector}

Per abilitare la consegna di risorse con restrizioni nel caso in cui la richiesta venga inviata dall’istanza di authoring AEM o dal selettore di risorse, è essenziale un token IMS valido. Segui questi passaggi:

1. [Generare un token di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Accedi alla Console per sviluppatori del tuo ambiente AEM as a Cloud Service.

   * Accedi a **[!UICONTROL Ambiente]** > **[!UICONTROL Integrazioni]** > **[!UICONTROL Token locale]** > **[!UICONTROL Ottieni token di sviluppo locale]** > **[!UICONTROL Copia valore accessToken]**. Ulteriori informazioni su [come accedere al token e agli aspetti correlati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integra il token di accesso ottenuto in **[!UICONTROL Autorizzazione]** , verificando che il relativo valore sia preceduto da **[!UICONTROL Bearer]**.

1. Convalida la funzionalità del token di accesso avviando una richiesta. Dovrebbe generare un errore 404 nei casi in cui non sia presente alcun token di accesso IMS o il token di accesso fornito non presenti gli stessi utenti/gruppi/ruoli aggiunti nei metadati della risorsa.

#### Consegna per i provider di identità personalizzati nell’istanza Publish {#delivery-custom-identity-provider}

Nel caso di un provider di identità personalizzato configurato nell’istanza Publish o Anteprima, puoi indicare il gruppo che deve avere accesso alle risorse protette in `groupMembership` durante il processo di impostazione. Quando accedi al provider di identità personalizzato tramite [Integrazione SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), il `groupMembership` L’attributo viene letto e utilizzato per creare un cookie, che viene inviato in tutte le richieste di autenticazione, simile a un token IMS in caso di richiesta da parte dell’autore AEM o del selettore di risorse.

Quando una risorsa protetta è disponibile in una pagina e viene effettuata una richiesta all’URL di consegna per eseguire il rendering della risorsa, AEM controlla i ruoli presenti nel cookie o nel token IMS e li confronta con il `dam:roles property` applicate durante la creazione della risorsa. Se viene trovata una corrispondenza, la risorsa viene visualizzata.

>[!NOTE]
>
> In [ticket di supporto per attivare Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), nel caso di utilizzo, indica consegna limitata. Il team ingegneristico Adobe fornirà i chiarimenti necessari e/o definirà la procedura per la consegna limitata.
