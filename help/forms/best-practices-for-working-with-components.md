---
title: Best practice per l’utilizzo dei componenti
seo-title: Best practices for working with components
description: Alcune best practice e punti chiave da ricordare quando si lavora con i componenti per moduli adattivi
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Best practice per l’utilizzo dei componenti{#best-practices-for-working-with-components}

Alcune best practice e punti chiave da tenere a mente quando si utilizzano i componenti per moduli adattivi sono i seguenti:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, tocca il componente e tocca ![proprietà](assets/Smock_Wrench_18_N.svg) per aprire le proprietà del componente nel browser Proprietà.
* Un componente viene identificato con il suo nome elemento. Quando tocchi ![proprietà](assets/Smock_Wrench_18_N.svg), puoi modificare il nome del componente modificando il **[!UICONTROL Nome elemento]** nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e caratteri di sottolineatura (_). Altri caratteri speciali non sono consentiti e il nome dell’elemento deve iniziare con una lettera.

* È possibile modificare la proprietà Titolo di un componente Modulo adattivo in linea nell’editor dei moduli senza aprire il browser Proprietà, purché il titolo sia visibile sul modulo. Per eseguire questa operazione:

   1. Tocca per selezionare un componente con una **[!UICONTROL Titolo]** di cui **[!UICONTROL Nascondi titolo]** la proprietà è disabilitata.

   1. Tocca ![Icona Modifica](assets/Smock_Edit_18_N.svg) per rendere modificabile il titolo.

   1. Modifica il titolo e tocca il tasto Invio oppure tocca un punto qualsiasi all’esterno del componente per salvare le modifiche. Tocca il tasto Esc per eliminare le modifiche.

* Alcuni componenti per moduli adattivi come e-mail e telefono includono pattern di convalida predefiniti. Tuttavia, è possibile specificare una convalida personalizzata aggiornando la **[!UICONTROL Pattern di convalida]** sotto il pannello a soffietto Pattern nelle proprietà del componente. Per ulteriori informazioni sulle convalide predefinite, consulta le descrizioni dei componenti nella tabella precedente.

* I campi Forms adattivi, come Numeric Box e Email, possono essere configurati per includere tipi di input HTML5 specializzati. Quando questi campi sono concentrati su dispositivi mobili e tablet, il tastierino mostra in primo piano un alfabeto, numeri e caratteri specifici comunemente utilizzati per inserire informazioni nei campi. Consente agli utenti di immettere le informazioni rapidamente senza dover alternare tra i set di caratteri sul tastierino. Per consentire un input specializzato per un componente, abilita la **[!UICONTROL Usa numero tipo HTML]** casella di controllo nelle relative proprietà dei componenti.

* È possibile abilitare un componente Casella di testo per accettare il testo RTF. Per abilitare il testo RTF per una casella di testo, attivare la **[!UICONTROL Consenti RTF]** nelle proprietà del componente.

* È possibile abilitare i componenti Casella di testo, E-mail e Telefono per la compilazione automatica dei valori per campi quali nome, indirizzo, carta di credito, telefono ed e-mail dalle informazioni memorizzate nelle impostazioni di compilazione automatica del browser. Per abilitare questa funzione, seleziona **[!UICONTROL Abilita riempimento automatico]** nelle proprietà del componente e seleziona un **[!UICONTROL Attributo di riempimento automatico]**. Quando un utente compila un modulo adattivo, i valori vengono suggeriti dal profilo di compilazione automatica nel browser o in base ai valori precedentemente compilati dall’utente. La compilazione automatica funziona se le impostazioni di compilazione automatica nel browser dell’utente sono attivate.

* Specificare i valori per gli elementi Pulsante di scelta e Casella di controllo in `{value}={text}` nelle proprietà del componente.
* Il componente File allegato, per impostazione predefinita, consente a un utente di allegare un solo file. Tuttavia, è possibile configurare le proprietà del componente per supportare più allegati. Inoltre, se un utente allega più file con lo stesso nome file, gli allegati possono causare alcuni problemi. Pertanto, è consigliabile associare un identificatore univoco per ciascun allegato inviato all’invio del modulo. Per eseguire questa operazione:

   1. Sul tuo [!DNL AEM Forms] server, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
   1. Trova e tocca **[!UICONTROL Servizio di configurazione Forms adattivo]**.
   1. Nella finestra di dialogo Servizio di configurazione Forms adattivo, abilita **[!UICONTROL Rendi univoci i nomi dei file]**. Per impostazione predefinita, è disabilitata.

* Per consentire agli utenti di allegare un PDF tramite il browser Safari, assicurati che **application/pdf** viene aggiunto alla proprietà Tipi di file supportati del componente File allegato. Forms adattivo creato con precedente [!DNL AEM Forms] la versione può contenere **.pdf** anziché **application/pdf** nella proprietà Tipi di file supportati .

>[!NOTE]
>
>I componenti per modulo adattivo non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.