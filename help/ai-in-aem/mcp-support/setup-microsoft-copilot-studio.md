---
title: Configurazione di Microsoft Copilot Studio con AEM MCP
description: Scopri come configurare Microsoft Copilot Studio per la connessione ai server AEM MCP
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c8e96fe6-1a05-47c0-8215-0c28705e5e48
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Configurazione di Microsoft Copilot Studio con AEM MCP {#setup-microsoft-copilot-studio}

Segui questi passaggi per collegare Microsoft Copilot Studio ai server MCP di AEM.

>[!NOTE]
>
>L’interfaccia utente di Microsoft Copilot Studio è soggetta a modifiche e non è definitiva. Le presenti istruzioni sono a scopo illustrativo.

1. In **Agenti**, avvia il flusso per aggiungere un agente che utilizzerà gli strumenti MCP di AEM.

   * Crea un nuovo agente.

   ![Pannello Agenti in Microsoft Copilot Studio.](assets/copilot-1.png)

1. Apri l’area Strumenti per tale agente in modo da poter registrare la modalità di chiamata delle funzionalità esterne.

   * Passare alla sezione dello strumento e fare clic su **Aggiungi strumento**.

   ![Finestra di dialogo Aggiungi strumento in Microsoft Copilot Studio.](assets/copilot-2.png)

1. Decidere se riutilizzare un&#39;integrazione esistente o definire un nuovo strumento supportato da MCP.

   * Selezionate uno strumento esistente o createne uno nuovo.

   ![Selezione del protocollo di contesto del modello come tipo di strumento.](assets/copilot-3.png)

1. Quando si crea un nuovo strumento MCP, continuare con il passaggio del server **Model Context Protocol**, inclusa la modalità di anteprima quando viene visualizzata.

   * Configura un nuovo strumento MCP che punta a uno o più **URL** del server AEM MCP.

   ![Aggiunta di un server Model Context Protocol in modalità anteprima.](assets/copilot-4.png)

1. Definisci in che modo l’agente raggiunge questo endpoint MCP, specificando anche se l’accesso è condiviso o dedicato.

   * Stabilisci una connessione, che può essere **condivisa** o **dedicata** tra agenti.

   ![Finestra di dialogo per la creazione di una nuova connessione.](assets/copilot-5.png)

1. In **Aggiungi e configura**, fornisci o conferma i dettagli dello strumento MCP in modo che l&#39;agente possa raggiungere il tuo ambiente AEM.

   ![Pannello Aggiungi e configura per lo strumento MCP.](assets/copilot-6.png)

1. Termina i campi nel modulo dello strumento MCP (ad esempio, **URL** del server e opzioni relative all&#39;autenticazione).

   * In alternativa, abilitare **modalità di conferma automatica** o richiedere **conferma all&#39;utente finale** per tutte le interazioni dello strumento.

   ![Modulo di configurazione dello strumento MCP.](assets/copilot-7.png)

1. Convalida della connettività al server MCP; accesso completo basato su browser quando viene reindirizzato da Copilot Studio.

   * Effettua l&#39;accesso con il tuo **Adobe ID** quando reindirizzato.

   ![Verifica della connessione al server AEM MCP in corso.](assets/copilot-8.png)

1. Prima di eseguire un test, apri **Gestisci connessioni** (o **gestione connessione**) e assegna la connessione corretta alla sessione.

   * Durante il test dell&#39;agente, apri **gestione connessione** per assegnare una connessione alla sessione.

   ![Il pannello Gestione connessioni mostra le connessioni disponibili.](assets/copilot-9.png)

1. Nell’esperienza di test, esegui l’agente sulla connessione MCP di AEM.

   * Durante il test dell&#39;agente, premere **Riprova** dopo aver assegnato una connessione nella **gestione connessione**.

   ![Verifica dell&#39;agente con la connessione MCP di AEM.](assets/copilot-10.png)
