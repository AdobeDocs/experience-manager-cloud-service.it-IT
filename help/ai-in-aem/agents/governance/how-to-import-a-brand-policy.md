---
title: Importare un criterio per i marchi
description: Utilizzare Adobe Governance Agent per importare un criterio per il marchio
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 94d671ebbd5aeb5992fdbc9d779ffbca51f82585
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# Importare un criterio per i marchi {#how-to-import-a-brand-policy}

## Panoramica {#overview}

Una politica del brand definisce regole, standard e vincoli che garantiscono che tutti i contenuti prodotti o aggiornati da Adobe Experience Manager rimangano coerenti con l’identità del brand di un’azienda. Questo include tipicamente il tono della voce, la terminologia, le linee guida visive e le regole editoriali.

L’agente di governance utilizza i criteri del marchio come fonte di verità per analizzare le pagine esistenti e guidare la generazione di contenuti. I clienti possono fornire i propri criteri del marchio originali, che l’agente di governance converte automaticamente in controlli dei criteri leggibili dall’intelligenza artificiale. Questi controlli vengono quindi utilizzati per convalidare i contenuti e fornire all’agente di produzione un framework affidabile e applicabile per generare o aggiornare le pagine che rimangono allineate con il brand.

## Che cos’è un Brand Policy nell’agente di governance {#what-is-a-brand-policy-in-the-governance-agent}

Nel contesto dell’agente di governance, una politica del brand è una rappresentazione strutturata delle regole del brand che può essere compresa e applicata dall’intelligenza artificiale. Invece di richiedere ai clienti di riscrivere le linee guida in un formato tecnico, l’agente di governance accetta le politiche del brand nella loro forma originale (ad esempio documenti, linee guida o descrizioni di regole).

Una volta importato, il criterio viene trasformato in un set di controlli dei criteri di IA che possono:

* Analizza le pagine esistenti per rilevare le incoerenze del brand
* Contrassegna le deviazioni dal tono, dalla terminologia o dalle regole obbligatorie
* Fornire indicazioni chiare agli agenti a valle
* Assicurati che il contenuto generato o aggiornato rimanga conforme al brand fin dalla progettazione

Questo approccio consente ai team di riutilizzare la documentazione esistente del marchio, beneficiando al contempo di governance automatizzata e produzione scalabile di contenuti.

## Utilizzo dei criteri per i marchi {#how-brand-policies-are-used}

Dopo l’importazione di un criterio del marchio:

* L’agente di governance interpreta e normalizza il criterio in controlli di intelligenza artificiale applicabili
* Le pagine possono essere analizzate in base alla policy per identificare lacune o violazioni
* L’agente di produzione utilizza questi controlli come vincoli durante la generazione o l’aggiornamento del contenuto
* La conformità del brand diventa coerente, ripetibile e verificabile tra siti e team


## Importare un criterio per i marchi {#import-a-brand-policy}

Per importare un brand nell’agente di governance:

1. Crea un marchio, assegnando un nome e un dominio principale. Per eseguire questa operazione, fai clic sul pulsante **Contesto di governance** nella navigazione a sinistra nella tua Experience Manager home, quindi premi il pulsante **+ Aggiungi marchio**, come illustrato di seguito:

   ![Aggiunta di un nuovo brand](/help/ai-in-aem/agents/governance/assets/add_brand.png){width="70%"}

1. Imposta il nome del brand e una descrizione nella finestra seguente

   ![Denominazione del marchio](/help/ai-in-aem/agents/governance/assets/add_brand_dialogue.png){width="60%"}

1. I nuovi brand vengono creati in stato di bozza. Assicurati di impostare il nuovo brand creato su Attivo, facendo clic sulla scheda del brand, premendo il tasto di modifica (matita) nell&#39;angolo in alto a destra dello schermo, imposta **Stato** su **Attivo** nella finestra seguente e fai clic su **Salva modifiche**. Devi abilitare i brand impostandoli su Attivi prima di poterli utilizzare.

   ![Imposta lo stato del brand su Attivo](/help/ai-in-aem/agents/governance/assets/set_brand_active.png){width="60%"}

