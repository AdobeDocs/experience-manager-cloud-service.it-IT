---
title: Configurazione di JetBrains con GitHub Copilot e AEM MCP
description: Scopri come configurare GitHub Copilot negli IDE JetBrains per la connessione ai server MCP di AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c5b46aff5b4ccffa60e8bebf7341935b435079e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 1%

---

# Configurazione di JetBrains con GitHub Copilot e AEM MCP {#setup-jetbrains-copilot}

Segui questi passaggi per collegare GitHub Copilot in un IDE JetBrains (come IntelliJ IDEA, WebStorm o PyCharm) ai server MCP di AEM.

1. Apri GitHub Copilot Chat nell&#39;IDE JetBrains facendo clic sull&#39;icona **GitHub Copilot Chat** sul lato destro dell&#39;editor.

   ![L&#39;IDE JetBrains con GitHub Copilot Chat aperto.](assets/jetbrains-copilot-1.png)

1. Fai clic sull&#39;icona **impostazioni** nel pannello Chat con copilot per aprire la configurazione MCP.

   ![Pannello Chat Copilot di GitHub con l&#39;icona delle impostazioni evidenziata.](assets/jetbrains-copilot-2.png)

1. In **Impostazioni**, passa a **Strumenti > Copilota GitHub > MCP (Model Context Protocol)** e fai clic su **Configura** per aprire il file di configurazione `mcp.json`.

   ![La finestra di dialogo Impostazioni JetBrains visualizza la configurazione MCP (Model Context Protocol) in GitHub Copilot.](assets/jetbrains-copilot-3.png)

1. Aggiungere uno o più URL del server AEM MCP al file `mcp.json`. Ad esempio:

   ```json
   {
     "servers": {
       "aem": {
         "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
       }
     }
   }
   ```


   ![Il file di configurazione mcp.json con l&#39;URL del server MCP di AEM.](assets/jetbrains-copilot-4.png)


1. Salva il file. Il Copilot GitHub rileva automaticamente la nuova configurazione del server e mostra un&#39;azione **Avvia**.

   ![Il file mcp.json che mostra il server AEM configurato con gli strumenti rilevati.](assets/jetbrains-copilot-5.png)

1. Fai clic sull&#39;azione **Inizio** e, quando richiesto, accedi con il tuo Adobe ID per completare il flusso di autenticazione.

1. Puoi rivedere e gestire gli strumenti individuati facendo clic sull&#39;indicatore **strumenti** che viene visualizzato nel pannello Chat copilota. Se necessario, attivare o disattivare singoli strumenti.


   ![La finestra di dialogo Configura strumenti mostra gli strumenti MCP di AEM disponibili.](assets/jetbrains-copilot-6.png)

1. Utilizza GitHub Copilot Chat per richiamare gli strumenti di AEM come parte dei flussi di lavoro di sviluppo o di contenuto.