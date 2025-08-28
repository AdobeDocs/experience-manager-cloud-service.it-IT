---
title: Introduzione agli elenchi IP consentiti
description: Scopri come gli Elenchi consentiti IP possono limitare gli indirizzi da cui gli utenti possono accedere ai domini in AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fdd86b966f0480c00b7cd975d63a48b82fb1d027
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 21%

---


# Introduzione agli elenchi IP consentiti {#introduction}

Scopri come gli Elenchi consentiti IP possono limitare gli indirizzi da cui gli utenti possono accedere ai domini in AEM as a Cloud Service.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gestire gli elenchi IP consentiti"
>abstract="AEM as a Cloud Service è accessibile tramite Internet ed è protetto tramite autenticazione e autorizzazione degli utenti. È possibile utilizzare gli elenchi IP consentiti di Cloud Manager per controllare l’accesso e limitarlo ai soli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare degli elenchi di indirizzi IP consentiti attendibili da cui gli utenti del sito possono accedere ai domini AEM."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Aggiungere un elenco IP consentiti"
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Visualizzare e aggiornare un elenco di indirizzi IP consentiti"

## Panoramica {#overview}

Per impostazione predefinita, AEM as a Cloud Service è accessibile tramite Internet. Mentre la sicurezza viene gestita tramite l’autenticazione e l’autorizzazione degli utenti, l’inserimento nell’elenco Consentiti IP è un modo per limitare l’accesso solo agli indirizzi IP attendibili.

Gli Elenchi consentiti IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo a tali indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono [creare e aggiungere Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) di indirizzi IP attendibili da cui gli utenti del sito possono accedere ai domini AEM.

Dopo l&#39;aggiunta, è possibile applicare o rimuovere più volte [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) come unità o entità da un servizio Author, Publish o entrambi in un ambiente.

>[!NOTE]
>
>Se non viene applicato alcun Elenco consentiti IP, per impostazione predefinita sono consentiti tutti gli indirizzi IP. Quando viene applicato un Elenco consentiti IP, non sono consentiti indirizzi IP diversi da quelli dell’Elenco consentiti IP.

## Note sull’utilizzo {#usage-notes}

* È possibile aggiungere al programma un massimo di 50 Elenchi consentiti IP.
* A ogni Elenco consentiti IP è possibile aggiungere un massimo di 50 indirizzi IP/CIDR.
* I nomi di Elenchi consentiti IP sono supportati in Cloud Manager per il servizio Author, Publish o entrambi in un ambiente.

### Pipeline front-end e Elenchi consentiti IP {#front-end-pipeline}

Se si utilizza, o si intende utilizzare, la pipeline front-end [per sviluppare siti](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md), è necessario aggiungere in anticipo il seguente Elenco consentiti IP di Cloud Manager.

Quando [aggiungi l&#39;Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist), denominalo *`Cloud Manager`*, quindi copia l&#39;elenco di indirizzi seguente e incollali nella finestra di dialogo Elenco consentiti IP.

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

Per evitare interruzioni nell’esecuzione della pipeline front-end, assicurati che questo Elenco consentiti IP di Cloud Manager sia aggiunto. Quindi, applica l&#39;elenco all&#39;ambiente di authoring *prima* di abilitare la pipeline.

Per ulteriori informazioni, vedere [Applica Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) e [Abilita pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

### Editor universale e Elenchi consentiti IP {#universal-editor}

Se si desidera utilizzare l&#39;editor universale per la creazione dei contenuti, è necessario aggiungere a un Elenco consentiti gli indirizzi IP utilizzati dal servizio Editor universale e applicarli.

1. Recuperare gli indirizzi IP utilizzati dal servizio Universal Editor dal seguente endpoint API: `http://universal-editor-service.adobe.io/ip-ranges`.
1. Creare un elenco consentiti con tali indirizzi IP, denominandolo `Universal Editor Service` o simile.
1. Applica l&#39;elenco consentiti `Universal Editor Service`.

L&#39;elenco degli indirizzi IP utilizzati dal servizio Universal Editor è soggetto a modifiche ed è necessario aggiornare di conseguenza l&#39;elenco consentiti.
