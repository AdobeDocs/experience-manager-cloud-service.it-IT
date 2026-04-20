---
title: Configurazione di Anthropic Claude con AEM MCP
description: Scopri come configurare Anthropic Claude per la connessione ai server AEM MCP
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2b90b2b2-cdd0-4f1e-890f-2f58f578face
source-git-commit: fede808fcd8b082a71273bf9ffceb48b5332f45d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Configurazione di Anthropic Claude con AEM MCP {#setup-claude}

Segui questi passaggi per collegare Anthropic Claude ai server MCP di AEM.

* Nella configurazione MCP di Claude, registra uno o più URL del server AEM MCP.
* Completa il flusso di accesso di Adobe.
* Se necessario, abilita la conferma automatica per alcuni strumenti nell’area di configurazione. Questa opzione è consigliata per le operazioni di ricerca o di sola lettura.
* Assicurati che il server MCP sia selezionato prima di avviare la conversazione.
* Chiedi a Claude di eseguire le attività relative ad AEM. Claude seleziona gli strumenti AEM esposti dal server MCP in base al prompt.

Per configurare Claude per AEM MCP, effettua le seguenti operazioni:

>[!NOTE]
>
>L’interfaccia utente di Claude è soggetta a modifiche e non è definitiva. Le presenti istruzioni sono a scopo illustrativo.

1. Apri il menu dell&#39;account nell&#39;angolo inferiore sinistro dell&#39;app Web Claude e scegli **Impostazioni** per aprire l&#39;area Impostazioni.

   ![Menu dell&#39;account in Claude con impostazioni selezionate.](assets/claude-1.png)

1. Nella barra laterale Impostazioni, seleziona **Connettori**. Nella pagina Connettori, scegli **Aggiungi connettore personalizzato** per registrare un endpoint MCP personalizzato.

   ![Pagina Connettori in Impostazioni con Aggiungi connettore personalizzato.](assets/claude-2.png)

1. Nella finestra di dialogo **Aggiungi connettore personalizzato**, immetti un nome visualizzato (ad esempio, **Servizio MCP contenuti AEM**) e l&#39;URL del server MCP AEM, quindi scegli **Aggiungi**. Utilizza **Impostazioni avanzate** solo quando la distribuzione richiede opzioni aggiuntive.

   ![Finestra di dialogo Aggiungi connettore personalizzato con nome e URL MCP.](assets/claude-3.png)

1. Nell&#39;elenco Connettori, individua la voce del connettore personalizzato (che mostra un&#39;etichetta **CUSTOM**) e scegli **Connect** per accedere e collegare il connettore all&#39;account Claude.

   ![Elenco dei connettori con Connect selezionato per il servizio MCP dei contenuti di AEM.](assets/claude-4.png)

1. Quando il connettore viene visualizzato nell&#39;elenco con il relativo URL, scegli **Configura** accanto a **Servizio MCP di contenuti AEM** per aprire i dettagli del connettore e continuare l&#39;installazione.

   ![Elenco dei connettori con Configurazione selezionata per il servizio AEM Content MCP.](assets/claude-5.png)

1. Nella pagina **Autorizzazioni dello strumento**, controlla il valore predefinito (ad esempio, **Richiede l&#39;approvazione**), quindi imposta ogni strumento di AEM su **Consenti sempre**, **Richiedi l&#39;autorizzazione** o **Non consentire mai** in base ai criteri di sicurezza.

   ![Autorizzazioni dello strumento per il servizio AEM Content MCP.](assets/claude-6.png)

1. Apri una conversazione. Seleziona il menu Strumenti e modello (icona cursori) a sinistra del campo del messaggio, abilita **AEM Content MCP Service** in Connectors, quindi immetti il messaggio in modo che Claude possa utilizzare gli strumenti MCP per quella chat.

   ![Compositore chat con AEM Content MCP Service abilitato nel menu Strumenti.](assets/claude-7.png)

## Connettore Adobe Experience Manager Claude {#aem-claude-connector}

Per installare il **connettore Adobe Experience Manager Claude**, apri **Impostazioni** > **Connettori** in Claude. Puoi anche aprire la pagina Connettori direttamente all&#39;indirizzo [https://claude.ai/settings/connectors](https://claude.ai/settings/connectors). Il connettore registra un server MCP che espone un set crescente di strumenti per i flussi di lavoro di AEM.

![Installazione di Adobe Experience Manager Claude Connector dalla directory dei connettori.](assets/claude-connector.png)