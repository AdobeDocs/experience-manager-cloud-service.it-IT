---
title: Come si crea il modello dati del modulo?
description: L’integrazione dei dati di Experience Manager Forms offre un’interfaccia utente intuitiva per la creazione e l’utilizzo dei modelli di dati dei moduli. Scopri come creare modelli di dati modulo con o senza origini dati configurate.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---

# Crea modello dati modulo {#create-form-data-model}

![Integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] l’integrazione dei dati fornisce un’interfaccia utente intuitiva per creare e utilizzare modelli di dati modulo. Un modello dati modulo si basa su origini dati per lo scambio di dati; tuttavia, è possibile creare un modello dati modulo con o senza un’origine dati. Esistono due approcci per creare un modello dati da a seconda che siano state configurate origini dati:

* **Utilizzo di origini dati preconfigurate**: Se hai configurato origini dati come descritto in [Configurare origini dati](configure-data-sources.md), è possibile selezionarli durante la creazione di un modello dati del modulo. Porta tutti gli oggetti, le proprietà e i servizi del modello dati dalle origini dati selezionate disponibili per l’uso nel modello dati del modulo.

* **Senza origini dati**: Se non sono state configurate origini dati per il modello dati del modulo, è comunque possibile crearlo senza origini dati. È possibile utilizzare il modello dati modulo per creare un Forms adattivo <!--and interactive communication--> e testarli utilizzando dati campione. Quando sono disponibili origini dati, è possibile eseguire un binding del modello dati del modulo con origini dati, che si riflettono automaticamente nel Forms adattivo associato<!--and interactive communications-->.

>[!NOTE]
>
>Devi essere membro di entrambi **fdm-author** e **form-user** gruppi per poter creare e utilizzare il modello dati del modulo. Contatta il tuo [!DNL Experience Manager] amministratore per diventare membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Verificare di aver configurato le origini dati che si desidera utilizzare nel modello dati modulo come descritto in [Configurare origini dati](configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, effettuare le seguenti operazioni:

1. In [!DNL Experience Manager] istanza autore, passa a **[!UICONTROL Forms > Integrazioni dati]**.
1. Tocca **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo :

   * Specificare un nome per il modello dati del modulo.
   * (**Facoltativo**) Specifica titolo, descrizione e tag per il modello dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate**) Tocca l’icona di spunta accanto a **[!UICONTROL Configurazione origine dati]** e seleziona il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che desideri utilizzare. Limita l’elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, qualsiasi database JDBC e [!DNL Experience Manager] le origini dati del profilo utente sono elencate per impostazione predefinita. Se non selezioni un nodo di configurazione, vengono elencate le origini dati da tutti i nodi di configurazione.

1. Tocca **[!UICONTROL Successivo]**.

1. (**Applicabile solo se le origini dati sono configurate**) **[!UICONTROL Seleziona origine dati]** in questa schermata sono elencate le eventuali origini dati disponibili. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Tocca **[!UICONTROL Crea]** e nella finestra di dialogo di conferma, tocca **[!UICONTROL Apri]** per aprire l’editor per modelli dati modulo.

   Esaminiamo i diversi componenti dell’interfaccia utente dell’Editor modelli dati per moduli.

   ![Un modello dati modulo con tre origini dati: un servizio RESTful, [!DNL Experience Manager] profilo utente e un RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Origini dati]** Elenca le origini dati in un modello dati modulo. Espandere un’origine dati per visualizzare gli oggetti e i servizi del modello dati corrispondente.

   B. **[!UICONTROL Aggiorna definizioni origine dati]** Recupera eventuali modifiche nelle definizioni dell’origine dati da origini dati configurate e le aggiorna nella scheda Origini dati dell’Editor modello dati modulo.

   C. **[!UICONTROL Modello]** Area contenuto in cui vengono visualizzati gli oggetti del modello dati aggiunti.

   D. **[!UICONTROL Servizi]** Area contenuto in cui vengono visualizzate operazioni o servizi di origine dati aggiunti.

   E. **[!UICONTROL Barra degli strumenti]** Strumenti per l’utilizzo del modello dati del modulo. La barra degli strumenti mostra più opzioni a seconda dell’oggetto selezionato nel modello dati del modulo.

   F. **[!UICONTROL Aggiungi selezionati]** Aggiunge oggetti e servizi del modello dati selezionati al modello dati del modulo.

Per ulteriori informazioni sull’editor di modelli dati modulo e su come utilizzarlo per modificare e configurare il modello dati modulo, consulta [Utilizzare il modello dati del modulo](work-with-form-data-model.md).

## Aggiorna origini dati {#update}

Per aggiungere o aggiornare origini dati a un modello dati modulo esistente, procedere come segue.

1. Vai a **[!UICONTROL Forms > Integrazioni dati]**, selezionare il Modello dati modulo in cui si desidera aggiungere o aggiornare le origini dati, quindi toccare **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati modulo, passare alla **[!UICONTROL Aggiorna origine]** scheda .

   In **[!UICONTROL Aggiorna origine]** scheda:

   * Tocca l’icona Sfoglia in **[!UICONTROL Configurazione in base al contesto]** e selezionare un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati che si desidera aggiungere. Se non selezioni un nodo, le configurazioni cloud risiedono solo nel `global` quando tocchi , vengono elencati i nodi **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, tocca **[!UICONTROL Aggiungi origini]** e selezionare le origini dati da aggiungere al modello dati del modulo. Tutte le origini dati configurate in `global` e viene visualizzato l&#39;eventuale nodo di configurazione selezionato.

   * Per sostituire un’origine dati esistente con un’altra origine dati dello stesso tipo, tocca **[!UICONTROL Modifica]** per l’origine dati e seleziona dall’elenco delle origini dati disponibili.
   * Per eliminare un’origine dati esistente, tocca **[!UICONTROL Elimina]** per l’origine dati. L’icona Elimina è disabilitata se un oggetto modello dati nell’origine dati viene aggiunto nel modello dati del modulo.

      ![proprietà fdm](assets/fdm-properties.png)

1. Tocca **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurarsi di aggiornare i riferimenti di binding, come appropriato, in Forms adattivo<!--and interactive communications--> che utilizzano il modello dati del modulo aggiornato.

## Passaggi successivi {#next-steps}

È ora disponibile un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti del modello dati, modificare le proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, consulta [Utilizzare il modello dati del modulo](work-with-form-data-model.md).
