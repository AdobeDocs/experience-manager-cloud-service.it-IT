---
title: Come salvare il modulo adattivo basato sui componenti core come bozza e utilizzare il componente Bozze e invii per elencare bozze e invii?
description: Scopri come salvare come bozza un modulo adattivo basato su componenti core. Scopri anche come utilizzare il componente Bozze e invii per elencare le bozze e gli invii per gli utenti connessi?
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 72e8223c91e5722e27ebd6853b8b75a7415f3e4d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---


# Salvare ed elencare i moduli come bozze nella pagina Sites

Si consideri un utente che inizia a compilare un modulo ma deve sospendere e tornare in un secondo momento. L&#39;AEM offre un&#39;opzione `save-as-draft` che consente all&#39;utente di salvare il modulo come bozza per il completamento futuro. Per facilitare questa fase, AEM fornisce il componente **Bozze e invii** Portale dei moduli pronto all&#39;uso, che visualizza le bozze e gli invii sulle pagine AEM Sites. Il componente elenca i moduli salvati come bozze da completare in un secondo momento, nonché quelli inviati. Solo gli utenti connessi possono modificare le bozze o visualizzare i moduli inviati. Tuttavia, se un utente anonimo passa all&#39;elenco dei moduli utilizzando il componente **Ricerca e elenco** e salva un modulo come bozza, tale bozza non viene elencata dal componente **Bozze e invii**. Per visualizzare le bozze e gli invii, è necessario che gli utenti abbiano effettuato l&#39;accesso al momento dell&#39;invio del modulo.

![Icona Bozze](assets/drafts-component.png){width="250" align="center"}

## Prerequisiti

