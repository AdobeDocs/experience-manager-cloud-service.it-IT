---
title: Gestione dei tipi di pubblico
description: La console Pubblico consente di creare, organizzare e gestire i tipi di pubblico per il tuo account di Adobe Target o gestire segmenti per ContextHub
exl-id: dff72c15-afcd-4b16-a711-e9ca3010e3ec
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 87%

---

# Gestione dei tipi di pubblico{#managing-audiences}

La console Pubblico consente di creare, organizzare e gestire i tipi di pubblico per il tuo account di Adobe Target o gestire i segmenti per ContextHub:

* Aggiungere tipi di pubblico: tipi di pubblico Adobe Target o segmenti ContextHub.
* Gestisci tipi di pubblico.

Un tipo di pubblico, denominato *segmento* in ContextHub, è una classe di visitatori definita da criteri specifici che determinano chi visualizzerà un’attività sottoposta a targeting. Quando esegui il targeting di un’attività, puoi selezionare i tipi di pubblico direttamente nel processo di targeting oppure crearne di nuovi nella console Pubblico.

Nella console Pubblico, i tipi di pubblico sono organizzati per marchio.

I tipi di pubblico sono disponibili nella modalità Impostazione destinazione per [creare contenuti con destinazione](/help/sites-cloud/authoring/personalization/targeted-content.md), dove puoi anche creare dei tipi di pubblico (ma devi usare la console Pubblico per creare i tipi di pubblico per Adobe Target). I tipi di pubblico creati in modalità Targeting vengono visualizzati nella console Pubblico.

I tipi di pubblico vengono visualizzati con un’etichetta che descrive il tipo di pubblico definito:

* CH - Segmento ContextHub
* AT - Pubblico Adobe Target

## Creazione di un segmento ContextHub nella console Pubblico {#creating-a-contexthub-segment-in-the-audiences-console}

Puoi creare un segmento ContextHub nella console Pubblico o durante il processo di targeting.

Per creare un segmento ContextHub nella console Pubblico:

