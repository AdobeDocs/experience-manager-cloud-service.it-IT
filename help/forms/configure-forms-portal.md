---
title: Come creare un portale Forms su una pagina Experience Manager Sites
description: Scopri come creare un portale Forms e utilizzare i componenti core predefiniti in una pagina di AEM Sites.
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 1%

---

# Elencare Forms adattivo su un portale {#publish-forms-on-portal}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/introduction-publishing-forms.html) |
| AEM as a Cloud Service | Questo articolo |

In un tipico scenario di distribuzione di un portale incentrato sui moduli, lo sviluppo di moduli e lo sviluppo di portali sono due attività separate. Mentre i progettisti di moduli progettano e memorizzano i moduli in un repository, gli sviluppatori Web creano un&#39;applicazione Web per elencare i moduli e gestirne l&#39;invio. Forms viene copiato sul livello web in quanto non vi è alcuna comunicazione tra l’archivio dei moduli e l’applicazione web.

Tali scenari spesso causano problemi di gestione e ritardi nella produzione. Ad esempio, se nell&#39;archivio è disponibile una versione più recente di un modulo, è necessario sostituire il modulo sul livello Web, modificare l&#39;applicazione Web e ridistribuire il modulo sul sito pubblico. La ridistribuzione dell’applicazione web potrebbe causare tempi di inattività del server. In genere, il tempo di inattività del server è un’attività pianificata e pertanto le modifiche non possono essere inviate istantaneamente al sito pubblico.

AEM Forms fornisce componenti portale che riducono i costi generali di gestione e i ritardi di produzione. I componenti consentono agli sviluppatori Web di creare e personalizzare un portale Forms nei siti Web creati con Adobe Experience Manager (AEM).

I componenti del portale moduli consentono di aggiungere le funzionalità seguenti:

* Elencare i moduli in layout personalizzati. Sono disponibili i layout della vista a elenco e della vista a schede. È possibile creare layout personalizzati.
* Consente di visualizzare metadati personalizzati e azioni personalizzate durante la visualizzazione dell&#39;elenco.
* Elenca i moduli pubblicati dall’interfaccia utente di AEM Forms nell’istanza di pubblicazione in cui vengono utilizzati i componenti di Forms Portal.
* Consenti agli utenti finali di eseguire il rendering dei moduli in formato HTML e PDF.
* Abilita la ricerca di moduli in base a titolo e descrizione.
* Utilizza CSS personalizzato per personalizzare l’aspetto del portale.
* Creare collegamenti ai moduli.
* Elenca le bozze e gli invii relativi a Adaptive Forms creati dall’utente finale.

## Componenti di una pagina del portale Forms {#forms-portal-components}

AEM Forms fornisce i seguenti componenti portale pronti all’uso:

* Ricerca ed elenco: questo componente consente di elencare i moduli dall’archivio dei moduli alla pagina del portale e fornisce opzioni di configurazione per elencare i moduli in base a criteri specificati.

* Bozze e invii: mentre il componente Ricerca ed elenco visualizza i moduli resi pubblici da Forms Author, il componente Bozze e invii visualizza i moduli salvati come bozze da compilare in un secondo momento e quelli inviati. Questo componente fornisce un’esperienza personalizzata a qualsiasi utente connesso.

* Collegamento: questo componente consente di creare un collegamento a un modulo in un punto qualsiasi della pagina.

