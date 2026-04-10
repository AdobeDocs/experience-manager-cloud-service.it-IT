---
title: Introduzione a Edge Delivery Services in Cloud Manager
description: Scopri come distribuire i progetti Cloud Manager utilizzando Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 71d514b2eaf83732cc0856f6b508ab814fe7f469
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 53%

---


# Introduzione a Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità per quanto riguarda la creazione di contenuti sul sito web. Questa possibilità consente di effettuare le seguenti operazioni:

* Creare siti veloci con un punteggio Lighthouse perfetto.
* Monitoraggio continuo delle prestazioni tramite telemetria operativa.
* Aumento dell’efficienza di authoring separando le origini dei contenuti.

Puoi utilizzare sia la gestione dei contenuti AEM che l’authoring WYSIWYG utilizzando l’Editor universale, nonché l’authoring basato su documenti.

Cloud Manager in AEM as a Cloud Service consente di abilitare il servizio Edge Delivery per il progetto.

>[!TIP]
>
>Per informazioni dettagliate su Edge Delivery Services e su come utilizzarli con AEM, consulta la [panoramica su Edge Delivery Services](/help/edge/overview.md#how-does-it-work).

## Introduzione a Edge Delivery Services in Cloud Manager {#edge-in-cloud-manager}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, ora è possibile integrare il sito con Edge Delivery Services direttamente in Cloud Manager e pubblicare utilizzando un’[esperienza guidata e self-service](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

Inoltre, puoi accedere a un’esperienza unificata per gestire tutte le proprietà di AEM e al contempo garantire la coerenza tra i flussi di lavoro chiave. Questi flussi di lavoro includono la gestione dei nomi di dominio e dei certificati SSL e le mappature CDN.

Cloud Manager offre due tipi di distribuzione per Edge Delivery Services nella rete CDN gestita Adobe con funzionalità distinte. [Ulteriori informazioni](#edge-delivery-deployment-options).

>[!NOTE]
>
>Edge Delivery Services può anche essere integrato negli ambienti AEM Sites as a Cloud Service esistenti utilizzando la pipeline di configurazione e i selettori di origine. Per ulteriori dettagli, vedere [Proxy in Edge Delivery Services](/help/implementing/dispatcher/cdn-configuring-traffic.md#proxying-to-edge-delivery) e [Configurare un proxy da un ambiente esistente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment).

## Opzioni di implementazione di Edge Delivery Services in Adobe Managed CDN {#edge-delivery-deployment-options}

In Adobe Managed CDN sono disponibili due tipi di distribuzione per Edge Delivery Services:

1. **Con un ambiente AEMaaCS esistente**: configurare un proxy HTTP da un ambiente AEM Sites as a Cloud Service esistente. Questo approccio viene in genere utilizzato quando si dispone già di un ambiente esistente e si desidera migrare parte di un sito a Edge Delivery Services. Vedere [Configurare un proxy da un ambiente esistente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment).

1. **Senza un ambiente AEMaaCS esistente (ambiente Edge)**: configurare un nuovo sito Edge Delivery indipendentemente da un ambiente AEM Sites as a Cloud Service. Questo approccio viene utilizzato quando non disponi di un ambiente AEM Author o Publish e desideri utilizzare Edge Delivery Services da solo. Consulta [Configurare un sito Edge Delivery senza un ambiente esistente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment).

Queste due opzioni hanno anche funzionalità diverse:

* **La pipeline di configurazione** è disponibile per gli ambienti AEM as a Cloud Service.
* **La pipeline di configurazione** è attualmente disponibile solo per gli ambienti Edge tramite il programma Beta limitato.

Per istruzioni di installazione complete, consulta [CDN gestito da Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed)


## Informazioni su Edge Delivery Services con l’authoring di AEM (Beta) {#eds-aem-authoring}

>[!NOTE]
>
>Il livello di pubblicazione flessibile e le funzioni crosswalk di authoring di AEM descritte qui sono in Beta. Per partecipare a Beta, invia un&#39;e-mail a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con il tuo ID organizzazione Adobe e l&#39;ID programma.

Le moderne esperienze web richiedono prestazioni elevate, ma molte organizzazioni si basano anche su flussi di lavoro di authoring AEM consolidati, governance e modelli di riutilizzo dei contenuti. Per aiutare i team a modernizzare la distribuzione senza interrompere l’authoring, Cloud Manager introduce funzionalità che consentono di eseguire le seguenti operazioni:

* Distribuisci esperienze tramite Edge Delivery Services.
* Continua a utilizzare AEM Author per la creazione di contenuti.
* Eseguire il provisioning solo dell&#39;infrastruttura necessaria per l&#39;architettura.

Queste funzionalità consentono alle organizzazioni di adottare la distribuzione moderna in modo incrementale, senza sacrificare i flussi di lavoro esistenti.

### Opzioni di authoring per i siti Edge Delivery {#authoring-options-eds}

Quando crei un sito Edge Delivery in Cloud Manager, puoi scegliere l’approccio di authoring preferito:

* Authoring basato su documenti: creazione di contenuti in Google Drive o SharePoint. Non è richiesto alcun ambiente AEM.
* Authoring di AEM: creazione di contenuti in AEM mediante l&#39;Editor universale. Questo metodo richiede un ambiente AEM Author. Con questa opzione, non è necessario un livello di pubblicazione quando Edge Delivery gestisce la distribuzione dei contenuti.

Le organizzazioni possono scegliere tra questi approcci o utilizzarli entrambi in modo incrementale, a seconda delle preferenze del flusso di lavoro. Consulta [Crea il tuo primo sito Edge Delivery con un clic](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md).

### Livello di pubblicazione flessibile {#flexible-publish-tier}

Cloud Manager consente di configurare se è stato eseguito il provisioning di un livello di pubblicazione per gli ambienti del programma. Non tutte le architetture richiedono un livello di pubblicazione come mostrato nella tabella seguente:

| Architettura | Livello di pubblicazione |
| --- | --- |
| AEM Sites tradizionale | Obbligatorio |
| Headless/API-first | Obbligatorio |
| Edge Delivery Services | Non obbligatorio |

Attivando il livello di pubblicazione solo quando necessario, i team possono eseguire il provisioning degli ambienti più rapidamente, semplificare l’infrastruttura e ridurre i componenti non necessari. Consulta [Livello di pubblicazione flessibile (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

## Vantaggi dell’utilizzo del percorso consigliato da Adobe per Edge Delivery Services {#recommended-path-eds}

Ottimizza i vantaggi offerti da Adobe accedendo e utilizzando la licenza di Edge Delivery Services tramite Cloud Manager. In questo modo puoi sfruttare diversi vantaggi chiave.

* [Utilizza la licenza per il programma scelto](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [aggiorna altri programmi](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) o entrambi.
* [Utilizza un archivio Git esterno](/help/implementing/cloud-manager/managing-code/external-repositories.md) (porta il tuo Git personale) per sincronizzare e distribuire il codice del sito Edge Delivery Services. Per sfruttare questa funzionalità, devi prima [integrare il tuo sito in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). <!-- NEW from CQDOC-22867 -->
* [Utilizza la pipeline di configurazione di Edge Delivery](/help/implementing/dispatcher/cdn-configuring-traffic.md) per configurare le impostazioni CDN gestite da Adobe per il tuo sito Edge Delivery definendo regole quali filtri del traffico, selettori dell&#39;origine e reindirizzamenti. <!-- NEW from CQDOC-22867 -->
* Sfrutta i vantaggi di [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) per eseguire operazioni CRUD (creare, leggere, aggiornare, eliminare).
* [Accedi ai rapporti di SLA](/help/implementing/cloud-manager/reports/report-sla.md).
* [Accedi al supporto Adobe](/help/edge/overview.md#support-ticket) per i programmi di produzione registrati.

Se disponi di una licenza Edge Delivery Services (EDS), puoi utilizzare una [rete CDN gestita da Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) per il tuo sito Edge Delivery. In questo modo si abilita la gestione CDN self-service e i certificati DV che vengono rinnovati automaticamente ogni tre mesi, a meno che non si elimini il certificato.

In alternativa, se scegli di utilizzare la rete CDN (ovvero una rete CDN non gestita da Adobe), indipendentemente dalle licenze Edge Delivery Services, devi configurarla sulla piattaforma `aem.live`. Consulta [Configurazione CDN BYO](https://www.aem.live/docs/byo-cdn-setup).


## Informazioni sull’aggiunta di Edge Delivery Services a un programma di produzione o a un programma sandbox {#about-adding-eds-to-prod-sandbox}

 Edge Delivery Services può essere aggiunto in diversi modi a seconda di come hai iniziato il progetto e di quando desideri creare il sito.

| Caso d’uso | Descrizione |
| --- | --- |
| Desidero aggiungere Edge Delivery Services a un nuovo programma di produzione. | Consulta [Creare programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>Nella procedura guidata, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere Edge Delivery Services a un programma di produzione esistente. | Consulta [Modificare i programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Nella finestra di dialogo **Modifica programma**, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere un sito Edge Delivery a Cloud Manager | Consulta [Aggiungere un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Desidero creare un sito Edge Delivery ora | Consulta [Creare rapidamente un sito Edge Delivery in Cloud Manager con il clic di un pulsante](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| Desidero aggiungere Edge Delivery Services a un programma sandbox nuovo o esistente. | Consulta [Creare programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Quando crei un programma sandbox, Edge Delivery Services viene aggiunto al programma per impostazione predefinita; non è necessario selezionarlo.<br>I programmi sandbox esistenti prima della disponibilità generale di Edge Delivery ereditano automaticamente Edge Delivery Services. |
| Desidero creare un sito Edge Delivery che utilizzi l’authoring AEM | Consulta [Creare un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site). Quando si utilizza l’authoring AEM con Edge Delivery, il livello di pubblicazione è facoltativo. Consulta [Livello di pubblicazione flessibile (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier). |

>[!NOTE]
>
>* Per aggiungere o modificare programmi, è necessario essere membri del ruolo **Proprietario business** o disporre dell’autorizzazione necessaria.
>* Prima di poter applicare la licenza a un programma di produzione, l’organizzazione deve disporre di una licenza per Edge Delivery Services non utilizzata.
>* Una volta che la licenza Edge Delivery Services viene applicata o rimossa da un programma, la modifica ha effetto immediato senza la necessità di eseguire una pipeline.


## Informazioni sull’elenco attività di Edge Delivery in Cloud Manager {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

L’**elenco attività di Edge Delivery** in Cloud Manager è un elenco di controllo delle attività di onboarding per guidare l’utente attraverso questa procedura e nella gestione del sito Edge Delivery fino alla [pubblicazione](/help/journey-onboarding/go-live-checklist.md).

![Elenco attività di un sito Edge Delivery in Cloud Manager](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Attività | Descrizione |
| --- | --- | --- |
| 1 | Partecipa al canale di collaborazione sui prodotti | Facendo clic su **Invia richiesta ora** viene spedita ad Adobe una richiesta di creazione di un canale per la tua azienda. Se il canale esiste già, viene effettuato l’inoltro al canale della tua azienda. |
| 2 | Completa i prerequisiti | Consulta il [tutorial introduttivo](https://www.aem.live/developer/tutorial). |
| 3 | Aggiungi sito Edge Delivery O <br>Crea un sito ora | Consulta [Aggiungere un sito Edge Delivery](#eds-add-site).<br>Consulta [Creare un sito Edge Delivery in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| 4 | Configura un sito Edge Delivery per l’utilizzo di un archivio Git esterno | Consulta [Configurare un sito Edge Delivery per l’utilizzo di un archivio Git esterno](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md). |
| 5 | Aggiungi dominio | Consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 6 | Aggiungi certificato SSL | Consulta [Aggiungi certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 7 | Configura la CDN del sito Edge Delivery. | Consulta [Aggiungere una mappatura di dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md). |
| 8 | Configurare la convalida push | Consulta [Configurare la convalida push per un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md). |
| 9 | Pubblicazione | Consulta [Elenco di controllo per la pubblicazione](https://www.aem.live/docs/go-live-checklist). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## Registrare un ticket di assistenza {#eds-support-ticket}

{{support-ticket}}



