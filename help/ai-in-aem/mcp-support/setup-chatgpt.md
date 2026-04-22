---
title: Configurazione di OpenAI ChatGPT con AEM MCP
description: Scopri come configurare OpenAI ChatGPT per la connessione ai server MCP di AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Configurazione di OpenAI ChatGPT con AEM MCP {#setup-chatgpt}

Segui questi passaggi per collegare OpenAI ChatGPT ai server MCP di AEM.

* Aggiungi uno o più URL del server AEM MCP nell’area in cui sono configurati le connessioni o gli strumenti MCP.
* Attiva la connessione e accedi con il tuo Adobe ID quando viene reindirizzato.
* In una chat, fai riferimento agli strumenti di AEM configurati nelle tue richieste, ad esempio:

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

>[!NOTE]
>
>L&#39;interfaccia utente di OpenAI ChatGPT è soggetta a modifiche e non è definitiva. Le presenti istruzioni sono a scopo illustrativo.

1. Apri **Impostazioni** in modo da poter raggiungere l&#39;area in cui sono configurati gli strumenti o le connessioni MCP.

   ![Finestra di dialogo Impostazioni ChatGPT.](assets/chatgpt-1.png)

1. In **App e connettori**, apri **Impostazioni avanzate** per gestire il connettore e le opzioni relative a MCP.

   ![Pannello Impostazioni avanzate app e connettori in ChatGPT.](assets/chatgpt-2.png)

1. Abilita la **modalità sviluppatore** in **App e connettori** per aggiungere e configurare app o connettori personalizzati.

   ![Abilitazione della modalità Sviluppatore nella sezione App e connettori.](assets/chatgpt-3.png)

1. Avvia **Crea nuova app** (o controllo equivalente) per aggiungere una voce di app per il server MCP di AEM.

   ![Finestra di dialogo per la creazione di una nuova app in ChatGPT.](assets/chatgpt-4.png)

1. Completa il modulo **Nuova app**, ad esempio denomina l&#39;app e immetti l&#39;URL del server AEM MCP e tutti gli altri campi obbligatori, quindi **Salva**.

   ![Modulo di configurazione nuova app in ChatGPT.](assets/chatgpt-5.png)

1. Conferma che il servizio **AEM Content MCP** (o l&#39;app configurata) sia presente in **App e connettori** in modo che ChatGPT possa utilizzarlo.

   ![Il servizio AEM Content MCP elencato in App e connettori.](assets/chatgpt-6.png)

1. In una chat, scrivi un messaggio che indica a ChatGPT di utilizzare gli **strumenti AEM** configurati (ad esempio, per eseguire query sul contenuto o sui siti dell&#39;autore).

   ![Richiesta a ChatGPT di utilizzare il servizio MCP dei contenuti di AEM.](assets/chatgpt-7.png)