1. Una volta creato il brand, crea un dominio principale nella seguente finestra premendo il collegamento **Domini** a sinistra:

   ![Configurazione di un dominio per il brand](/help/ai-in-aem/agents/governance/assets/add_domain.png)

   >[!IMPORTANT]
   >
   >Proprio come i nuovi marchi, i nuovi domini vengono creati con lo stato Bozza predefinito. Per cambiare le impostazioni, vai al tuo marchio, fai clic su **Domini**, quindi modifica il dominio utilizzando l&#39;icona a forma di matita e imposta il suo stato su **Attivo**.

1. Dopo aver configurato il dominio principale, puoi caricare il documento sui criteri del brand visitando **Criteri** nell&#39;angolo superiore sinistro della finestra e premendo il pulsante **+ Aggiungi criterio**.

   ![Aggiunta di un criterio dalla scheda marchio](/help/ai-in-aem/agents/governance/assets/add_policy_treeview.png)

   >[!NOTE]
   >
   >In alternativa, è possibile aggiungere i criteri passando alla scheda **Criteri** e premendo il collegamento **+ Aggiungi criterio**.

1. Nella finestra successiva, premi **Carica PDF** e seleziona i documenti di politica del brand in formato PDF

   ![Carica il documento sulla politica del brand](/help/ai-in-aem/agents/governance/assets/upload_brand_policy_document.png){width="70%"}

   L’agente di governance analizzerà le linee guida della politica del brand utilizzando la lingua naturale, estraerà gli assegni ottenuti dal documento e li tradurrà in attività effettive. Una volta elaborato il documento, è possibile visualizzare un riepilogo dell’importazione, incluso il numero di controlli e lo stato del criterio, come illustrato di seguito:

   ![Finestra di panoramica sullo stato dei criteri del brand](/help/ai-in-aem/agents/governance/assets/policy_status.png)

1. Dopo aver creato il brand e aver caricato il documento sulle policy, puoi ottenere una visualizzazione dettagliata per marchio dalla scheda **Marchi** e facendo clic sulla scheda di un brand. Questa è la visualizzazione che si desidera utilizzare per creare categorie di assegni, premendo i tre punti accanto a una categoria esistente e selezionando **+ Aggiungi categoria**, come mostrato nella schermata seguente:

   ![Aggiungi categoria](/help/ai-in-aem/agents/governance/assets/add_category.png)

   È inoltre possibile utilizzare questa visualizzazione per creare, modificare ed eliminare i controlli, descritti nei passaggi seguenti.

1. Per una visualizzazione più dettagliata di ogni singolo controllo, puoi passare alla scheda **Controlli** e visualizzare un elenco di ogni singolo controllo estratto dai documenti delle linee guida. Puoi filtrare i controlli in base al marchio o allo stato:

   ![Visualizza singoli controlli marchio](/help/ai-in-aem/agents/governance/assets/see_brand_checks.png)

   È inoltre possibile visualizzare ulteriori dettagli su ogni singolo controllo facendo clic sui tre punti (**...**) a sinistra del controllo e premendo **Visualizza dettagli**. Verrà aperta una nuova finestra con ulteriori informazioni sul controllo:

   ![Visualizza dettagli assegno individuale](/help/ai-in-aem/agents/governance/assets/view_check_details.png)

   È inoltre possibile eliminare gli assegni premendo **Elimina** dalla stessa posizione del menu oppure modificarli premendo **Modifica**:

   ![Modifica di un assegno](/help/ai-in-aem/agents/governance/assets/edit_check.png)

1. È possibile aggiungere manualmente un controllo premendo **Aggiungi controllo** nell&#39;angolo superiore sinistro della finestra Controlli:

   ![Aggiunta di un assegno](/help/ai-in-aem/agents/governance/assets/add_check.png)

   Nella schermata seguente, puoi configurare i dettagli come:

   * Nome del controllo
   * La regola, descritta in linguaggio naturale
   * La categoria
   * Ambito/i a cui si applica

   ![Configurazione dei dettagli di controllo](/help/ai-in-aem/agents/governance/assets/add_check_window.png)

1. Infine, per un elenco dei domini e dei brand a cui sono associati, puoi premere la scheda **Domini**. Questa sezione ti consente di aggiungere, eliminare o modificare i domini nel tuo elenco.

