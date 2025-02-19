---
title: Introduzione a Edge Delivery Services in Cloud Manager
description: Scopri come distribuire i progetti Cloud Manager utilizzando Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '766'
ht-degree: 100%

---


# Introduzione a Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità per quanto riguarda la creazione di contenuti sul sito web. Questa possibilità consente di effettuare le seguenti operazioni:

* Creare siti veloci con un punteggio Lighthouse perfetto.
* Monitorare costantemente le prestazioni tramite RUM (Monitoraggio dell’utilizzo reale).
* Aumento dell’efficienza di authoring separando le origini dei contenuti.

Puoi utilizzare sia la gestione dei contenuti AEM che l’authoring WYSIWYG utilizzando l’Editor universale, nonché l’authoring basato su documenti.

Cloud Manager in AEM as a Cloud Service consente di abilitare il servizio Edge Delivery per il progetto.

>[!TIP]
>
>Per informazioni dettagliate su Edge Delivery Services e su come utilizzarli con AEM, consulta la [panoramica su Edge Delivery Services](/help/edge/overview.md).

## Introduzione a Edge Delivery Services in Cloud Manager {#edge-in-cloud-manager}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, ora è possibile integrare il sito con Edge Delivery Services direttamente in Cloud Manager e pubblicare utilizzando un’[esperienza guidata e self-service](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Inoltre, puoi accedere a un’esperienza unificata per gestire tutte le proprietà di AEM e al contempo garantire la coerenza tra i flussi di lavoro chiave. Questi flussi di lavoro includono la gestione dei nomi di dominio e dei certificati SSL e le mappature CDN.

## Vantaggi dell’utilizzo del percorso consigliato da Adobe per Edge Delivery Services {#recommended-path-eds}

Ottimizza i vantaggi offerti da Adobe accedendo e utilizzando la licenza di Edge Delivery Services tramite Cloud Manager. In questo modo puoi sfruttare diversi vantaggi chiave.

* [Utilizza la licenza per il programma scelto](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [aggiorna altri programmi](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) o entrambi.
* Sfrutta i vantaggi di [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) per eseguire operazioni CRUD (creare, leggere, aggiornare, eliminare).
* [Accesso alla generazione di rapporti SLA](/help/implementing/cloud-manager/sla-reporting.md) (*in arrivo*)
* [Accedi al supporto Adobe](/help/edge/overview.md#support-ticket) per i programmi di produzione registrati.

Inoltre, l’utilizzo di Cloud Manager consente di utilizzare [Adobe Managed CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) per il sito Edge Delivery e di sfruttare vantaggi chiave, quali la gestione self-service della rete CDN, inclusa la configurazione e l’aggiunta di certificati DV. Inoltre, dopo la creazione di un certificato DV, Adobe lo rinnova automaticamente ogni tre mesi, a meno che non venga eliminato. Se non disponi di una licenza di Edge Delivery Services con Adobe e decidi di ignorare questi vantaggi, puoi utilizzare solo la tua rete CDN gestita autonomamente. Questa configurazione deve essere sulla piattaforma [`aem.live`](https://www.aem.live/docs/go-live-checklist#cdn-configuration).

## Informazioni sull’aggiunta di Edge Delivery Services a un programma di produzione o a un programma sandbox

Un Edge Delivery Services può essere aggiunto in diversi modi a seconda di come hai iniziato il progetto.

| Caso d’uso | Descrizione |
| --- | --- |
| Desidero aggiungere Edge Delivery Services a un nuovo programma di produzione. | Consulta [Creare programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>Nella procedura guidata, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere Edge Delivery Services a un programma di produzione esistente. | Consulta [Modificare i programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Nella finestra di dialogo **Modifica programma**, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere un sito Edge Delivery a Cloud Manager | Consulta [Aggiungere un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Desidero aggiungere Edge Delivery Services a un programma sandbox nuovo o esistente. | Consulta [Creare programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Quando crei un programma sandbox, Edge Delivery Services viene aggiunto al programma per impostazione predefinita; non è necessario selezionarlo.<br>I programmi sandbox esistenti prima della disponibilità generale di Edge Delivery ereditano automaticamente Edge Delivery Services. |

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
| 3 | Aggiungi sito Edge Delivery | Consulta [Aggiungere un sito Edge Delivery](#eds-add-site). |
| 4 | Aggiungi dominio | Consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Aggiungi certificato SSL | Consulta [Aggiungi certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configura la CDN del sito Edge Delivery. | Consulta [Aggiungere una configurazione CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md). |
| 7 | Configurare la convalida push | Consulta [Configurare la convalida push per un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md). |
| 8 | Pubblicazione | Consulta [Elenco di controllo per la pubblicazione](/help/edge/docs/go-live-checklist.md). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## Registrare un ticket di assistenza {#eds-support-ticket}

{{support-ticket}}