È possibile [importare i componenti predefiniti di Forms Portal](#import-forms-portal-components-aem-archetype) dall’archetipo del progetto AEM. Dopo l’importazione, esegui le seguenti configurazioni:

* [Configurare un’archiviazione esterna](#configure-azure-storage-adaptive-forms)

* [Abilitare i componenti di Forms Portal](#enable-forms-portal-components)

* [Configurare i componenti di Forms Portal](#configure-forms-portal-components)

## Importare componenti di Forms Portal {#import-forms-portal-components-aem-archetype}

Per importare componenti predefiniti di Forms Portal su AEM Forms as a Cloud Service, effettua le seguenti operazioni:

1. **Clona l’archivio Git di Cloud Manager nell’istanza di sviluppo locale:**  L’archivio Git di Cloud Manager contiene un progetto AEM predefinito. Si basa su [Archetipo AEM](https://github.com/adobe/aem-project-archetype/). Clona l’archivio Git di Cloud Manager utilizzando la gestione self-service dell’account Git dall’interfaccia utente di Cloud Manager per inserire il progetto nell’ambiente di sviluppo locale. Per informazioni dettagliate sull’accesso all’archivio, consulta [Accesso agli archivi](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **Crea [!DNL Experience Manager Forms] as a [Cloud Service] progetto:** Crea [!DNL Experience Manager Forms] as a [Cloud Service] progetto basato su [AEM Archetipo 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) o più tardi. L’archetipo aiuta gli sviluppatori a iniziare facilmente a sviluppare per [!DNL AEM Forms] as a Cloud Service. Include inoltre alcuni temi e modelli di esempio per aiutarti a iniziare rapidamente.

   Per creare [!DNL Experience Manager Forms] progetto as a Cloud Service, apri il prompt dei comandi ed esegui il comando seguente. Da includere [!DNL Forms] configurazioni, temi e modelli specifici, set `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Inoltre, modifica `appTitle`, `appId`, e `groupId`, nel comando precedente per riflettere l’ambiente.

   Quando il progetto è pronto, aggiorna il `<core.forms.components.version>x.y.z</core.forms.components.version>` proprietà nel livello superiore `pom.xml` del progetto Archetipo per riflettere la versione più recente di [core-forms-components](https://github.com/adobe/aem-core-forms-components) nel tuo `AEM Archetype` progetto.

1. **Implementa il progetto nell’ambiente di sviluppo locale:** Puoi utilizzare il seguente comando per distribuire nell’ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Per l&#39;elenco completo dei comandi, vedere [Creazione e installazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Distribuisci il codice nel tuo [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## Configurare l’archiviazione Azure per Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce [!DNL Azure] configurazione di archiviazione per integrare forms con [!DNL Azure] servizi di storage. Il modello dati modulo può essere utilizzato per creare Forms adattivo che interagisce con [!DNL Azure] per abilitare i flussi di lavoro aziendali.

### Crea configurazione archiviazione Azure {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, assicurati di disporre di un account di archiviazione Azure e di una chiave di accesso per autorizzare l’accesso a [!DNL Azure] account di archiviazione.

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.
1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo.
1. Specifica il nome del [!DNL Azure] account di archiviazione in **[!UICONTROL Account di archiviazione Azure]** campo.

### Configurare il connettore di archiviazione unificata per Forms Portal {#configure-usc-forms-portal}

Per configurare il connettore di archiviazione unificata per i flussi di lavoro AEM, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.
1. In **[!UICONTROL Forms Portal]** sezione, seleziona **[!UICONTROL Azure]** dal **[!UICONTROL Storage]** elenco a discesa.
1. Specifica la [percorso di configurazione per la configurazione dell’archiviazione Azure](#create-azure-storage-configuration) nel **[!UICONTROL Percorso configurazione archiviazione]** campo.
1. Tocca **[!UICONTROL Pubblica]** e quindi tocca **[!UICONTROL Salva]** per salvare la configurazione.

## Abilita componenti di Forms Portal {#enable-forms-portal-components}

Per utilizzare qualsiasi componente core (inclusi i componenti portale predefiniti) in un sito Adobe Experience Manager (AEM), è necessario creare un componente proxy e abilitarlo per il sito. Per creare un componente proxy e abilitare i componenti portale, vedere [Utilizzo dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

Una volta attivato, il componente portale può essere utilizzato nell&#39;istanza di authoring della pagina Sites.

## Aggiungere e configurare componenti di Forms Portal {#configure-forms-portal-components}

Puoi creare e personalizzare Forms Portal sui siti web creati con AEM aggiungendo e configurando i componenti del portale. Assicurati che [i componenti sono abilitati](#enable-forms-portal-components) prima di utilizzarli nel portale Forms.

Per aggiungere un componente, trascina e rilascia il componente dal riquadro Componenti al contenitore di layout sulla pagina, oppure tocca l’icona Aggiungi sul contenitore di layout e aggiungi il componente dal [!UICONTROL Inserisci nuovo componente] .

### Configura componente Bozze e invii {#configure-drafts-submissions-component}

Il componente Bozze e invii visualizza i moduli salvati come bozze da compilare in un secondo momento e quelli inviati. Per configurare, tocca il componente, quindi tocca il ![Icona Configura](assets/configure_icon.png). In [!UICONTROL Bozze e invii] , specificare il titolo per indicare l&#39;elenco dei moduli come bozza o inviati. Seleziona anche se il componente deve elencare le bozze di moduli o i moduli inviati in formato scheda o elenco.

![Icona Bozze](assets/drafts-component.png)

![Icona Invii](assets/submission-listing.png)

### Configurare il componente Ricerca ed elenco {#configure-search-lister-component}

Il componente Ricerca ed Elenco viene utilizzato per elencare i moduli adattivi su una pagina e per implementare la ricerca nei moduli elencati.

![Icona Ricerca ed elenco](assets/search-and-lister-component.png)

Per configurare, tocca il componente, quindi tocca il ![Icona Configura](assets/configure_icon.png). Il [!UICONTROL Ricerca ed elenco] viene visualizzata una finestra di dialogo.

1. In [!UICONTROL Visualizzazione] , configura quanto segue:
   * In entrata **[!UICONTROL Titolo]**, specifica il titolo del componente Ricerca ed elenco. Un titolo indicativo consente agli utenti di eseguire ricerche rapide nell’elenco dei moduli.
   * Dalla sezione **[!UICONTROL Layout]** selezionare il layout per rappresentare i moduli in formato scheda o elenco.
   * Seleziona **[!UICONTROL Nascondi ricerca]** e **[!UICONTROL Nascondi ordinamento]** per nascondere le funzionalità di ricerca e ordinamento.
   * In entrata **[!UICONTROL Descrizione]**, fornisci la descrizione che viene visualizzata quando passi il cursore sul componente.
1. In [!UICONTROL Cartella risorse] , specificare il percorso da cui i moduli vengono estratti ed elencati nella pagina. Puoi configurare più percorsi di cartelle.
1. In [!UICONTROL Risultati] , configura il numero massimo di moduli da visualizzare per pagina. Il valore predefinito è otto moduli per pagina.

### Configura componente collegamento {#configure-link-component}

Il componente collegamento consente di fornire nella pagina i collegamenti a un modulo adattivo. Per configurare, tocca il componente, quindi tocca il ![Icona Configura](assets/configure_icon.png). Il [!UICONTROL Modifica componente collegamento] viene visualizzata una finestra di dialogo.

1. In [!UICONTROL Visualizzazione] , fornisci la didascalia del collegamento e la descrizione comando per facilitare l&#39;identificazione dei moduli rappresentati dal collegamento.
1. In [!UICONTROL Info risorsa] , specifica il percorso dell’archivio in cui è memorizzata la risorsa.
1. In [!UICONTROL Parametri query] , specificare i parametri aggiuntivi nel formato coppia chiave-valore. Quando fai clic sul collegamento, questi parametri aggiuntivi vengono trasmessi insieme al modulo.

## Configurare L’Invio Di Moduli Asincroni Tramite Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

Puoi configurare per l’invio di un modulo adattivo solo quando tutti i destinatari hanno completato la cerimonia di firma. Segui i passaggi seguenti per configurare l’impostazione utilizzando Adobe Sign.

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, tocca l’icona Proprietà ed espandi la sezione **[!UICONTROL FIRMA ELETTRONICA]** opzione.
1. Seleziona **[!UICONTROL Abilita Adobe Sign]**. Vengono visualizzate diverse opzioni di configurazione.
1. In [!UICONTROL Inviare il modulo] , seleziona la sezione **[!UICONTROL dopo che ogni destinatario ha completato la firma]** per configurare l’azione Invia modulo, in cui il modulo viene inviato per la prima volta a tutti i destinatari per la firma. Una volta che tutti i destinatari hanno firmato il modulo, solo allora il modulo viene inviato.

## Salva Forms Adattivo Come Bozze {#save-adaptive-forms-as-drafts}

È possibile salvare i moduli come bozze per completarli in un secondo momento. Esistono due modi in cui un modulo viene salvato come bozza:
* Crea una regola &quot;Salva modulo&quot; su un componente del modulo, ad esempio un pulsante. Facendo clic sul pulsante, la regola viene attivata e il modulo viene salvato come bozza.
* Abilita la funzione di salvataggio automatico, che salva il modulo in base all’evento specificato o dopo un intervallo di tempo configurato.

### Creare regole per salvare un modulo adattivo come bozza {#rule-to-save-adaptive-form-as-draft}

Per creare una regola &quot;Salva modulo&quot; su un componente del modulo, ad esempio un pulsante, segui i passaggi seguenti:

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, tocca ![Icona Componenti](assets/components_icon.png) e trascina [!UICONTROL Pulsante] al modulo.
1. Tocca il [!UICONTROL Pulsante] e quindi tocca il ![Icona Configura](assets/configure_icon.png).
1. Tocca il [!UICONTROL Modifica regole] per aprire l&#39;editor di regole.
1. Tocca **[!UICONTROL Crea]** per configurare e creare la regola.
1. In [!UICONTROL Quando] , seleziona &quot;viene fatto clic&quot; e nella sezione [!UICONTROL Then] , selezionare le opzioni &quot;Salva modulo&quot;.
1. Tocca **[!UICONTROL Fine]** per salvare la regola.

### Abilita salvataggio automatico {#enable-auto-save}

Puoi configurare la funzione di salvataggio automatico per un modulo adattivo come segue:

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, tocca il ![Icona Proprietà](assets/configure_icon.png) ed espandi [!UICONTROL SALVATAGGIO AUTOMATICO] opzione.
1. Seleziona la **[!UICONTROL Abilita]** per abilitare il salvataggio automatico del modulo. Puoi configurare quanto segue:
* Per impostazione predefinita, il [!UICONTROL Evento modulo adattivo] è impostato su &quot;true&quot;, il che implica che il modulo viene salvato automaticamente dopo ogni evento.
* In entrata [!UICONTROL Trigger], configura per attivare il salvataggio automatico in base al verificarsi di un evento o dopo un intervallo di tempo specifico.
