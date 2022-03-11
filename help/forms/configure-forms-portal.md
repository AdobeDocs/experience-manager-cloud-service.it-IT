---
title: Come creare un portale Forms su una pagina Experience Manager Sites
description: Scopri come creare un portale Forms e utilizzare i componenti core predefiniti in una pagina AEM Sites.
exl-id: 13cfe3ba-2e85-46bf-a029-2673de69c626
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 1%

---

# Elencare Forms adattivo su un portale {#publish-forms-on-portal}

In uno scenario di distribuzione tipico del portale incentrato sui moduli, lo sviluppo dei moduli e lo sviluppo del portale sono due attività discongiunte. Mentre i progettisti di moduli progettano e memorizzano i moduli in un archivio, gli sviluppatori web creano un’applicazione Web per elencare i moduli e gestire l’invio dei moduli. Forms viene copiato sul livello web in quanto non vi è comunicazione tra l’archivio dei moduli e l’applicazione web.

Tali scenari si traducono spesso in problemi di gestione e ritardi nella produzione. Ad esempio, se nella directory archivio è disponibile una versione più recente del modulo, è necessario sostituire il modulo sul livello Web, modificare l’applicazione Web e ridistribuire il modulo sul sito pubblico. La ridistribuzione dell&#39;applicazione Web potrebbe causare tempi di inattività del server. In genere, i tempi di inattività del server sono un’attività pianificata e pertanto le modifiche non possono essere inviate istantaneamente al sito pubblico.

AEM Forms fornisce componenti del portale che riducono i costi generali di gestione e i ritardi di produzione. I componenti consentono agli sviluppatori web di creare e personalizzare un portale Forms sui siti web creati con Adobe Experience Manager (AEM).

I componenti del portale moduli consentono di aggiungere le seguenti funzionalità:

* Elencare moduli in layout personalizzati. Sono disponibili layout predefiniti per le viste a elenco e a schede. Puoi creare layout personalizzati.
* Consente di visualizzare metadati personalizzati e azioni personalizzate durante l’elenco.
* Elenca i moduli pubblicati dall’interfaccia utente di AEM Forms nell’istanza di pubblicazione in cui vengono utilizzati i componenti di Forms Portal.
* Consentire agli utenti finali di eseguire il rendering dei moduli in formato HTML e PDF.
* Abilita la ricerca di moduli in base al titolo e alla descrizione.
* Utilizza CSS personalizzati per personalizzare l’aspetto del portale.
* Creare collegamenti ai moduli.
* Elenca le bozze e gli invii relativi a Adaptive Forms creati dall&#39;utente finale.

## Componenti di una pagina del portale Forms {#forms-portal-components}

AEM Forms fornisce i seguenti componenti del portale:

* Ricerca e filtro: Questo componente consente di elencare i moduli dall’archivio moduli nella pagina del portale e fornisce opzioni di configurazione per elencare i moduli in base a criteri specifici.

* Bozze e invii: Mentre il componente Ricerca e filtro visualizza i moduli resi pubblici dall’autore di Forms, il componente Bozze e invii visualizza i moduli salvati come bozze per essere completati in seguito e inviati. Questo componente offre un’esperienza personalizzata a qualsiasi utente connesso.

* Collegamento: Questo componente consente di creare un collegamento a un modulo in qualsiasi punto della pagina.

