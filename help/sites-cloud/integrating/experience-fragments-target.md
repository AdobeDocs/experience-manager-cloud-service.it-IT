---
title: Esportazione di frammenti di esperienza in Adobe Target
description: Esportazione di frammenti di esperienza in Adobe Target
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 8e13f671ada67e4e22b66094ad23bf5a0508ccba
workflow-type: tm+mt
source-wordcount: '2259'
ht-degree: 1%

---

# Esportazione di frammenti di esperienza in Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* I frammenti esperienza AEM vengono esportati nell’area di lavoro predefinita di Adobe Target.
>* AEM deve essere integrato con Adobe Target secondo le istruzioni di cui [Integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).


Puoi esportare [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md), creato in Adobe Experience Manager as a Cloud Service (AEM), in Adobe Target (Target). Possono quindi essere utilizzati come offerte nelle attività di Target, per testare e personalizzare le esperienze su larga scala.

Sono disponibili tre opzioni per esportare un frammento esperienza in Adobe Target:

* HTML (predefinito): Supporto per la distribuzione di contenuti web e ibridi
* JSON: Supporto per la distribuzione di contenuti headless
* HTML e JSON

Per preparare la tua istanza per l’esportazione AEM frammenti esperienza in Adobe Target, devi:

* [Procedi all’integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Aggiungere la configurazione cloud](#add-the-cloud-configuration)
* [Aggiungere la configurazione legacy](#add-the-legacy-configuration)

Dopo di che puoi:

* [Esportare un frammento esperienza in Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [Utilizzare i frammenti esperienza in Adobe Target](#using-your-experience-fragments-in-adobe-target)
* E anche [Eliminare un frammento esperienza già esportato in Adobe Target](#deleting-an-experience-fragment-already-exported-to-adobe-target)

I frammenti esperienza possono essere esportati nell’area di lavoro predefinita in Adobe Target o in aree di lavoro definite dall’utente per Adobe Target.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target non esistono in Adobe Target. Vengono definiti e gestiti in Adobe IMS (Identity Management System), quindi selezionati per l’utilizzo nelle soluzioni tramite Adobe Developer Console.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target possono essere utilizzate per consentire ai membri di un&#39;organizzazione (gruppo) di creare e gestire offerte e attività solo per questa organizzazione; senza dare accesso ad altri utenti. Ad esempio, organizzazioni specifiche per paese nell&#39;ambito di una preoccupazione globale.

>[!NOTE]
>
>Per ulteriori informazioni, consulta anche:
>
>* [Sviluppo Adobe Target](http://developers.adobetarget.com/)
>* [Componenti core - Frammenti esperienza](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
>* [Adobe Target - Come Si Utilizzano I Frammenti Esperienza Adobe Experience Manager (AEM)?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)
>* [AEM 6.5 - Configurazione manuale dell’integrazione con Adobe Target - Creazione di una configurazione Cloud di Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)


## Prerequisiti {#prerequisites}

Sono necessarie diverse azioni:

1. Devi [integrare AEM con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. I frammenti esperienza vengono esportati dall’istanza di authoring AEM, per cui devi [Configurare AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) nell’istanza di authoring, per garantire che tutti i riferimenti all’interno del frammento esperienza siano esternalizzati per la distribuzione web.

   >[!NOTE]
   >
   >Per la riscrittura di collegamenti non coperti dall’impostazione predefinita, la variabile [Provider di rewriter del collegamento del frammento esperienza](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) è disponibile. Con questo, è possibile sviluppare regole personalizzate per la tua istanza.

## Aggiungere la configurazione cloud {#add-the-cloud-configuration}

Prima di esportare un frammento è necessario aggiungere il **Configurazione cloud** per **Adobe Target** al frammento o alla cartella. Questo consente anche di:

* specifica le opzioni di formato da utilizzare per l’esportazione
* selezionare un’area di lavoro di Target come destinazione
* seleziona un dominio esternalizzatore per riscrivere i riferimenti nel frammento esperienza (facoltativo)

Le opzioni richieste possono essere selezionate in **Proprietà pagina** della cartella e/o del frammento richiesti; la specifica viene ereditata in base alle necessità.

1. Passa a **Frammenti esperienza** console.

1. Apri **Proprietà pagina** per la cartella o il frammento appropriato.

   >[!NOTE]
   >
   >Se aggiungi la configurazione cloud alla cartella principale Frammento esperienza, questa viene ereditata da tutti gli elementi secondari.
   >
   >Se aggiungi la configurazione cloud al frammento esperienza stesso, questa viene ereditata da tutte le varianti.

1. Seleziona la **Cloud Services** scheda .

1. Sotto **Configurazione Cloud Service**, seleziona **Adobe Target** dall’elenco a discesa.

   >[!NOTE]
   >
   >È possibile personalizzare il formato JSON di un’offerta Frammento esperienza. A questo scopo, definisci un componente Frammento esperienza cliente e poi annota come esportare le sue proprietà nel modello Sling del componente.
   >
   >Consulta il componente core : [Componenti core - Frammenti esperienza](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. Sotto **Adobe Target** seleziona:

   * la configurazione appropriata
   * l&#39;opzione di formato richiesta
   * un’area di lavoro Adobe Target
   * se necessario - il dominio esternalizzatore

   >[!CAUTION]
   >
   >Il dominio dell&#39;esternalizzatore è facoltativo.
   >
   > Un esternalizzatore AEM è configurato quando desideri che il contenuto esportato punti a uno specifico *pubblicare* dominio. Per ulteriori dettagli vedi [Configurazione di AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > Inoltre, i domini esternalizzatori sono rilevanti solo per il contenuto del frammento esperienza inviato a Target, e non per i metadati come Visualizza contenuto offerta.

   Ad esempio, per una cartella:

   ![Cartella - Cloud Services](assets/xf-target-integration-01.png "Cartella - Cloud Services")

1. **Salva e chiudi**.

## Aggiungere la configurazione legacy {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>L’aggiunta di una nuova configurazione legacy è uno scenario speciale supportato solo per l’esportazione di frammenti esperienza.

Dopo [aggiunta della configurazione cloud](#add-the-cloud-configuration) per utilizzare Launch by Adobe, per integrare inizialmente AEM con Adobe Target, è inoltre necessario eseguire l’integrazione manuale con Adobe Target utilizzando una configurazione legacy.

### Creazione di una configurazione cloud di Target {#creating-a-target-cloud-configuration}

Per consentire a AEM di interagire con Adobe Target, crea una configurazione cloud di Target. Per creare la configurazione, fornisci il codice client Adobe Target e le credenziali utente.

Puoi creare la configurazione cloud di Target una sola volta perché puoi associare la configurazione a più campagne AEM. Se disponi di diversi codici client Adobe Target, crea una configurazione per ogni codice client.

Puoi configurare la configurazione cloud per sincronizzare i segmenti da Adobe Target. Se abiliti la sincronizzazione, i segmenti vengono importati in background da Target non appena viene salvata la configurazione cloud.

Segui la procedura seguente per creare una configurazione cloud di Target in AEM:

1. Passa a **Cloud Services legacy** tramite **Logo AEM** > **Strumenti** > **Cloud Services** > **Cloud Services legacy**.
Ad esempio: ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   La **Adobe Experience Cloud** viene visualizzata la pagina della panoramica.

1. In **Adobe Target** sezione, fai clic su **Configura ora**.
1. In **Crea configurazione** finestra di dialogo:

   1. Assegna alla configurazione un **Titolo**.
   1. Seleziona la **Configurazione Adobe Target** modello.
   1. Fai clic su **Crea**.

Ora puoi selezionare la nuova configurazione da modificare.

1. Viene visualizzata la finestra di dialogo di modifica.

   ![config-target-settings-dialog](assets/config-target-settings-dialog.png)

   <!-- Can this still occur?

   >[!NOTE]
   >
   >When configuring A4T with AEM, you may see a Configuration reference missing entry. To be able to select the analytics framework, do the following:
   >
   >1. Navigate to **Tools** &gt; **General** &gt; **CRXDE Lite**.
   >1. Navigate to **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   >1. Set the property **disable** to **false**.
   >1. Tap or click **Save All**.

   -->

1. In **Impostazioni di Adobe Target** fornire valori per queste proprietà.

   * **Autenticazione**: per impostazione predefinita, IMS (le credenziali utente sono obsolete)

   * **Codice client**: il codice client dell’account di Target

   * **ID tenant**: ID tenant

   * **Configurazione IMS**: seleziona la configurazione desiderata dall’elenco a discesa

   * **Tipo di API**: impostazione predefinita REST (XML è obsoleto)

   * **Configurazione di A4T Analytics Cloud**: Seleziona la configurazione cloud di Analytics utilizzata per gli obiettivi e le metriche delle attività di destinazione. È necessario se utilizzi Adobe Analytics come origine per la generazione di rapporti durante il targeting del contenuto.

      <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **Utilizza targeting accurato:** Per impostazione predefinita questa casella di controllo è selezionata. Se questa opzione è selezionata, la configurazione del servizio cloud attenderà il caricamento del contesto prima di caricare il contenuto. Vedi la nota che segue.

   * **Sincronizza segmenti da Adobe Target:** Seleziona questa opzione per scaricare i segmenti definiti in Target e utilizzarli in AEM. Devi selezionare questa opzione quando la proprietà Tipo API è REST, perché i segmenti in linea non sono supportati e devi sempre utilizzare i segmenti da Target. Il termine AEM &quot;segmento&quot; è equivalente al &quot;pubblico&quot; di Target.

   * **Libreria client:** questo valore predefinito è AT.js (mbox.js è obsoleto)

      >[!NOTE]
      >
      >Il file della libreria di Target, [AT.JS](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html), è una nuova libreria di implementazione per Adobe Target progettata sia per le tipiche implementazioni web che per le applicazioni a pagina singola.
      >
      >mbox.js è stato dichiarato obsoleto e verrà rimosso in una fase successiva.
      >
      >Adobe consiglia di utilizzare AT.js invece di mbox.js come libreria client.
      >
      >AT.js offre diversi miglioramenti rispetto alla libreria mbox.js :
      >
      >* Tempi di caricamento delle pagine migliorati per le implementazioni web
      >* Maggiore sicurezza
      >* Migliori opzioni di implementazione per le applicazioni a pagina singola
      >* AT.js contiene i componenti inclusi in target.js, quindi cessano le chiamate a target.js

      >
      >È possibile selezionare AT.js o mbox.js nel **Libreria client** menu a discesa.

   * **Utilizza Tag Management System per distribuire la libreria client** - Seleziona questa opzione per utilizzare la libreria client da Adobe Launch o da un altro sistema di gestione tag (o DTM, che è obsoleto).

   * **AT.js personalizzato**: Sfoglia per caricare il tuo AT.js personalizzato. Lascia vuoto per utilizzare la libreria predefinita.

      >[!NOTE]
      >
      >Per impostazione predefinita, quando si sceglie di accedere alla procedura guidata di configurazione di Adobe Target, il targeting accurato è abilitato.
      >
      >Il targeting accurato significa che la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Di conseguenza, in termini di prestazioni, un targeting accurato può creare un ritardo di alcuni millisecondi prima del caricamento del contenuto.
      >
      >Il targeting accurato è sempre abilitato nell’istanza di authoring. Tuttavia, nell’istanza di pubblicazione puoi scegliere di disattivare il targeting accurato a livello globale cancellando il segno di spunta accanto a Targeting accurato nella configurazione del servizio cloud (**http://localhost:4502/etc/cloudservices.html**). Puoi inoltre attivare e disattivare il targeting accurato per i singoli componenti indipendentemente dall’impostazione nella configurazione del servizio cloud.
      >
      >Se ***già*** i componenti di destinazione creati e modificate questa impostazione, le modifiche non influiscono su tali componenti. Devi apportare direttamente le modifiche a tali componenti.

1. Fai clic su **Connettersi ad Adobe Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita** viene visualizzato. Fai clic su **OK** sul messaggio e quindi **OK** nella finestra di dialogo.

   Se non riesci a connetterti a Target, consulta la sezione [risoluzione](#troubleshooting-target-connection-problems) sezione .

### Aggiunta di un framework di Target {#adding-a-target-framework}

<!-- Is this section needed? -->

Dopo aver configurato la configurazione cloud di Target, aggiungi un framework di Target. Il framework identifica i parametri predefiniti inviati ad Adobe Target dalla [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) componenti. Target utilizza i parametri per determinare i segmenti che si applicano al contesto corrente.

Puoi creare più framework per una singola configurazione di Target. I framework multipli sono utili quando devi inviare un diverso set di parametri a Target per diverse sezioni del sito web. Crea un framework per ogni set di parametri da inviare. Associa ogni sezione del sito web al framework appropriato. Nota t*che una pagina web può utilizzare un solo framework alla volta.

1. Nella pagina di configurazione di Target, fai clic su **+** (segno più) accanto a Configurazioni disponibili.

1. Nella finestra di dialogo Crea framework , specifica un **Titolo**, seleziona **Framework Adobe Target** e fai clic su **Crea**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   Viene visualizzata la pagina del framework. La barra laterale fornisce componenti che rappresentano informazioni provenienti da [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) che puoi mappare.

   <!-- ![chlimage_1-162](assets/chlimage_1-162.png) -->

1. Trascina il componente ClientContext che rappresenta i dati da utilizzare per la mappatura sulla destinazione di rilascio. In alternativa, trascina il **Archivio ContextHub** componente del framework.

   >[!NOTE]
   >
   >Durante la mappatura, i parametri vengono passati a una mbox tramite stringhe semplici. Non è possibile mappare array da ContextHub.

   Ad esempio, per utilizzare **Dati profilo** informazioni sui visitatori del sito per controllare la campagna Target, trascina **Dati profilo** alla pagina. Vengono visualizzate le variabili dei dati di profilo disponibili per la mappatura ai parametri di Target.

   <!-- ![chlimage_1-163](assets/chlimage_1-163.png) -->

1. Seleziona le variabili da rendere visibili al sistema Adobe Target selezionando la **Condividi** nelle colonne appropriate.

   <!-- ![chlimage_1-164](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >La sincronizzazione dei parametri è solo unidirezionale, da AEM ad Adobe Target.

Viene creato il framework. Per replicare il framework nell&#39;istanza di pubblicazione, utilizza il **Attiva framework** dalla barra laterale.

<!--
### Associating Activities With the Target Cloud Configuration  {#associating-activities-with-the-target-cloud-configuration}

Associate your [AEM activities](/help/sites-cloud/authoring/personalization/activities.md) with your Target cloud configuration so that you can mirror the activities in [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
>What types of activities are available is determined by the following:
>
>* If the **xt_only** option is enabled on the Adobe Target tenant (clientcode) used on the AEM side to connect to Adobe Target, then you can create **only** XT activities in AEM.
>
>* If the **xt_only** options is **not** enabled on the Adobe Target tenant (clientcode), then you can create **both** XT and A/B activities in AEM.
>
>**Additional note:** **xt_only** options is a setting applied on a certain Target tenant (clientcode) and can only be modified directly in Adobe Target. You cannot enable or disable this option in AEM.
-->

<!--
### Associating the Target Framework With Your Site {#associating-the-target-framework-with-your-site}

After you create a Target framework in AEM, associate your web pages with the framework. The targeted components on the pages send the framework-defined data to Adobe Target for tracking. (See [Content Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).)

When you associate a page with the framework, the child pages inherit the association.

1. In the **Sites** console, navigate to the site that you want to configure.
1. Using either [quick actions](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) or [selection mode](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources), select **View Properties.**
1. Select the **Cloud Services** tab.
1. Tap/click **Edit**.
1. Tap/click **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![chlimage_1-165](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Tap/click **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which allows you to publish it as well.
-->

<!--
### Troubleshooting Target Connection Problems {#troubleshooting-target-connection-problems}

Perform the following tasks to troubleshoot problems that occur when connecting to Target:

* Make sure that the user credentials that you provide are correct.
* Make sure that the AEM instance can connect to the Target server. For example, make sure that firewall rules are not blocking outbound AEM connections, or that AEM is configured to use necessary proxies.
* Look for helpful messages in the AEM error log. The error.log file is located in the **crx-quickstart/logs** directory where AEM is installed.
* When editing the activity in Adobe Target, the URL is pointing to localhost. Work around this by setting the AEM externalizer to the correct URL.
-->

## Esportazione di un frammento esperienza in Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Per le risorse multimediali, come le immagini, viene esportato solo un riferimento a Target. La risorsa stessa rimane memorizzata in AEM Assets e viene distribuita dall’istanza di pubblicazione AEM.
>
>Per questo motivo è necessario pubblicare il frammento esperienza con tutte le relative risorse prima di esportare in Target.

Per esportare un frammento di esperienza da AEM a Target (dopo aver specificato la configurazione cloud):

1. Passa alla console Frammenti esperienza .
1. Seleziona il frammento esperienza da esportare nella destinazione.

   >[!NOTE]
   >
   >Deve essere una variante Web del frammento esperienza.

1. Tocca o fai clic su **Esportazione in Adobe Target**.

   >[!NOTE]
   >
   >Se il frammento esperienza è già stato esportato, seleziona **Aggiornamento in Adobe Target**.

1. Tocca o fai clic su **Esportazione senza pubblicazione** o **Pubblica** se necessario.

   >[!NOTE]
   >
   >Selezione **Pubblica** pubblicherà immediatamente il frammento di esperienza e lo invierà a Target.

1. Tocca o fai clic su **OK** nella finestra di dialogo di conferma.

   Il frammento esperienza deve ora essere in Target.

   >[!NOTE]
   >
   >[Vari dettagli](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) dell&#39;esportazione è visibile in **Vista a elenco** della console e **Proprietà**.

   >[!NOTE]
   >
   >Quando visualizzi un frammento esperienza in Adobe Target, la funzione *ultima modifica* La data visualizzata è la data dell’ultima modifica apportata al frammento in AEM, non la data dell’ultima esportazione del frammento in Adobe Target.

>[!NOTE]
>
>In alternativa, è possibile eseguire l’esportazione dall’editor di pagine utilizzando comandi comparabili nella sezione [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) menu.

## Utilizzo dei frammenti esperienza in Adobe Target {#using-your-experience-fragments-in-adobe-target}

Dopo aver eseguito le attività precedenti, il frammento di esperienza viene visualizzato nella pagina Offerte di Target. Per favore, dai un&#39;occhiata al [documentazione specifica di Target](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) per scoprire cosa è possibile ottenere.

>[!NOTE]
>
>Quando visualizzi un frammento esperienza in Adobe Target, la funzione *ultima modifica* La data visualizzata è la data dell’ultima modifica apportata al frammento in AEM, non la data dell’ultima esportazione del frammento in Adobe Target.

## Eliminazione di un frammento esperienza già esportato in Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

L’eliminazione di un frammento esperienza già esportato in Target potrebbe causare problemi se il frammento è già utilizzato in un’offerta in Target. L’eliminazione del frammento renderebbe l’offerta inutilizzabile mentre il contenuto del frammento viene consegnato da AEM.

Per evitare tali situazioni:

* Se il frammento esperienza non è attualmente utilizzato in un’attività, AEM consente all’utente di eliminare il frammento senza un messaggio di avviso.
* Se il frammento esperienza è attualmente utilizzato da un’attività in Target, un messaggio di errore avvisa l’utente AEM delle possibili conseguenze che l’eliminazione del frammento avrà sull’attività.

   Il messaggio di errore in AEM non impedisce all’utente di (forzare-)eliminare il frammento esperienza. Se il frammento esperienza viene eliminato:

   * L’offerta Target con AEM Frammento esperienza può mostrare un comportamento indesiderato

      * È probabile che l’offerta venga comunque riprodotta in seguito al push di Experience Fragment HTML a Target
      * Eventuali riferimenti nel frammento esperienza potrebbero non funzionare correttamente se le risorse di riferimento sono state eliminate anche in AEM.
   * Naturalmente, eventuali ulteriori modifiche al frammento esperienza sono impossibili in quanto il frammento esperienza non esiste più in AEM.
