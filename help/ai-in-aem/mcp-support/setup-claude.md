---
title: Configurazione di Anthropic Claude con AEM MCP
description: Scopri come configurare Anthropic Claude per la connessione ai server MCP di AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2b90b2b2-cdd0-4f1e-890f-2f58f578face
source-git-commit: 07a7aa5f02d7bfa992df825f3b8a19e18d569d5b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Configurazione di Anthropic Claude con AEM MCP {#setup-claude}

Questo articolo tratta due diversi modi per utilizzare Anthropic Claude con AEM:

- Configurare manualmente uno o più server MCP di AEM in Claude (i server descritti in [Utilizzo di MCP con AEM as a Cloud Service — Server MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md#mcp-servers)).
- Installa il connettore Adobe Experience Manager dal marketplace dei connettori di Anthropic. Attualmente ha parità di funzioni con Content MCP Server e presenterà un sottoinsieme crescente di strumenti disponibili nei server MCP di AEM.



## Configurare manualmente i server MCP di AEM in Claude {#manual-configure-aems-mcp-servers-in-claude}

Questa sezione descrive l&#39;approccio **configurazione manuale**, in cui puoi aggiungere uno o più server MCP di AEM a Claude come connettori personalizzati.

>[!NOTE]
>
>L’interfaccia utente di Claude è soggetta a modifiche e non è definitiva. Le presenti istruzioni sono a scopo illustrativo.

1. Apri il menu dell&#39;account nell&#39;angolo inferiore sinistro dell&#39;app Web Claude e scegli **Impostazioni** per aprire l&#39;area Impostazioni.

   ![Menu dell&#39;account in Claude con impostazioni selezionate.](assets/claude-1.png)

1. Nella barra laterale Impostazioni, seleziona **Connettori**. Nella pagina Connettori, scegli **Aggiungi connettore personalizzato** per registrare un endpoint MCP personalizzato.

   ![Pagina Connettori in Impostazioni con Aggiungi connettore personalizzato.](assets/claude-2.png)

1. Nella finestra di dialogo **Aggiungi connettore personalizzato**, immetti un nome visualizzato (ad esempio, **Servizio MCP di contenuti AEM**) e l&#39;URL del server MCP, quindi scegli **Aggiungi**. Utilizza **Impostazioni avanzate** solo quando la distribuzione richiede opzioni aggiuntive.

   ![Finestra di dialogo Aggiungi connettore personalizzato con nome e URL MCP.](assets/claude-3.png)

1. Nell&#39;elenco Connettori, individua la voce del connettore personalizzato (che mostra un&#39;etichetta **CUSTOM**) e scegli **Connect** per accedere e collegare il connettore all&#39;account Claude.

   ![Elenco dei connettori con Connect selezionato per il servizio MCP dei contenuti di AEM.](assets/claude-4.png)

1. Quando il connettore viene visualizzato nell&#39;elenco con il relativo URL, scegli **Configura** accanto a **Servizio MCP di contenuti AEM** per aprire i dettagli del connettore e continuare l&#39;installazione.

   ![Elenco dei connettori con Configurazione selezionata per il servizio AEM Content MCP.](assets/claude-5.png)

1. Nella pagina **Autorizzazioni dello strumento**, controlla il valore predefinito (ad esempio, **Richiede l&#39;approvazione**), quindi imposta ogni strumento di AEM su **Consenti sempre**, **Richiedi l&#39;autorizzazione** o **Non consentire mai** in base ai criteri di sicurezza.

   ![Autorizzazioni dello strumento per il servizio AEM Content MCP.](assets/claude-6.png)

1. Apri una conversazione. Seleziona il menu Strumenti e modello (icona cursori) a sinistra del campo del messaggio, abilita **AEM Content MCP Service** in Connectors, quindi immetti il messaggio in modo che Claude possa utilizzare gli strumenti MCP per quella chat.

   ![Compositore chat con AEM Content MCP Service abilitato nel menu Strumenti.](assets/claude-7.png)

## Installare il connettore Adobe Experience Manager (Anthropic Connector Marketplace) {#install-adobe-experience-manager-connector}

Questa sezione descrive il **connettore installabile** dal marketplace del connettore di Anthropic (anziché aggiungere un URL del connettore personalizzato). Include un sottoinsieme degli strumenti disponibili nei server MCP di AEM.

Per installare il **Connettore Adobe Experience Manager**, apri **Impostazioni** > **Connettori** in Claude. Puoi anche aprire la pagina Connettori direttamente all&#39;indirizzo [https://claude.ai/settings/connectors](https://claude.ai/settings/connectors). Il connettore registra un server MCP che espone un set crescente di strumenti per i flussi di lavoro di AEM.

![Installazione di Adobe Experience Manager Claude Connector dalla directory dei connettori.](assets/claude-connector.png)