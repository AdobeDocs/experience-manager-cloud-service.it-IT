---
title: Introduzione agli elenchi IP consentiti
description: Scopri come gli Elenchi consentiti IP possono limitare gli indirizzi da cui gli utenti possono accedere ai domini in AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 20%

---


# Introduzione agli elenchi IP consentiti {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gestione degli elenchi IP consentiti"
>abstract="AEM as a Cloud Service è accessibile tramite Internet ed è protetto tramite l’autenticazione e l’autorizzazione degli utenti. Gli Elenchi consentiti IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo agli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare degli elenchi di indirizzi IP consentiti attendibili da cui gli utenti del sito possono accedere ai domini AEM."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Aggiungere un elenco IP consentiti"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Visualizzare e aggiornare un Elenco consentiti IP"

Per impostazione predefinita, l’accesso a AEM as a Cloud Service avviene tramite Internet. Mentre la sicurezza viene gestita tramite l’autenticazione e l’autorizzazione degli utenti, l’inserimento nell’elenco Consentiti IP è un modo per limitare l’accesso solo agli indirizzi IP attendibili.

Gli Elenchi consentiti IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo a tali indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono [creare Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) di indirizzi IP attendibili da cui gli utenti del sito possono accedere ai domini AEM.

Dopo l&#39;aggiunta, è possibile applicare o rimuovere più volte [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) come unità o entità da un servizio Author, Publish o entrambi in un ambiente.

>[!NOTE]
>
>Se non viene applicato alcun Elenco consentiti IP, per impostazione predefinita sono consentiti tutti gli indirizzi IP. Quando viene applicato un Elenco consentiti IP, non sono consentiti indirizzi IP diversi da quelli dell’Elenco consentiti IP.

## Limitazioni {#limitations}

Vi sono diverse limitazioni agli Elenchi consentiti IP da tenere a mente.

* Nel programma è possibile aggiungere fino a 50 Elenchi consentiti IP.
* A ogni Elenco consentiti IP è possibile aggiungere un massimo di 50 indirizzi IP/CIDR.
* I nomi di Elenchi consentiti IP sono supportati in Cloud Manager per il servizio Author, Publish o entrambi in un ambiente.
