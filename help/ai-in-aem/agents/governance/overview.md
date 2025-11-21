---
title: Panoramica dell’agente di governance
description: Scopri in che modo AEM Governance Agent protegge l’integrità del brand e la conformità in AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 9b26cd1f30ad6fa23e28c9f36fe48091e069962e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Panoramica dell’agente di governance {#governance-agent}

**Governance Agent** è una soluzione progettata per salvaguardare l&#39;integrità del brand e la conformità in Adobe Experience Manager. Impone regole di sicurezza, normative e marchio per garantire che ogni interazione e attivazione rispetti gli standard stabiliti. L&#39;agente di governance è completamente integrato nell&#39;assistente di intelligenza artificiale ed è progettato per funzionare senza problemi all&#39;interno degli ambienti aziendali sfruttando gli strumenti **A2A (Agent-to-Agent)** e **MCP (Model Control Protocol)**. Queste integrazioni consentono all’agente di connettersi con orchestratori di intelligenza artificiale avanzati come ChatGPT, Claude e altri sistemi di intelligenza artificiale esterni, garantendo intelligenza flessibile e scalabile tra le piattaforme.

Le funzionalità principali includono:

* **Governance del brand:** mantenere la coerenza del brand e ridurre la revisione manuale automatizzando i controlli del brand tra contenuti e risorse
* **Autorizzazioni e Digital Rights Management (DRM):** garantisce una collaborazione sicura e conforme controllando le autorizzazioni e i diritti di utilizzo nelle risorse digitali.

Combinando queste funzioni, l’agente di governance riduce i rischi e consente una distribuzione rapida, sicura e on-brand su larga scala.

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Abilità nell’agente di governance di AEM {#skills-in-aem-governance-agent}

### Governance del brand {#brand-governance}

L’agente di governance può convalidare i contenuti in base alle linee guida del brand per garantire la coerenza tra tutte le esperienze digitali. Utilizza regole del brand preacquisite, come tono, dichiarazioni, utilizzo del logo, tipografia e immagini. Funziona in tempo reale all’interno della chat, degli editor e della modalità batch in Experience Hub, rendendolo ideale per contenuti generati dall’intelligenza artificiale, migrazioni di siti e creazione di siti in breve tempo.

![Panoramica sulla governance dei marchi](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**Esempi di richiesta:**

* *La pagina è allineata al mio marchio?`https://www.website/en.html`*
* *`https://www.website/en.html` segue le linee guida per i messaggi del brand?*
* *Verifica se `https://www.website/homepage` segue le linee guida del brand*
* *Mostra le linee guida per il marchio*

### Autorizzazione e Digital Rights Management {#permission-and-digital-rights-management}

#### Gestione delle autorizzazioni in Content Hub {#permission-management-in-content-hub}

In Content Hub, l’agente di governance assicura che solo le persone giuste accedano alle risorse giuste al momento giusto. Grazie all&#39;applicazione di controlli granulari basati su attributi e diritti di utilizzo, protegge i contenuti sensibili e al tempo stesso consente una collaborazione sicura. Ciò significa ridurre i rischi di conformità, rafforzare l&#39;integrità del marchio e velocizzare i flussi di lavoro; i team possono condividere e riutilizzare le risorse in tutta sicurezza senza preoccuparsi di accessi non autorizzati o utilizzi impropri. Questo equilibrio tra sicurezza e flessibilità si traduce in una maggiore efficienza operativa e fiducia in tutta l&#39;organizzazione.

![Panoramica sulla gestione delle autorizzazioni](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**Esempi di richiesta:**

* *Mostra tutte le regole ABAC di Content Hub esistenti.*
* *Crea una regola che consenta al gruppo &quot;Marketing&quot; di accedere a tutte le risorse.*
* *Concedi al gruppo vendite l&#39;accesso alle risorse il cui marketing:segment è uguale a EMEA.*
* *Elimina tutte le regole che danno accesso ad agenzia esterna*
* *Cos&#39;è ABAC in Content Hub e cosa puoi aiutarmi a fare?*

#### Assets Digital Rights Management {#assets-digital-rights-management}

Utilizzando l’agente, puoi gestire i diritti digitali di Assets nell’ecosistema dei contenuti. Controlla le autorizzazioni e i diritti di utilizzo a un livello granulare, garantendo che le risorse siano accessibili e utilizzate solo entro limiti di conformità definiti. In questo modo è possibile garantire la massima tranquillità, proteggere la proprietà intellettuale, ridurre i rischi normativi e mantenere l&#39;integrità del marchio. Automatizzando l&#39;applicazione dei diritti, i team possono collaborare in modo sicuro e sicuro, accelerando la distribuzione dei contenuti senza compromettere la sicurezza o la conformità.

![Panoramica sulla gestione DRM](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**Esempi di richiesta:**

* *Le risorse dell&#39;utente scadono a breve?*
* *Trovami tutte le risorse bici scadute il mese scorso.*
* *Quali risorse sono scadute di recente?*
* *Trovami risorse senza data di scadenza*
* *Mostra tutte le risorse in /content/dam/products che stanno per scadere nei prossimi 14 giorni*

