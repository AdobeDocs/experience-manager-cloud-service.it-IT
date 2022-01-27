---
title: Esportazione di frammenti esperienza in Adobe Target
description: Esportazione di frammenti esperienza in Adobe Target
source-git-commit: 4b83fdbe4c0c260a609734b3c460ce884f0c8c9e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---

# Esportazione di frammenti esperienza in Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* I frammenti esperienza AEM vengono esportati nell’area di lavoro predefinita di Adobe Target.
>* AEM deve essere integrato con Adobe Target secondo le istruzioni di cui [Integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).


Puoi esportare [Frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md), creato in Adobe Experience Manager as a Cloud Service (AEM), in Adobe Target (Target). Possono quindi essere utilizzati come offerte nelle attività di Target, per testare e personalizzare le esperienze su larga scala.

Sono disponibili tre opzioni di formato per esportare un frammento esperienza in Adobe Target:

* HTML (predefinito): Supporto per la distribuzione di contenuti web e ibridi
* JSON: Supporto per la distribuzione di contenuti headless
* HTML e JSON

Dopo [Integrazione con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) AEM Frammenti esperienza possono essere esportati nell’area di lavoro predefinita in Adobe Target o in aree di lavoro definite dall’utente per Adobe Target.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target non esistono in Adobe Target. Vengono definiti e gestiti in Adobe IMS (Identity Management System), quindi selezionati per l’utilizzo tra le soluzioni utilizzando le integrazioni Adobe I/O.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target possono essere utilizzate per consentire ai membri di un&#39;organizzazione (gruppo) di creare e gestire offerte e attività solo per questa organizzazione; senza dare accesso ad altri utenti. Ad esempio, organizzazioni specifiche per paese nell&#39;ambito di una preoccupazione globale.

>[!NOTE]
>
>Per ulteriori informazioni, consulta anche:
>
>* [Sviluppo Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componenti core - Frammenti esperienza](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
>* [Adobe Target - Come Si Utilizzano I Frammenti Esperienza Adobe Experience Manager (AEM)?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)


## Prerequisiti {#prerequisites}


Sono necessarie diverse azioni:

1. Devi [integrare AEM con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).
2. I frammenti esperienza vengono esportati dall’istanza di authoring AEM, per cui devi [Configurare AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) nell’istanza di authoring, per garantire che tutti i riferimenti all’interno del frammento esperienza siano esternalizzati per la distribuzione web.

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
   >
   >Se aggiungi la configurazione cloud al frammento esperienza stesso, questa viene ereditata da tutte le varianti.

1. Seleziona la **Cloud Services** scheda .

1. Sotto **Configurazione Cloud Service**, seleziona **Adobe Target** dall’elenco a discesa.

   >[!NOTE]
   >
   >È possibile personalizzare il formato JSON di un’offerta Frammento esperienza. A questo scopo, definisci un componente Frammento esperienza cliente e poi annota come esportare le sue proprietà nel modello Sling del componente.
   >
   >Consulta il componente core :
   >
   >[Componenti core - Frammenti esperienza](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   Sotto **Adobe Target** seleziona:

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

<!--
   For example, for a folder:

   ![Folder - Cloud Services](assets/xf-target-integration-01.png "Folder - Cloud Services")
-->

1. **Salva e chiudi**.

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
