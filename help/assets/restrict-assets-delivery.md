---
title: Limitare la consegna di risorse in Experience Manager
description: Scopri come limitare la consegna delle risorse in [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Limitare l’accesso alle risorse in [!DNL Experience Manager] {#restrict-access-to-assets}

La governance centrale delle risorse in Experience Manager consente all’amministratore DAM o ai Brand Manager di gestire l’accesso alle risorse. Possono limitare l’accesso configurando i ruoli per le risorse approvate sul lato authoring, in particolare sull’istanza di authoring as a Cloud Service dell’AEM.

Utenti [ricerca](search-assets-api.md) o utilizzando [URL di consegna](deliver-assets-apis.md) può accedere alle risorse con restrizioni una volta superato il processo di autorizzazione.

![Accesso limitato alle risorse](/help/assets/assets/restricted-access.png)

## Consegna limitata tramite un token IMS {#restrict-delivery-ims-token}

Ad Experience Manager, la consegna limitata tramite IMS prevede due fasi chiave:

* Authoring
* Distribuzione

### Authoring {#authoring}

Per limitare la distribuzione delle risorse, è necessario configurare i ruoli per le risorse all’interno di [!DNL Experience Manager] o [!DNL Experience Manager Assets]. Per configurare i ruoli in [!DNL Experience Manager], effettua le seguenti operazioni:

1. Vai a [!DNL Experience Manager] come amministratore DAM.
1. Seleziona la risorsa per la quale devi configurare il ruolo.
1. Accedi a **[!UICONTROL Proprietà]** > **[!UICONTROL Avanzate]** e garantire che **[!UICONTROL Ruoli]** il campo esiste in [!UICONTROL Metadati avanzati] scheda.

   ![Metadati dei ruoli](/help/assets/assets/roles_metadata.jpg)
Se il campo non è disponibile, procedi come segue per aggiungerlo:

   1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.
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
   >Per la nuova visualizzazione Risorse, puoi concedere l’accesso solo fino al livello della cartella e esclusivamente ai gruppi anziché ai singoli utenti. Ulteriori informazioni su [gestione delle autorizzazioni in Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

### Consegna di risorse limitate {#delivery-restricted-assets}

La distribuzione di risorse con restrizioni si basa sull’autorizzazione ad accedere alle risorse. L’autorizzazione si basa su un token IMS se la richiesta viene inviata da un’istanza di authoring AEM o da Asset Selector oppure su un cookie speciale se nell’istanza di pubblicazione o anteprima sono impostati provider di identità personalizzati.

#### Consegna per l’autore AEM o il selettore risorse {#delivery-aem-author-asset-selector}

Per abilitare la consegna di risorse con restrizioni nel caso in cui la richiesta venga inviata dall’istanza di authoring AEM o dal selettore di risorse, è essenziale un token IMS valido. Segui questi passaggi:

1. [Generare un token di accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Accedi alla Console per sviluppatori dell’ambiente as a Cloud Service AEM.

   * Accedi a **[!UICONTROL Ambiente]** > **[!UICONTROL Integrazioni]** > **[!UICONTROL Token locale]** > **[!UICONTROL Ottieni token di sviluppo locale]** > **[!UICONTROL Copia valore accessToken]**. Ulteriori informazioni su [come accedere al token e agli aspetti correlati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integra il token di accesso ottenuto in **[!UICONTROL Autorizzazione]** , verificando che il relativo valore sia preceduto da **[!UICONTROL Bearer]**.

1. Convalida la funzionalità del token di accesso avviando una richiesta. Dovrebbe generare un errore 404 nei casi in cui non sia presente alcun token di accesso IMS o il token di accesso fornito non presenti gli stessi utenti/gruppi/ruoli aggiunti nei metadati della risorsa.

#### Consegna per provider di identità personalizzati {#delivery-custom-identity-provider}

Se nell’istanza di pubblicazione o anteprima è configurato un provider di identità personalizzato, puoi indicare il gruppo che deve avere accesso alle risorse protette in `groupMembership` durante il processo di impostazione. Quando accedi al provider di identità personalizzato tramite [Integrazione SAML](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), il `groupMembership` L’attributo viene letto e utilizzato per creare un cookie, che viene inviato in tutte le richieste di autenticazione, simile a un token IMS in caso di richiesta da parte dell’autore AEM o del selettore di risorse.

Quando una risorsa protetta è disponibile in una pagina e viene effettuata una richiesta all’URL di consegna per eseguire il rendering della risorsa, AEM controlla i ruoli presenti nel cookie o nel token IMS e li confronta con il `dam:roles property` applicate durante la creazione della risorsa. Se viene trovata una corrispondenza, la risorsa viene visualizzata.
