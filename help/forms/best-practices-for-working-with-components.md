---
title: Best practice per l’utilizzo dei componenti
seo-title: Best practices for working with components
description: Alcune best practice e punti chiave da ricordare quando si lavora con componenti di moduli adattivi
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---


# Best practice per l’utilizzo dei componenti{#best-practices-for-working-with-components}

Di seguito sono riportate alcune best practice e punti chiave da tenere a mente quando si lavora con componenti di moduli adattivi:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, tocca il componente e tocca ![proprietà](assets/Smock_Wrench_18_N.svg) per aprire le proprietà del componente nel browser Proprietà.
* Un componente è identificato dal relativo nome elemento. Quando tocchi ![proprietà](assets/Smock_Wrench_18_N.svg), è possibile modificare il nome del componente cambiando il **[!UICONTROL Nome elemento]** valore del campo nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e trattini bassi (_). Non sono consentiti altri caratteri speciali e il nome dell’elemento deve iniziare con una lettera.

* Puoi modificare la proprietà Title di un componente Modulo adattivo in linea nell’editor di moduli senza aprire il browser Properties (Proprietà), purché il titolo sia visibile nel modulo. Per eseguire questa operazione:

   1. Tocca per selezionare un componente che ha **[!UICONTROL Titolo]** proprietà e il cui **[!UICONTROL Nascondi titolo]** è disabilitata.

   1. Tocca ![Icona Modifica](assets/Smock_Edit_18_N.svg) per rendere modificabile il titolo.

   1. Modifica il titolo e tocca Ritorna o tocca un punto qualsiasi all’esterno del componente per salvare le modifiche. Toccare il tasto Esc per ignorare le modifiche.

* Alcuni componenti del modulo adattivo, come e-mail e telefono, includono modelli di convalida predefiniti. Tuttavia, puoi specificare la convalida personalizzata aggiornando il **[!UICONTROL Pattern di convalida]** sotto il pannello a soffietto Patterns nelle proprietà del componente. Per ulteriori informazioni sulle convalide predefinite, consulta le descrizioni dei componenti nella tabella precedente.

* I campi Forms adattivi, come Casella numerica e E-mail, possono essere configurati per includere tipi di input HTML5 specializzati. Quando questi campi sono attivati su dispositivi mobili e tablet, il tastierino mostra in anticipo caratteri, numeri e caratteri specifici che vengono comunemente utilizzati per immettere informazioni nei campi. Consente agli utenti di immettere rapidamente le informazioni senza dover passare da un set di caratteri all’altro sul tastierino. Per consentire l&#39;input specializzato di un componente, attivare **[!UICONTROL Usa numero tipo HTML]** nelle proprietà dei componenti.

* È possibile abilitare un componente Casella di testo per accettare il testo RTF. Per abilitare il testo RTF per una casella di testo, attivare **[!UICONTROL Consenti formato Rich Text]** nelle proprietà del componente.

* È possibile abilitare i componenti Casella di testo, E-mail e Telefono per riempire automaticamente i valori di campi come nome, indirizzo, carta di credito, telefono ed e-mail dalle informazioni memorizzate nelle impostazioni di riempimento automatico del browser. Per abilitare questa funzione, seleziona **[!UICONTROL Abilita riempimento automatico]** nelle proprietà del componente e seleziona una **[!UICONTROL Attributo riempimento automatico]**. Quando un utente compila un modulo adattivo, i valori vengono suggeriti dal profilo di riempimento automatico nel browser o in base ai valori precedentemente compilati dall’utente. Il riempimento automatico funziona se le impostazioni di riempimento automatico nel browser dell’utente sono attivate.

* Specificare i valori per gli elementi Pulsante di opzione e Casella di controllo in `{value}={text}` nelle proprietà del componente.
* Per impostazione predefinita, il componente File allegato consente di allegare un solo file. Tuttavia, è possibile configurare le proprietà del componente per supportare più allegati. Inoltre, se un utente allega più file con lo stesso nome file, gli allegati possono causare alcuni problemi. Pertanto, si consiglia di associare un identificatore univoco per ogni allegato inviato al momento dell’invio del modulo. Per eseguire questa operazione:

   1. Sul tuo [!DNL AEM Forms] server, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
   1. Trova e tocca **[!UICONTROL Servizio di configurazione Forms adattivo]**.
   1. Nella finestra di dialogo Servizio di configurazione di Forms adattivo, abilita **[!UICONTROL Imposta nomi file univoci]**. Per impostazione predefinita, è disabilitato.

* Per consentire agli utenti di collegare un PDF tramite il browser Safari, assicurati che **application/pdf** viene aggiunta alla proprietà Tipi di file supportati del componente File allegato. Forms adattivo creato con precedente [!DNL AEM Forms] versione può contenere **.pdf** invece di **application/pdf** nella proprietà Tipi di file supportati.

>[!NOTE]
>
>I componenti per moduli adattivi non supportano le lingue da destra a sinistra (RTL). Ad esempio, ebraico.