---
title: Introduzione a Edge Delivery Services in Cloud Manager
description: Scopri come distribuire i progetti Cloud Manager utilizzando i Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e28e4bf06c28f97d665e5fd86ab87d484116504f
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 8%

---


# Introduzione a Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità per quanto riguarda la creazione di contenuti sul sito web. Questa funzionalità consente di effettuare le seguenti operazioni:

* Crea siti veloci con un punteggio perfetto Lighthouse.
* Monitoraggio continuo delle prestazioni tramite RUM (Real Use Monitoring).
* Aumentare l’efficienza di authoring disaccoppiando le origini di contenuto.

Puoi utilizzare sia la gestione dei contenuti AEM che l’authoring WYSIWYG utilizzando l’editor universale e l’authoring basato su documenti.

Cloud Manager in AEM as a Cloud Service consente di abilitare il servizio Edge Delivery per il progetto.

>[!TIP]
>
>Per informazioni dettagliate sui Edge Delivery Services e su come utilizzarli con AEM, consulta la [panoramica dei Edge Delivery Services](/help/edge/overview.md).

## Informazioni sui Edge Delivery Services in Cloud Manager {#edge-in-cloud-manager}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, puoi accedere al tuo sito tramite Edge Delivery Services direttamente in Cloud Manager e andare in diretta [tramite un&#39;esperienza guidata e autonoma](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Inoltre, puoi accedere a un’esperienza unificata per gestire tutte le proprietà dell’AEM e al contempo garantire la coerenza tra i flussi di lavoro chiave. Tra questi sono inclusi la gestione dei nomi di dominio, la gestione dei certificati SSL e le mappature CDN.

## Vantaggi dell’utilizzo del percorso consigliato dall’Adobe per i Edge Delivery Services {#recommended-path-eds}

Massimizzare i vantaggi offerti da Adobe accedendo alla licenza del Edge Delivery Services e utilizzandola tramite Cloud Manager. In questo modo puoi sfruttare diversi vantaggi chiave.

* [Utilizza la licenza per il programma scelto](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [aggiorna altri programmi](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) o entrambi.
* Sfrutta i vantaggi di [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) per eseguire operazioni CRUD (Create, Read, Update, Delete).
* [Accesso ai report di SLA](/help/implementing/cloud-manager/sla-reporting.md) (*in arrivo*)
* [Accedi al supporto Adobe](/help/edge/overview.md#support-ticket) per i programmi di produzione registrati.

Inoltre, l&#39;utilizzo di Cloud Manager consente di utilizzare [Adobe Managed CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) per il sito Edge Delivery e di sfruttare i vantaggi chiave, quali la gestione self-service della rete CDN, inclusa la configurazione e l&#39;aggiunta di certificati DV. Inoltre, dopo la creazione di un certificato DV, Adobe lo rinnova automaticamente ogni tre mesi, a meno che non venga eliminato. Se non disponi di una licenza di Edge Delivery Services con Adobe e decidi di ignorare questi vantaggi, puoi utilizzare solo la tua rete CDN gestita autonomamente. Questa configurazione deve essere sulla piattaforma [`aem.live`](https://www.aem.live/docs/go-live-checklist#cdn-configuration).

## Informazioni sull’aggiunta di Edge Delivery Services a un programma di produzione o a un programma sandbox

Un Edge Delivery Services può essere aggiunto in diversi modi a seconda di come hai iniziato il progetto.

| Caso d’uso | Descrizione |
| --- | --- |
| Voglio aggiungere dei Edge Delivery Services a un nuovo programma di produzione. | Consulta [Creare programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>Nella procedura guidata, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere Edge Delivery Services a un programma di produzione esistente. | Consulta [Modifica programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Nella finestra di dialogo **Modifica programma**, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere un sito Edge Delivery a Cloud Manager | Consulta [Aggiungere un sito Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Desidero aggiungere Edge Delivery Services a un programma sandbox nuovo o esistente. | Consulta [Creare programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Quando si crea un programma sandbox, i Edge Delivery Services vengono aggiunti al programma per impostazione predefinita; non è necessario selezionarlo.<br>I programmi sandbox esistenti prima della disponibilità generale di Edge Delivery ereditano automaticamente i Edge Delivery Services. |

>[!NOTE]
>
>* Per aggiungere o modificare programmi, è necessario essere membri del ruolo **Proprietario business** o disporre dell&#39;autorizzazione necessaria.
>* Prima di poter applicare la licenza a un programma di produzione, la tua organizzazione deve disporre di una licenza per Edge Delivery Services non utilizzata.
>* Una volta che la licenza Edge Delivery Services viene applicata o rimossa da un programma, la modifica ha effetto immediato senza la necessità di eseguire una pipeline.


## Informazioni sull’elenco delle attività di Edge Delivery {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

L&#39;**elenco attività di Edge Delivery** è un elenco di controllo delle attività di onboarding che ti guiderà attraverso l&#39;onboarding e la gestione del tuo sito Edge Delivery fino al [go-live](/help/journey-onboarding/go-live-checklist.md).

![Elenco attività sito Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Attività | Descrizione |
| --- | --- | --- |
| 1 | Partecipa al canale di collaborazione sui prodotti | Facendo clic su **Invia richiesta ora**, invia una richiesta ad Adobe per la creazione di un canale per la società. Se il canale esiste già, viene effettuato l’inoltro al canale della tua azienda. |
| 2 | Completa i prerequisiti | Facendo clic su **Visualizza esercitazione introduttiva**, si accede alla [Guida introduttiva - Esercitazione per sviluppatori](https://www.aem.live/developer/tutorial). |
| 3 | Aggiungi sito Edge Delivery | Consulta [Aggiungere un sito Edge Delivery](#eds-add-site). |
| 4 | Aggiungi dominio | Vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Aggiungi certificato SSL | Vedi [Aggiungi certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configurare la rete CDN del sito Edge Delivery | Vedere [Aggiungere una configurazione CDN](#add-cdn). |


## Registra un ticket di supporto {#eds-support-ticket}

{{support-ticket}}

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

