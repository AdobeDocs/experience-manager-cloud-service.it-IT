---
title: Configurazione dell’integrazione di AI Translation
description: Scopri come collegare Adobe Experience Manager ad Azure OpenAI per la traduzione automatica utilizzando i servizi cloud di traduzione e il Translation Integration Framework.
feature: Language Copy
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="Si applica ad AEM Sites)."
solution: Experience Manager Sites
source-git-commit: cb7dcc07a5913d6c7e88e0eec03f0003f1e3997a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Configurazione dell’integrazione di AI Translation {#ai-translation-integration}

L&#39;integrazione della traduzione basata su IA consente di utilizzare un **modello di linguaggio di grandi dimensioni (LLM)** come servizio di traduzione per i contenuti creati in Adobe Experience Manager. Connetti AEM al tuo provider LLM (a partire da Microsoft Azure OpenAI), riutilizza gli stessi [flussi di lavoro di traduzione](/help/sites-cloud/administering/translation/overview.md) come per altri connettori e, facoltativamente, carica **guide stile di traduzione** in modo che AEM possa generare regole che mantengano il tono, la terminologia e il linguaggio del brand coerenti tra le diverse lingue.

Per informazioni di base sui progetti di traduzione, sulle configurazioni cloud e sul framework di integrazione della traduzione, consulta [Traduzione di contenuti per siti multilingue](overview.md) e [Configurazione del framework di integrazione della traduzione](integration-framework.md).

## Integrazione della traduzione basata su intelligenza artificiale in AEM {#how-ai-translation-fits-in-aem}

I modelli di linguaggio di grandi dimensioni possono tradurre passaggi completi con attenzione al contesto, al tono e agli idiomi piuttosto che alla sostituzione letterale parola per parola. Quando configuri l&#39;integrazione di traduzione AI, LLM funge da **servizio di traduzione di terze parti** allo stesso modo degli altri provider a cui ti connetti tramite AEM. Fornisci la tua **licenza e le tue credenziali** per il servizio LLM.

Il supporto iniziale connette AEM a **Azure OpenAI**. Adobe prevede di aggiungere il supporto per ulteriori provider in una versione successiva.

Puoi configurare sia la connessione LLM che le guide di stile opzionali in **Servizi cloud di traduzione**, insieme alle altre configurazioni di traduzione. Puoi utilizzare diversi servizi di traduzione per diverse [configurazioni cloud](/help/sites-cloud/administering/translation/integration-framework.md#creating-a-translation-integration-configuration); ad esempio, una configurazione può utilizzare la traduzione basata su IA mentre un&#39;altra utilizza un connettore di traduzione automatica tradizionale.

## Configurazione dei servizi cloud di traduzione {#configure-translation-cloud-services}

Configura la traduzione AI nella stessa area in cui gestisci altre configurazioni cloud per la traduzione.

1. Nel [menu di navigazione globale](/help/sites-cloud/authoring/basic-handling.md#global-navigation), seleziona **Strumenti** > **Servizi cloud** > **Servizi cloud di traduzione**.
1. Aprire o creare la configurazione in cui si desidera abilitare la traduzione AI (incluso `/conf/global` se la funzionalità deve essere applicata in modo ampio).

![La console Servizi cloud di traduzione mostra dove vengono gestite le configurazioni di traduzione.](assets/ai-translation-integration/aem_ai-translation_translation-cloud-services.png)

## Configurazione della connessione LLM {#configure-the-llm-connection}

L&#39;esperienza **Configurazione traduzione agente** include una sezione **Configurazione LLM** in cui è possibile connettere il provider.

1. Apri la configurazione di traduzione AI per la voce dei servizi cloud di traduzione.
1. Seleziona **[!UICONTROL Configurazione LLM]**.
1. Scegli il tuo provider (ad esempio, **Azure OpenAI**).
1. Immetti le credenziali e i dettagli dell&#39;endpoint richiesti per la sottoscrizione (**Chiave API**, **Versione API**, **Percorso base**, **Nome distribuzione** e tutti gli altri campi richiesti dal provider).
1. Salva la configurazione.

![Schermata Configurazione traduzione agente con scheda Configurazione LLM e campi OpenAI di Azure.](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-config.png)

## Aggiunta di guide allo stile di traduzione e regole generate {#add-translation-style-guides-and-generated-rules}

Puoi caricare **documenti della guida allo stile di traduzione** (in genere uno per lingua di destinazione). AEM analizza ogni guida e genera **regole di traduzione** per allineare l&#39;output alle aspettative del tuo marchio e linguistiche.

1. In **Configurazione traduzione agente**, selezionare **[!UICONTROL Linee guida LLM]**.
1. Scegliere una lingua e utilizzare **[!UICONTROL Carica]** per aggiungere un documento di guida di stile per tale lingua.
1. Mentre AEM elabora una guida, un indicatore di stato mostra lo stato di avanzamento (**elaborazione**, **completato** o **interrotto**).
1. Rivedi o modifica le regole generate nell’editor (ad esempio, JSON che acquisisce il tono, la terminologia e gli esempi).

![Scheda Linee guida LLM che mostra l&#39;elenco delle impostazioni locali e le regole di traduzione generate per una lingua selezionata.](assets/ai-translation-integration/aem_ai-translation_agentic-translation-llm-guidelines.png)

## Impostazione del metodo di traduzione predefinito nel framework {#set-the-default-translation-method-in-the-framework}

Dopo il salvataggio della configurazione cloud, registra **traduzione agente** come comportamento predefinito nella configurazione [Framework di integrazione della traduzione](integration-framework.md) quando crei progetti di traduzione. Se necessario, puoi modificare il metodo per progetto.

![Scheda Siti framework integrazione traduzione che mostra le opzioni del metodo di traduzione, inclusa la traduzione automatica.](assets/ai-translation-integration/aem_ai-translation_translation-integration-framework-default.png)

## Esecuzione di progetti di traduzione {#run-translation-projects}

Una volta configurata e associata la traduzione AI alle tue pagine, [crea ed esegui progetti di traduzione](managing-projects.md) nello stesso modo in cui avviene con altri provider di traduzione. Il contenuto di pagine, frammenti di contenuto e risorse segue le regole di traduzione e le impostazioni del framework.

>[!NOTE]
>
>L&#39;integrazione della traduzione basata su IA è **non** disponibile dall&#39;Assistente [IA nell&#39;interfaccia utente di Adobe Experience Manager](/help/implementing/cloud-manager/ai-assistant-in-aem.md) o dall&#39;interfaccia dell&#39;agente di produzione di Experience. Utilizza i flussi di lavoro e le console di traduzione descritti in questo articolo.