* [Abilita i componenti core Forms adattivi per il tuo ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

  Dopo aver distribuito i Componenti core più recenti nell’ambiente, i componenti del portale Forms diventano accessibili nell’ambiente di authoring.

* [Configura il connettore di archiviazione e archiviazione unificata di Azure per il componente Forms Portal per bozze e invii](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### Configurare il connettore di archiviazione e archiviazione unificata di Azure per il componente Forms Portal per bozze e invii

Il componente **Bozze e invii** richiede una configurazione dell&#39;archiviazione per il salvataggio e l&#39;elenco delle bozze sulla pagina AEM Sites. Il connettore di archiviazione unificata offre un framework per collegare l’AEM allo storage esterno. Per salvare il modulo come bozza, verificare di disporre di un account di archiviazione Azure e di una chiave di accesso per autorizzare l&#39;accesso all&#39;account di archiviazione [!DNL Azure]. Una volta che disponi dell’account di archiviazione Azure e della chiave di accesso, effettua le seguenti operazioni per creare una configurazione di archiviazione Azure:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.

   ![Selezione scheda di archiviazione Azure](/help/forms/assets/save-form-as-draft-azure-card.png){width="250" align="center"}

1. Selezionare una cartella di configurazione per creare la configurazione e selezionare **[!UICONTROL Crea]**.

   ![Seleziona cartella di configurazione archiviazione di Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png){width="250" align="center"}

1. Specifica un titolo per la configurazione nel campo **[!UICONTROL Titolo]**.
1. Specificare il nome dell&#39;account di archiviazione [!DNL Azure] nei campi **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]**.

   ![Configurazione archiviazione Azure](/help/forms/assets/save-form-as-draft-azure-storage.png){width="250" align="center"}

1. Fai clic su **Salva**.

   >[!NOTE]
   >
   > È possibile recuperare l&#39;**[!UICONTROL account di archiviazione Azure]** e la **[!UICONTROL chiave di accesso Azure]** dal [portale Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

   Dopo aver creato la configurazione di archiviazione di Azure, configurare il connettore di archiviazione unificata per Forms Portal, attenendosi alla procedura seguente:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.

   ![Archiviazione connettore unificato](/help/forms/assets/save-form-as-draft-unified-connector.png){width="250" align="center"}

1. Nella sezione **[!UICONTROL Forms Portal]**, selezionare **[!UICONTROL Azure]** dall&#39;elenco a discesa **[!UICONTROL Archiviazione]**.
1. Specificare il percorso di configurazione per la configurazione di archiviazione Azure nel campo **[!UICONTROL Percorso configurazione di archiviazione]**.

   ![Impostazione archiviazione connettore unificato](/help/forms/assets/save-form-as-draft-unified-connector-storage.png){width="250" align="center"}

1. Seleziona **[!UICONTROL Salva]**.

>[!NOTE]
>
> Se devi configurare un’opzione di archiviazione, diversa da Azure, scrivi a aem-forms-ea@adobe.com dal tuo indirizzo e-mail ufficiale con i requisiti dettagliati.

Dopo aver configurato correttamente il connettore di archiviazione e archiviazione unificata di Azure per l&#39;archiviazione delle bozze e dei moduli inviati, aggiungere il componente **Bozze e invii** nella pagina di AEM Sites.

## Come aggiungere il componente Bozze e invii a una pagina di AEM Sites?

È possibile utilizzare i componenti predefiniti di Forms Portal per elencare le bozze e gli invii nella pagina Sites. Per aggiungere il componente del portale **Bozze e invii**, effettua le seguenti operazioni:

1. Apri la pagina AEM Sites in modalità **Modifica**.
1. Vai a **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Modifica modello]**
   ![Modifica criterio modello](/help/forms/assets/save-form-as-draft-edit-template.png){width="250" align="center"}

1. Fai clic sul **[!UICONTROL Criterio]** e seleziona la casella di controllo **[!UICONTROL Bozze e invii]** in **[Nome progetto archetipo AEM] - Forms and Communications Portal**.

   ![Selezione criteri](/help/forms/assets/save-form-as-draft-enable-policy.png){width="250" align="center"}

1. Fai clic su **[!UICONTROL Fine]**.
1. Ora riapri la pagina AEM Sites in modalità di authoring.
1. Nell’editor pagina, individua la sezione che consente di aggiungere il componente Forms Portal.
1. Fai clic sull&#39;icona **Aggiungi**. L’icona è un segno più (+) che indica l’opzione per aggiungere nuovi componenti.

   Facendo clic sull&#39;icona **Aggiungi** viene visualizzata una finestra di dialogo **Inserisci nuovo componente** in cui sono visualizzati vari componenti da inserire.

   >[!NOTE]
   >
   > In alternativa, puoi anche trascinare e rilasciare il componente.

1. Sfoglia i componenti disponibili nella finestra di dialogo e seleziona il componente desiderato dall’elenco. Selezionare ad esempio il componente **Bozze e invii** dall&#39;elenco per aggiungere il componente **Bozze e invii** di Forms Portal.

   ![Aggiungi bozza e componente invio](/help/forms/assets/save-form-as-draft-add-dns.png){width="250" align="center"}

Ora configura le proprietà del componente **Bozze e invii** in base ai requisiti.

## Configurare le proprietà del componente Bozze e invii

Puoi configurare le proprietà di **Bozze e invii**:
1. Seleziona il componente **Bozze e invii**.
1. Fare clic sull&#39;icona ![Configura](assets/configure_icon.png) per visualizzare la finestra di dialogo.
1. Nella finestra di dialogo **[!UICONTROL Bozze e invii]**, specifica quanto segue:
   * **Titolo** Per identificare un componente in una pagina Sites e per impostazione predefinita, il titolo viene visualizzato sopra il componente.
   * **Seleziona tipo**: per indicare il modulo come bozza o inviato. Se si sceglie **Bozza di Forms**, verranno visualizzati i moduli salvati come bozze. In alternativa, selezionando **Forms inviato** vengono visualizzati i moduli inviati dagli utenti connessi.
   * **Layout**: per visualizzare le bozze degli elenchi o i moduli inviati in formato scheda o elenco.

   ![Proprietà dei componenti Bozza e Invio](/help/forms/assets/save-form-as-draft-dns-properties.png){width="250" align="center"}

## Configurare i moduli da salvare come bozze

È possibile configurare Forms adattivo nei due modi seguenti per salvarlo come bozza da utilizzare in un secondo momento:
* [Azione utente](#user-action)
* [Salvataggio automatico](#auto-save)

### Azione utente

>[!NOTE]
>
> Assicurati che la versione dei [Componenti core sia impostata su 3.0.24 o successiva](https://github.com/adobe/aem-core-forms-components) per salvare i moduli come bozze utilizzando la regola **Salva modulo**.

Per salvare un modulo come bozza, creare una regola **Salva modulo** in un componente modulo, ad esempio un pulsante. Quando si fa clic sul pulsante, la regola viene attivata e il modulo viene salvato come bozza. Per creare una regola **Salva modulo** in un componente pulsante, effettua le seguenti operazioni:

1. Aprire un modulo adattivo in modalità di modifica.
1. Seleziona l&#39;icona **[!UICONTROL Modifica regole]** per aprire l&#39;editor di regole per il componente **Button**.
1. Seleziona **[!UICONTROL Crea]** per configurare e creare la regola per il pulsante.
1. Nella sezione **[!UICONTROL When]**, seleziona **is clicked** e nella sezione **[!UICONTROL Then]** seleziona l&#39;opzione **Save Form**.
1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

   ![Crea regola per il pulsante](/help/forms/assets/save-form-as-drfat-create-rule.png){width="250" align="center"}

Quando visualizzi l&#39;anteprima di un modulo adattivo, lo compili e fai clic sul pulsante **Salva modulo**, il modulo viene salvato come bozza.

### Salvataggio automatico

<span class="preview"> Questo articolo contiene informazioni sulla funzionalità **Salvataggio automatico**, una funzionalità non definitiva. La funzione pre-release è accessibile solo tramite il [canale pre-release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features).</span>

>[!NOTE]
>
> Assicurati che la versione dei [Componenti core sia impostata su 3.0.52 o successiva](https://github.com/adobe/aem-core-forms-components) per salvare i moduli come bozze utilizzando la funzione di salvataggio automatico.

Puoi anche configurare un modulo adattivo in modo che venga salvato automaticamente in base a un evento basato sul tempo, affinché il modulo venga salvato dopo la durata specificata. Quando [abiliti i componenti di Forms Portal per il tuo ambiente](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment), la scheda **Salvataggio automatico** viene visualizzata nelle proprietà del contenitore Forms. Puoi configurare la funzione di salvataggio automatico per un modulo adattivo:

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fai clic sull&#39;icona Proprietà contenitore guida ![Proprietà guida](/help/forms/assets/configure-icon.svg) e apri la scheda **[!UICONTROL Salvataggio automatico]**.

   ![Salvataggio automatico](/help/forms/assets/auto-save.png){width="250" align="center"}

1. Selezionare la casella di controllo **[!UICONTROL Abilita]** per abilitare il salvataggio automatico del modulo.
1. Configura **[!UICONTROL Trigger]** come **Basato sul tempo**, per salvare automaticamente il modulo <!--based on the occurrence of an event or--> dopo un intervallo di tempo specifico.
1. Specificare l&#39;intervallo di tempo in **[!UICONTROL Salvataggio automatico in questo intervallo (in secondi)]** per impostare la durata che attiva il salvataggio automatico del modulo nell&#39;intervallo definito.
1. Fai clic su **[!UICONTROL Fine]**.

## Visualizzare le bozze/i moduli inviati nella pagina Sites utilizzando il componente Bozze e invii

Per visualizzare le bozze salvate o i moduli inviati, utilizza il componente **Bozze e invii** di Forms Portal.
Quando **[!UICONTROL Seleziona tipo]** è selezionato come **Bozza di Forms** nella [finestra di dialogo per configurazione del componente Bozze e invii](#configure-properties-of-the-drafts--submissions-component), i moduli salvati come bozze vengono visualizzati nella pagina Sites. Per aprire le bozze, fai clic sui puntini di sospensione (...) e completa il modulo.

![Icona Bozze](assets/drafts-component.png){width="250" align="center"}

Quando **[!UICONTROL Seleziona tipo]** è selezionato come **Forms inviato** nella [finestra di dialogo per configurazione del componente Bozze e invii](#configure-properties-of-the-drafts--submissions-component), vengono visualizzati i moduli inviati. È possibile visualizzare i moduli inviati ma non modificarli.

![Icona Invii](assets/submission-listing.png){width="250" align="center"}

È inoltre possibile eliminare i moduli facendo clic sui puntini di sospensione (...) visualizzati nell&#39;angolo inferiore destro del modulo.

## Passaggi successivi

Nel prossimo articolo, scopri [come aggiungere riferimenti ai moduli nella pagina Sites utilizzando il componente Collega portale Forms](/help/forms/add-form-link-to-aem-sites-page.md).

## Articoli correlati

{{forms-portal-see-also}}

## Consulta anche {#see-also}

{{see-also}}