1. Nella console Navigazione, seleziona **Personalizzazione**. Seleziona **Tipi di pubblico**.
1. Seleziona **Crea segmento ContextHub**.

   ![Creazione di un segmento](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. Nella finestra di dialogo **Nuovo segmento ContextHub**, inserisci un titolo, regola l&#39;incremento e fai clic su **Crea**. Il nuovo segmento ContextHub appare nell’elenco dei tipi di pubblico.

   >[!NOTE]
   >
   >Per ordinare l’elenco modificato, tocca o fai clic su **Modificato** per ordinare in base all’ordine decrescente per visualizzare eventuali tipi di pubblico creati.

Per ulteriori dettagli sulla creazione di segmenti utilizzando ContextHub, consulta la documentazione Configurazione della segmentazione con ContextHub. <!--For further detail about creating segments using ContextHub, see [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md).-->

## Creazione di un pubblico di Adobe Target tramite la console Pubblico {#creating-an-adobe-target-audience-using-the-audience-console}

Puoi creare i tipi di pubblico di Adobe Target direttamente in AEM utilizzando la console Pubblico.

I tipi di pubblico sono definiti da regole che determinano chi è incluso in un’attività target. Una definizione di pubblico può includere più regole e ogni regola può includere più parametri.

Quando utilizzi più regole, queste vengono combinate tramite l&#39;operatore boolean AND, di conseguenza tutti i potenziali visitatori appartenenti al pubblico devono soddisfare tutte le condizioni definite per essere inclusi nell&#39;attività. Ad esempio, se definisci una regola per il sistema operativo AND una regola per il browser, verranno inclusi nell&#39;attività solo i visitatori che usano sia il sistema operativo sia il browser definiti nelle regole.

>[!NOTE]
>
>Se non vedi le voci **Crea pubblico Target** nel menu **Crea**, non disponi delle autorizzazioni necessarie per creare un pubblico. Per creare audience è necessario disporre di autorizzazioni di scrittura in `/etc/segmentation`. Per impostazione predefinita, gli autori dei contenuti del gruppo sono in possesso di autorizzazioni di scrittura.

Per creare un pubblico di Adobe Target:

1. Nella console Navigazione, seleziona **Personalizzazione**. Seleziona **Tipi di pubblico**.

   ![Navigazione ai tipi di pubblico](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. Nella console Pubblico, seleziona **Crea** e poi **Crea pubblico Target**.

   ![Creazione di un pubblico Target](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. In **Configurazione Adobe Target** , selezionare la configurazione di destinazione e selezionare **OK**.
1. Nell&#39;area Regola n. 1 selezionare il tipo di attributo e immettere le informazioni relative agli attributi nei campi disponibili. Al termine, seleziona il segno di spunta a destra dell’attributo per salvarlo. Per informazioni su tutti gli attributi, consulta [Attributi e relative opzioni](#attributes-and-their-options).
1. Fai clic su **Aggiungi regola** per aggiungere un’altra regola. Immetti tutte le regole necessarie. Le regole sono combinate con l’operatore boolean AND, il che significa che l’audience deve soddisfare tutti i requisiti di ciascuna regola per essere idonea a un’attività.
1. Seleziona **Avanti**.
1. Immetti un nome per il pubblico e seleziona **Salva**.
1. Seleziona **Salva**. Il pubblico è elencato nell’elenco Pubblico.

### Attributi e relative opzioni {#attributes-and-their-options}

Puoi creare regole di targeting per ciascuno dei seguenti attributi:

| **Attributo** | **Descrizione** | **Per ulteriori informazioni** |
|---|---|---|
| **Mobile** | Puoi indirizzare l’attività a chi usa specifici dispositivi mobili, in base a parametri come dispositivo mobile, tipo di dispositivo, fornitore, dimensioni dello schermo (in pixel) e altro ancora. | Consulta la [documentazione Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=it) in Adobe Target. |
| **Personalizzati** | I parametri personalizzati sono parametri mbox. Se passi dei parametri mbox alle mbox o se utilizzi la funzione targetPageParams, tali parametri vengono visualizzati qui per poter essere utilizzati nei tipi di pubblico. | Consulta la [documentazione sui parametri personalizzati](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=it) in Adobe Target. |
| **Sistema operativo** | Puoi eseguire il targeting dei visitatori che utilizzano un determinato sistema operativo. | Individua utenti che usano Linux, Macintosh, o Windows. |
| **Pagine del sito** | Puoi indirizzare l’attività ai visitatori che si trovano su una pagina specifica o con un parametro mbox specifico. | Consulta la [documentazione sulle pagine del sito](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=it) in Adobe Target. |
| **Browser** | Puoi eseguire il targeting degli utenti che usano un browser specifico o delle opzioni di browser specifiche quando visitano la tua pagina. | Consulta la [documentazione sulle opzioni del browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=it) in Adobe Target. |
| **Profilo visitatore** | Puoi indirizzare l’attività ai visitatori che soddisfano parametri di profilo specifici. | Consulta la [documentazione sul profilo del visitatore](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=it) in Adobe Target. |
| **Sorgenti di traffico** | Puoi indirizzare l’attività ai visitatori in base al motore di ricerca o alla pagina di destinazione che li rimanda al sito. | Consulta la [documentazione su Sorgenti di traffico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=it) in Adobe Target. |

## Modifica di un pubblico nella console Pubblico {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Puoi modificare solo i tipi di pubblico di Adobe Target creati nella stessa istanza AEM in cui stai modificando. Non è possibile modificare i tipi di pubblico di destinazione creati in ambienti AEM diversi.

Puoi modificare qualsiasi pubblico ContextHub dalla console Pubblico. Puoi modificare anche i tipi di pubblico di Adobe Target, ma solo quelli che sono stati creati in AEM:

1. Nella console Navigazione, seleziona **Personalizzazione**. Seleziona **Tipi di pubblico**.
1. Seleziona l’icona accanto al segmento ContextHub da modificare, quindi fai clic su **Modifica**.
1. Apporta le modifiche nell&#39;editor segmento. Per ulteriori informazioni, consulta la documentazione di ContextHub. <!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