È possibile [importare i componenti predefiniti di Forms Portal](#import-forms-portal-components-aem-archetype) dall&#39;Archetipo di progetto AEM. Dopo l’importazione, esegui le seguenti configurazioni:
* [Configurare uno spazio di archiviazione esterno](#configure-azure-storage-adaptive-forms)
* [Abilitare i componenti del portale Forms](#enable-forms-portal-components)
* [Configurare i componenti del portale Forms](#configure-forms-portal-components)

## Importare componenti del portale Forms {#import-forms-portal-components-aem-archetype}

Per importare componenti predefiniti di Forms Portal su AEM Forms as a Cloud Service, esegui i seguenti passaggi:

1. **Clona l’archivio Git di Cloud Manager nella tua istanza di sviluppo locale:**  L’archivio Git di Cloud Manager contiene un progetto AEM predefinito. Si basa su [Archetipo AEM](https://github.com/adobe/aem-project-archetype/). Clona il tuo archivio Git di Cloud Manager utilizzando Self-Service Git Account Management dall’interfaccia utente di Cloud Manager per portare il progetto nell’ambiente di sviluppo locale. Per informazioni dettagliate sull&#39;accesso all&#39;archivio, vedi [Accesso agli archivi](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **Crea [!DNL Experience Manager Forms] come [Cloud Service] progetto:** Crea [!DNL Experience Manager Forms] come [Cloud Service] basato su [Archetipo AEM 27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) o successiva. L’archetipo aiuta gli sviluppatori a iniziare facilmente a sviluppare per [!DNL AEM Forms] as a Cloud Service. Include inoltre alcuni temi e modelli di esempio per aiutarti a iniziare rapidamente.

   Per creare [!DNL Experience Manager Forms] Progetto as a Cloud Service, apri il prompt dei comandi ed esegui il comando sottostante. Per includere [!DNL Forms] configurazioni, temi e modelli specifici, set `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Inoltre, cambia `appTitle`, `appId`e `groupId`, nel comando precedente per riflettere l&#39;ambiente.

1. **In Prerelease, esegui i seguenti passaggi per utilizzare i componenti del portale Forms:**
   * [Abilita il canale prerelease](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en).
   * Sostituisci `core-forms-components-*` con la versione prerelease desiderata (ad esempio, 1.0.4-PRERELEASE-20211223) nel tuo `Cloud Manager/AEM Archetype` il progetto aggiornando `<core.forms.components.version>x.y.z</core.forms.components.version>` nel livello principale `pom.xml` del progetto Archetype.

1. **Distribuisci il progetto nell’ambiente di sviluppo locale:** È possibile utilizzare il comando seguente per distribuire nell&#39;ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Per l&#39;elenco completo dei comandi, vedere [Creazione e installazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Distribuisci il codice nel tuo [!DNL AEM Forms] Ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## Configurare l’archiviazione Azure per Forms adattivo {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md) fornisce [!DNL Azure] configurazione di archiviazione per integrare i moduli con [!DNL Azure] servizi di storage. Il modello dati modulo può essere utilizzato per creare un Forms adattivo che interagisca con [!DNL Azure] per abilitare i flussi di lavoro aziendali.

### Crea configurazione archiviazione Azure {#create-azure-storage-configuration}

Prima di eseguire questi passaggi, assicurati di disporre di un account di archiviazione di Azure e di una chiave di accesso per autorizzare l’accesso a [!DNL Azure] account di archiviazione.

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Archiviazione di Azure]**.
1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.
1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo .
1. Specifica il nome della [!DNL Azure] account di archiviazione nel **[!UICONTROL Account di archiviazione di Azure]** campo .

### Configurare il connettore di archiviazione unificata per il portale Forms {#configure-usc-forms-portal}

Esegui i seguenti passaggi per configurare Unified Storage Connector per i flussi di lavoro AEM:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.
1. In **[!UICONTROL Portale Forms]** sezione , seleziona **[!UICONTROL Azure]** dal **[!UICONTROL Storage]** elenco a discesa.
1. Specifica la [percorso di configurazione per la configurazione di archiviazione di Azure](#create-azure-storage-configuration) in **[!UICONTROL Percorso di configurazione dell&#39;archiviazione]** campo .
1. Tocca **[!UICONTROL Pubblica]** quindi tocca **[!UICONTROL Salva]** per salvare la configurazione.

## Abilita componenti del portale Forms {#enable-forms-portal-components}

Per utilizzare qualsiasi componente di base (inclusi i componenti del portale predefiniti) in un sito Adobe Experience Manager (AEM), è necessario creare un componente proxy e abilitarlo per il sito. Per creare un componente proxy e abilitare i componenti del portale, vedi [Utilizzo dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

Una volta abilitato un componente portale, puoi utilizzarlo nell’istanza di authoring della pagina Sites.

## Aggiungere e configurare i componenti del portale Forms {#configure-forms-portal-components}

Puoi creare e personalizzare Forms Portal sui siti web creati utilizzando AEM aggiungendo e configurando i componenti del portale. Assicurati che [componenti abilitati](#enable-forms-portal-components) prima di utilizzarli nel portale Forms.

Per aggiungere un componente, trascinalo dal riquadro Componenti al contenitore di layout nella pagina oppure tocca l’icona di aggiunta nel contenitore di layout e aggiungi il componente dal [!UICONTROL Inserisci nuovo componente] finestra di dialogo.

### Configura il componente Bozze e invii {#configure-drafts-submissions-component}

Il componente Bozze e invii visualizza i moduli salvati come bozze per essere completati in seguito e inviati. Per configurare, tocca il componente e quindi tocca il ![Icona Configura](assets/configure_icon.png). In [!UICONTROL Bozze e invii] specificare il titolo per indicare l’elenco dei moduli come bozze o moduli inviati. Seleziona anche se il componente deve elencare i moduli bozza o i moduli inviati in formato scheda o elenco.

![Icona Bozze](assets/drafts-component.png)

![Icona Invii](assets/submission-listing.png)

### Configura componente Ricerca e Registrazione {#configure-search-lister-component}

Il componente Ricerca e filtro viene utilizzato per elencare i moduli adattivi su una pagina e per implementare la ricerca nei moduli elencati.

![Icona Ricerca e filtro](assets/search-and-lister-component.png)

Per configurare, tocca il componente e quindi tocca il ![Icona Configura](assets/configure_icon.png). La [!UICONTROL Ricerca e filtro] viene visualizzata la finestra di dialogo .

1. In [!UICONTROL Visualizzazione] configura quanto segue:
   * In **[!UICONTROL Titolo]**, specifica il titolo del componente Ricerca e filtro . Un titolo indicativo consente agli utenti di eseguire ricerche rapide nell’elenco dei moduli.
   * Da **[!UICONTROL Layout]** selezionare il layout per rappresentare i moduli in formato scheda o elenco.
   * Seleziona **[!UICONTROL Nascondi ricerca]** e **[!UICONTROL Nascondi ordinamento]** per nascondere la ricerca e l&#39;ordinamento in base alle funzioni.
   * In **[!UICONTROL Descrizione comandi]**, fornisce la descrizione comando visualizzata quando passi il cursore del mouse sul componente.
1. In [!UICONTROL Cartella risorse] specificare il percorso in cui i moduli vengono estratti ed elencati nella pagina. È possibile configurare più posizioni di cartelle.
1. In [!UICONTROL Risultati] configurare il numero massimo di moduli da visualizzare per pagina. Il valore predefinito è otto moduli per pagina.

### Configura componente collegamento {#configure-link-component}

Il componente Collegamento consente di fornire collegamenti a un modulo adattivo sulla pagina. Per configurare, tocca il componente e quindi tocca il ![Icona Configura](assets/configure_icon.png). La [!UICONTROL Modifica componente Collegamento] viene visualizzata la finestra di dialogo .

1. In [!UICONTROL Visualizzazione] , fornisce la didascalia di collegamento e la descrizione comando per facilitare l’identificazione dei moduli rappresentati dal collegamento.
1. In [!UICONTROL Informazioni risorsa] Specifica il percorso del repository in cui è memorizzata la risorsa.
1. In [!UICONTROL Parametri query] specifica i parametri aggiuntivi nel formato della coppia chiave-valore . Quando fai clic sul collegamento, questi parametri aggiuntivi vengono passati insieme al modulo.

## Configurare l’invio asincrono dei moduli con Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

Puoi configurare l’invio di un modulo adattivo solo dopo che tutti i destinatari avranno completato la cerimonia di firma. Segui i passaggi riportati di seguito per configurare l’impostazione utilizzando Adobe Sign.

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, tocca l’icona Proprietà ed espandi il **[!UICONTROL SEGNALAZIONE ELETTRONICA]** opzione .
1. Seleziona **[!UICONTROL Abilita Adobe Sign]**. Vengono visualizzate varie opzioni di configurazione.
1. In [!UICONTROL Invia il modulo] seleziona la sezione **[!UICONTROL dopo che ogni destinatario ha completato la cerimonia di firma]** opzione per configurare l’azione Invia modulo , in cui il modulo viene inviato per la prima volta a tutti i destinatari per la firma. Dopo che tutti i destinatari hanno firmato il modulo, viene inviato solo il modulo.

## Salva Forms adattivo come bozze {#save-adaptive-forms-as-drafts}

È possibile salvare i moduli come bozze per completarli in un secondo momento. Esistono due modi in cui un modulo viene salvato come bozza:
* Crea una regola &quot;Salva modulo&quot; su un componente modulo, ad esempio un pulsante. Facendo clic sul pulsante, la regola viene attivata e il modulo viene salvato come bozza.
* Attiva la funzione di salvataggio automatico, che salva il modulo in base all’evento specificato o dopo un intervallo di tempo configurato.

### Creare regole per salvare un modulo adattivo come bozza {#rule-to-save-adaptive-form-as-draft}

Per creare una regola &quot;Salva modulo&quot; su un componente modulo, ad esempio un pulsante, segui la procedura seguente:

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, tocca ![Icona Componenti](assets/components_icon.png) e trascinare il [!UICONTROL Pulsante] al modulo.
1. Tocca [!UICONTROL Pulsante] quindi tocca ![Icona Configura](assets/configure_icon.png).
1. Tocca [!UICONTROL Modifica regole] per aprire l’Editor regole.
1. Tocca **[!UICONTROL Crea]** per configurare e creare la regola.
1. In [!UICONTROL Quando] seleziona &quot;è cliccato&quot; e nella sezione [!UICONTROL Then] selezionare le opzioni &quot;Salva modulo&quot;.
1. Tocca **[!UICONTROL Fine]** per salvare la regola.

### Abilita salvataggio automatico {#enable-auto-save}

È possibile configurare la funzione di salvataggio automatico per un modulo adattivo come segue:

1. Nell’istanza di authoring, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, tocca il ![Icona Proprietà](assets/configure_icon.png) ed espandere [!UICONTROL SALVATAGGIO AUTOMATICO] opzione .
1. Seleziona la **[!UICONTROL Abilita]** casella di controllo per abilitare il salvataggio automatico del modulo. Puoi configurare le seguenti operazioni:
* Per impostazione predefinita, la [!UICONTROL Evento modulo adattivo] è impostato su &quot;true&quot;, il che implica che il modulo viene salvato automaticamente dopo ogni evento.
* In [!UICONTROL Trigger], configura per attivare il salvataggio automatico in base all’occorrenza di un evento o dopo un intervallo di tempo specifico.
