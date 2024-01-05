---
title: Esportazione di frammenti di esperienza in Adobe Target
description: Scopri come esportare i frammenti di esperienza in Adobe Target per testare e personalizzare le esperienze.
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 95%

---

# Esportazione di frammenti di esperienza in Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* I Frammenti di esperienza AEM vengono esportati nell’area di lavoro predefinita di Adobe Target.
>* AEM deve essere integrato con Adobe Target secondo le istruzioni contenute in [Integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

Puoi esportare i [Frammenti di esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) creati in Adobe Experience Manager as a Cloud Service (AEM) in Adobe Target (Target). Puoi quindi utilizzarli come offerte nelle attività di Target, per testare e personalizzare le esperienze su larga scala.

Sono disponibili tre opzioni per esportare un Frammento di esperienza in Adobe Target:

* HTML (predefinito): supporto per la distribuzione di contenuti web e ibridi
* JSON: supporto per la distribuzione di contenuti headless
* HTML e JSON

Per preparare la tua istanza per l’esportazione di Frammenti di esperienza AEM in Adobe Target, devi:

* [Procedi all’integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Aggiungere la configurazione cloud](#add-the-cloud-configuration)
* [Aggiungere la configurazione precedente](#add-the-legacy-configuration)

Dopo di che puoi:

* [Esportare un Frammento di esperienza in Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [Utilizzare i Frammenti di esperienza in Adobe Target](#using-your-experience-fragments-in-adobe-target)
* E anche [Eliminare un Frammento di esperienza già esportato in Adobe Target](#deleting-an-experience-fragment-already-exported-to-adobe-target)

I Frammenti di esperienza possono essere esportati nell’area di lavoro predefinita o in aree di lavoro definite dall’utente in Adobe Target.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target non sono già esistenti in Adobe Target. Vengono definite e gestite in Adobe IMS (Identity Management System), quindi selezionate per l’utilizzo nelle soluzioni tramite la console Adobe Developer.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target possono essere utilizzate per consentire ai membri di un’organizzazione (gruppo) di creare e gestire offerte e attività riservate all’organizzazione; senza dare accesso ad altri utenti. Ad esempio, organizzazioni specifiche per paese nell&#39;ambito di un’azienda globale.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [Sviluppo Adobe Target](https://developers.adobetarget.com/)
>* [Componenti core: Frammenti di esperienza](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
>* [Adobe Target: come si utilizzano i Frammenti di esperienza Adobe Experience Manager (AEM)?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html)
>* [AEM 6.5: configurazione manuale dell’integrazione con Adobe Target; creazione di una configurazione cloud di Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html?lang=it#creating-a-target-cloud-configuration)

## Prerequisiti {#prerequisites}

Sono necessarie diverse azioni:

1. Devi [integrare AEM con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. I Frammenti di esperienza vengono esportati dall’istanza di authoring AEM, per cui devi [Configurare AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) nell’istanza di authoring, per garantire che tutti i riferimenti all’interno del Frammento di esperienza siano esternalizzati per la distribuzione web.

   >[!NOTE]
   >
   >Per la riscrittura di collegamenti non coperti dall’impostazione predefinita, è disponibile il [provider del rewriter di collegamento di Frammento esperienza](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). Con questo, è possibile sviluppare regole personalizzate per la tua istanza.

## Aggiungere la configurazione cloud {#add-the-cloud-configuration}

Prima di esportare un frammento è necessario aggiungere la **Configurazione cloud** di **Adobe Target** al frammento o alla cartella. Questo consente anche di:

* specificare le opzioni di formato da utilizzare per l’esportazione
* selezionare un’area di lavoro di Target come destinazione
* selezionare un dominio esternalizzatore per riscrivere i riferimenti nel Frammento di esperienza (facoltativo)

Le opzioni richieste possono essere selezionate in **Proprietà pagina** della cartella e/o del frammento richiesti; la specifica viene ereditata secondo necessità.

1. Passa alla console **Frammenti di esperienza**.

1. Apri **Proprietà pagina** per la cartella o il frammento appropriato.

   >[!NOTE]
   >
   >Se aggiungi la configurazione cloud alla cartella principale Frammento di esperienza, questa viene ereditata da tutti gli elementi secondari.
   >
   >Se aggiungi la configurazione cloud al Frammento di esperienza stesso, questa viene ereditata da tutte le varianti.

1. Seleziona la scheda **Servizi cloud**.

1. Sotto **Configurazione servizio cloud**, seleziona **Adobe Target** dall’elenco a discesa.

   >[!NOTE]
   >
   >È possibile personalizzare il formato JSON di un’offerta Frammento di esperienza. A questo scopo, definisci un componente Frammento di esperienza cliente e poi annota come esportare le sue proprietà nel modello Sling del componente.
   >
   >Vedi il componente core: [Componenti core: Frammenti esperienza](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html?lang=it)

1. Sotto **Adobe Target** seleziona:

   * la configurazione appropriata
   * l’opzione di formato richiesta
   * un’area di lavoro Adobe Target
   * se necessario, il dominio esternalizzatore

   >[!CAUTION]
   >
   >Il dominio esternalizzatore è facoltativo.
   >
   > Un esternalizzatore AEM è configurato quando desideri che il contenuto esportato punti a uno specifico dominio di *pubblicazione*. Per ulteriori dettagli vedi [Configurazione di AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > Inoltre, i domini esternalizzatori sono rilevanti solo per il contenuto del Frammento di esperienza inviato a Target, e non per i metadati come Visualizza contenuto offerta.

   Ad esempio, per una cartella:

   ![Cartella - Servizi cloud](assets/xf-target-integration-01.png "Cartella - Servizi cloud")

1. **Salva e chiudi**.

## Aggiungere la configurazione precedente {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>L’aggiunta di una nuova configurazione precedente è uno scenario speciale supportato solo per l’esportazione di Frammenti di esperienza.

Dopo l’[aggiunta della configurazione cloud](#add-the-cloud-configuration) per utilizzare Experience Platform Launch, per l’integrare iniziale di AEM con Adobe Target, è inoltre necessario eseguire l’integrazione manuale con Adobe Target utilizzando una configurazione precedente.

### Creazione di una configurazione cloud di Target {#creating-a-target-cloud-configuration}

Per consentire ad AEM di interagire con Adobe Target, crea una configurazione cloud di Target. Per creare la configurazione, fornisci il codice client Adobe Target e le credenziali utente.

Puoi creare la configurazione cloud di Target una sola volta perché tale configurazione può essere associata a più campagne AEM. Se disponi di diversi codici client Adobe Target, crea una configurazione per ogni codice client.

Puoi impostare la configurazione cloud in modo da sincronizzare i segmenti da Adobe Target. Se abiliti la sincronizzazione, i segmenti vengono importati in background da Target non appena viene salvata la configurazione cloud.

Segui la procedura seguente per creare una configurazione cloud di Target in AEM:

1. Passa a **Servizi cloud precedenti** tramite **Logo AEM** > **Strumenti** > **Servizi cloud** > **Servizi cloud precedenti**.
Ad esempio: ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Viene visualizzata la pagina **Adobe Experience Cloud**.

1. Nella sezione **Adobe Target**, fai clic su **Configura ora**.
1. Nella finestra di dialogo **Crea configurazione**:

   1. Assegna alla configurazione un **Titolo**.
   1. Seleziona il modello **Configurazione Adobe Target**.
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
   >1. Select **Save All**.

   -->

1. In **Impostazioni Adobe Target** fornisci i valori per queste proprietà.

   * **Autenticazione**: per impostazione predefinita, IMS (le credenziali utente sono obsolete)

   * **Codice client**: il codice client dell’account di Target

   * **ID tenant**: ID del tenant

   * **Configurazione IMS**: seleziona la configurazione desiderata dall’elenco a discesa

   * **Tipo di API**: impostazione predefinita REST (XML è obsoleto)

   * **Configurazione A4T Analytics Cloud**: seleziona la configurazione cloud di Analytics utilizzata per gli obiettivi e le metriche delle attività di destinazione. È necessario se utilizzi Adobe Analytics come origine per la generazione di rapporti durante il targeting del contenuto.

     <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **Utilizza targeting accurato:** per impostazione predefinita questa casella di controllo è selezionata. Se questa opzione è selezionata, la configurazione del servizio cloud attenderà il caricamento del contesto prima di caricare il contenuto. Vedi la nota che segue.

   * **Sincronizza segmenti da Adobe Target:** seleziona questa opzione per scaricare i segmenti definiti in Target e utilizzarli in AEM. Seleziona questa opzione quando la proprietà Tipo API è REST, perché i segmenti in linea non sono supportati e devi sempre utilizzare i segmenti da Target. Il termine AEM &quot;segmento&quot; equivale al termine Target &quot;pubblico&quot;.

   * **Libreria client:** questo valore predefinito è AT.js (mbox.js è obsoleto)

     >[!NOTE]
     >
     >Il file della libreria di Target, [AT.JS](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=it), è una nuova libreria di implementazione di Adobe Target progettata sia per le tipiche implementazioni web che per le applicazioni a pagina singola.
     >
     >mbox.js è stato dichiarato obsoleto e verrà rimosso in una fase successiva.
     >
     >Adobe consiglia di utilizzare AT.js invece di mbox.js come libreria client.
     >
     >AT.js offre diversi miglioramenti rispetto alla libreria mbox.js:
     >
     >* Tempi di caricamento delle pagine migliorati per le implementazioni web
     >* Maggiore sicurezza
     >* Migliori opzioni di implementazione per le applicazioni a pagina singola
     >* AT.js contiene i componenti inclusi in target.js, quindi non effettua più chiamate a target.js
     >
     >Puoi selezionare AT.js o mbox.js nel menu a discesa **Libreria client**.

   * **Utilizza Tag Management System per distribuire la libreria client**: seleziona questa opzione per utilizzare la libreria client da Adobe Launch o da un altro sistema di gestione tag (o DTM, che è obsoleto).

   * **AT.js personalizzato**: sfoglia per caricare il tuo AT.js personalizzato. Lascia vuoto per utilizzare la libreria predefinita.

     >[!NOTE]
     >
     >Per impostazione predefinita, quando scegli di accedere alla procedura guidata di configurazione di Adobe Target, il targeting accurato è abilitato.
     >
     >Il targeting accurato significa che la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Di conseguenza, in termini di prestazioni, un targeting accurato può creare un ritardo di alcuni millisecondi prima del caricamento del contenuto.
     >
     >Il targeting accurato è sempre abilitato nell’istanza di authoring. Tuttavia, nell’istanza di pubblicazione puoi scegliere di disattivare il targeting accurato a livello globale cancellando il segno di spunta accanto a Targeting accurato nella configurazione del servizio cloud (**http://localhost:4502/etc/cloudservices.html**). Puoi inoltre attivare e disattivare il targeting accurato per i singoli componenti indipendentemente dall’impostazione nella configurazione del servizio cloud.
     >
     >Se hai ***già*** creato i componenti di destinazione e modificato questa impostazione, le modifiche non influiscono su tali componenti. Devi apportare le modifiche direttamente a tali componenti.

1. Fai clic su **Connetti ad Adobe Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita**. Fai clic su **OK** sul messaggio e quindi **OK** nella finestra di dialogo.

### Aggiunta di un framework Target {#adding-a-target-framework}

<!-- Is this section needed? -->

Dopo aver impostato la configurazione cloud di Target, aggiungi un framework di Target. Il framework identifica i parametri predefiniti inviati ad Adobe Target dai componenti [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md). Target utilizza i parametri per determinare i segmenti che si applicano al contesto corrente.

Puoi creare più framework per una singola configurazione di Target. I framework multipli sono utili quando devi inviare un diverso set di parametri a Target per diverse sezioni del sito Web. Crea un framework per ogni set di parametri da inviare. Associa ogni sezione del sito Web al framework appropriato. Nota che una pagina web può utilizzare un solo framework alla volta.

1. Nella pagina di configurazione di Target, fai clic su **+** (segno più) accanto a Configurazioni disponibili.

1. Nella finestra di dialogo Crea framework, specifica un **Titolo**, seleziona **Framework Adobe Target** e fai clic su **Crea**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   Viene visualizzata la pagina framework. La barra laterale fornisce componenti che rappresentano informazioni provenienti da [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) che puoi mappare.

   <!-- ![Framework](assets/chlimage_1-162.png) -->

1. Trascina il componente ClientContext che rappresenta i dati da utilizzare per la mappatura sulla destinazione di rilascio. In alternativa, trascina il componente **Archivio ContextHub** nel framework.

   >[!NOTE]
   >
   >Durante la mappatura, i parametri vengono passati a una mbox tramite stringhe semplici. Non è possibile mappare array da ContextHub.

   Ad esempio, per utilizzare i **Dati profilo** relativi ai visitatori del sito per controllare la campagna di Adobe Target, trascina il componente **Dati profilo** nella pagina. Vengono visualizzate le variabili dei dati di profilo disponibili per la mappatura per i parametri di Adobe Target.

   <!-- ![Profile Data](assets/chlimage_1-163.png) -->

1. Seleziona le variabili da rendere visibili al sistema Adobe Target selezionando la casella di selezione **Condividi** nelle colonne appropriate.

   <!-- ![Share](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >La sincronizzazione dei parametri è solo unidirezionale, cioè da AEM ad Adobe Target.

Il framework viene creato. Per replicare il framework nell’istanza di pubblicazione, utilizza l’opzione **Attiva framework** dalla barra laterale.

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
1. Select **Edit**.
1. Select **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![Cloud Service Configuration](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Select **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which lets you publish it as well.
-->

## Esportazione di un frammento di esperienza in Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Per le risorse multimediali, come le immagini, viene esportato solo un riferimento in Target. La risorsa stessa rimane memorizzata in AEM Assets e viene distribuita dall’istanza di pubblicazione AEM.
>
>Per questo motivo è necessario pubblicare il frammento di esperienza con tutte le relative risorse prima di esportarlo in Target.

Per esportare un frammento di esperienza da AEM a Target (dopo aver specificato la configurazione cloud):

1. Passa alla console Frammenti di esperienza.
1. Seleziona il frammento di esperienza da esportare in Target.

   >[!NOTE]
   >
   >Deve essere una variante Web del frammento di esperienza.

1. Seleziona **Esporta in Adobe Target**.

   >[!NOTE]
   >
   >Se il frammento di esperienza è già stato esportato, seleziona **Aggiorna in Adobe Target**.

1. Seleziona **Esporta senza pubblicare** o **Pubblica** secondo necessità.

   >[!NOTE]
   >
   >Selezionando **Pubblica** pubblicherà immediatamente il frammento di esperienza e lo invierà in Target.

1. Seleziona **OK** nella finestra di dialogo di conferma.

   Il frammento di esperienza deve ora essere in Target.

   >[!NOTE]
   >
   >[Vari dettagli](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) dell&#39;esportazione sono visibili in **Vista a elenco** della console e **Proprietà**.

   >[!NOTE]
   >
   >Quando visualizzi un frammento di esperienza in Adobe Target, la data dell&#39;*ultima modifica* visualizzata è la data dell’ultima modifica apportata al frammento in AEM, non la data dell’ultima esportazione del frammento in Adobe Target.

>[!NOTE]
>
>In alternativa, è possibile eseguire l’esportazione dall’editor di pagine utilizzando comandi comparabili nel menu [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information).

## Utilizzo dei frammenti di esperienza in Adobe Target {#using-your-experience-fragments-in-adobe-target}

Dopo aver eseguito le attività precedenti, il frammento di esperienza viene visualizzato nella pagina Offerte di Target. Per scoprire come potrai usarlo, consulta la [documentazione specifica di Target](https://experiencecloud.adobe.com/resources/help/it_IT/target/target/aem-experience-fragments.html).

>[!NOTE]
>
>Quando visualizzi un frammento di esperienza in Adobe Target, la data dell&#39;*ultima modifica* visualizzata è la data dell’ultima modifica apportata al frammento in AEM, non la data dell’ultima esportazione del frammento in Adobe Target.

## Eliminazione di un frammento di esperienza già esportato in Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

L’eliminazione di un frammento di esperienza già esportato in Target potrebbe causare problemi se il frammento è già utilizzato in un’offerta in Target. L’eliminazione del frammento renderebbe l’offerta inutilizzabile mentre il contenuto del frammento è distribuito da AEM.

Per evitare tali situazioni:

* Se il frammento di esperienza non è attualmente utilizzato in un’attività, AEM consente all’utente di eliminarlo senza un messaggio di avviso.
* Se il frammento di esperienza è attualmente utilizzato da un’attività in Target, un messaggio di errore avvisa l’utente AEM delle possibili conseguenze che l’eliminazione del frammento avrà sull’attività.

  Il messaggio di errore in AEM non impedisce all’utente di (forzare) eliminare il frammento di esperienza. Se il frammento di esperienza viene eliminato:

   * L’offerta Target con il frammento di esperienza AEM può mostrare un comportamento indesiderato

      * L&#39;offerta sarà probabilmente ancora visualizzata, poiché l&#39;HTML del frammento di esperienza è stato inviato su Target
      * Eventuali riferimenti nel frammento di esperienza potrebbero non funzionare correttamente se le risorse di riferimento sono state eliminate anche in AEM.

   * Naturalmente, eventuali ulteriori modifiche al frammento di esperienza sono impossibili in quanto questo non esiste più in AEM.
