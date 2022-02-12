---
title: 'Considerazioni sulle autorizzazioni per contenuti headless '
description: Scopri diverse considerazioni su autorizzazioni e ACL per un’implementazione headless con Adobe Experience Manager. Comprendi i diversi utenti tipo e i potenziali livelli di autorizzazione necessari sia per gli ambienti Author che per quelli Publish.
feature: Content Fragments,GraphQL API
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Considerazioni sulle autorizzazioni per contenuti headless

Con un’implementazione headless, è necessario affrontare diverse aree di sicurezza e autorizzazioni. Le autorizzazioni e gli utenti tipo possono essere considerati in generale in base all’ambiente AEM **Autore** o **Pubblica**. Ogni ambiente contiene utenti tipo diversi e con esigenze diverse.

## Considerazioni sul servizio authoring

Il servizio Author è il luogo in cui gli utenti interni creano, gestiscono e pubblicano i contenuti. Le autorizzazioni ruotano intorno ai diversi utenti tipo che gestiscono il contenuto.

### Gestione delle autorizzazioni a livello di gruppo

Come best practice, le autorizzazioni devono essere impostate su Gruppi in AEM. Noti anche come gruppi locali, questi gruppi possono essere gestiti nell’ambiente di authoring AEM.

Il modo più semplice per gestire l’appartenenza al gruppo è utilizzare i gruppi Adobe Identity Management System (IMS) e assegnare [Gruppi IMS a gruppi AEM locali](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en#managing-permissions-in-aem).

![Flusso delle autorizzazioni di Admin Console](assets/admin-console-aem-group-permissions.png)

Ad alto livello, il processo è:

1. Aggiungere utenti IMS a un gruppo di utenti IMS nuovo o esistente utilizzando [Admin Console](https://adminconsole.adobe.com/)
1. I gruppi IMS vengono sincronizzati con AEM quando gli utenti accedono.
1. Assegna gruppi IMS a gruppi AEM.
1. Impostare le autorizzazioni per AEM gruppi.
1. Quando gli utenti accedono a AEM e sono autenticati tramite IMS, ereditano le autorizzazioni del gruppo AEM.

>[!TIP]
>
> È possibile trovare un video dettagliato sulla gestione di IMS e AEM utenti e gruppi . [qui](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html).

Per gestire **gruppi** in AEM, passa a **Strumenti** > **Sicurezza** > **Gruppi**.

Per gestire le autorizzazioni dei gruppi in AEM, passa a **Strumenti** > **Sicurezza** > **Autorizzazioni**.

### Utenti DAM

&quot;DAM&quot;, in questo contesto, sta per Digital Asset Management. La **Utenti DAM** è un gruppo predefinito in AEM che può essere utilizzato per gli utenti &quot;quotidiani&quot; che gestiscono risorse digitali e frammenti di contenuto. Questo gruppo fornisce le autorizzazioni per **visualizzare**, **add**, **update**, **delete** e **pubblicare** Frammenti di contenuto e tutti gli altri file in AEM Assets.

Se utilizzi IMS per l’appartenenza al gruppo, aggiungi i gruppi IMS appropriati come membri del gruppo **Utenti DAM** gruppo. I membri del gruppo IMS ereditano le autorizzazioni del gruppo DAM Users durante l’accesso all’ambiente AEM.

#### Personalizzazione del gruppo utenti DAM

È meglio non modificare direttamente le autorizzazioni di un gruppo preconfigurato. Al contrario, puoi anche creare i tuoi gruppi personalizzati modellati dopo il **Utenti DAM** autorizzazioni di gruppo e ulteriori restrizioni all&#39;accesso a diversi **cartelle** in AEM Assets.

Per autorizzazioni più granulari, utilizza la variabile **Autorizzazioni** in AEM e aggiorna il percorso da `/content/dam` a un percorso più specifico, ovvero `/content/dam/mycontentfragments`.

Potrebbe essere opportuno concedere a questo gruppo di utenti le autorizzazioni necessarie per creare e modificare frammenti di contenuto, ma non per eliminarli. Per rivedere e assegnare le autorizzazioni per la modifica, ma non per eliminarla, vedi [Frammenti di contenuto - Considerazioni sull’eliminazione](/help/assets/content-fragments/content-fragments-delete.md).

### Editor modelli

La possibilità di modificare **Modelli per frammenti di contenuto** devono essere lasciati agli amministratori o a **piccolo gruppo** di utenti con autorizzazioni elevate. La modifica del modello per frammenti di contenuto ha molti effetti a valle.

>[!CAUTION]
>
>Le modifiche ai modelli di frammenti di contenuto modificano l’API GraphQL sottostante su cui le applicazioni headless si basano.

Se desideri creare un gruppo che gestisca i modelli di frammento di contenuto ma non l’accesso completo da parte dell’amministratore, puoi creare un gruppo con le seguenti voci di controllo di accesso:

| Percorso | Autorizzazione | Privilegi |
|-----| -------------| ---------|
| `/conf` | **consenti** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **consenti** | `rep:write`, `crx:replicate` |

## Autorizzazioni del servizio di pubblicazione

Il servizio Publish è considerato l’ambiente &quot;live&quot; ed è tipicamente quello con cui i consumatori API GraphQL interagiscono. I contenuti, dopo essere stati modificati e approvati nel servizio Author, vengono pubblicati nel servizio Publish . L’applicazione headless utilizza quindi il contenuto approvato dal servizio Publish tramite API GraphQL.

Per impostazione predefinita, il contenuto esposto tramite gli endpoint GraphQL del servizio AEM Publish è accessibile a tutti, inclusi gli utenti non autenticati.

### Autorizzazioni del contenuto

I contenuti esposti tramite AEM API GraphQL possono essere limitati utilizzando [Gruppi di utenti chiusi (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) impostate nelle cartelle delle risorse, che specificano quali gruppi di utenti AEM (e i relativi membri) possono accedere al contenuto delle cartelle Risorse.

I CUG delle risorse funzionano per:

* In primo luogo, negando l’accesso a tutte le cartelle e sottocartelle
* Quindi, consentire l&#39;accesso in lettura alla cartella e alle sottocartelle per tutti i gruppi di utenti AEM elencati nell&#39;elenco dei gruppi di utenti chiusi

I CUG possono essere impostati nelle cartelle di risorse contenenti contenuto esposto tramite API GraphQL. L’accesso alle cartelle di risorse su AEM Publish deve essere controllato tramite Gruppi di utenti, anziché direttamente dall’utente. Crea (o riutilizza) un gruppo di utenti AEM che consente di accedere alle cartelle di risorse contenenti contenuto esposto dalle API GraphQL.

#### Selezionare lo schema di autenticazione{#publish-permissions-users}

La [AEM Headless SDK](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) supporta due tipi di autenticazione:

* [Autenticazione basata su token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) utilizzo delle credenziali del servizio associate a un singolo account tecnico.
* Autenticazione di base tramite utenti AEM.

### Accedere all’API GraphQL

richieste HTTP che forniscono [credenziali di autenticazione appropriate](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) negli endpoint API GraphQL del servizio AEM Publish includere contenuto che le credenziali sono autorizzate a leggere e contenuto anonimamente accessibile. Gli altri utenti dell’API GraphQL non possono leggere il contenuto nelle cartelle protette da CUG.

