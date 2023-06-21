---
title: Introduzione agli elenchi IP consentiti
description: Inserire nell'elenco Consentiti Scopri come limitare gli indirizzi da cui gli utenti possono accedere ai domini su AEM as a Cloud Service è possibile utilizzare i IP.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 18%

---


# Introduzione agli elenchi IP consentiti {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Inserire nell&#39;elenco Consentiti Gestire i IP"
>abstract="AEM as a Cloud Service è accessibile via Internet ed è protetto tramite autenticazione e autorizzazione degli utenti. I inserisce nell&#39;elenco Consentiti di IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo agli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare inserisce nell&#39;elenco Consentiti di indirizzi IP attendibili da cui gli utenti del sito possono accedere ai domini AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Aggiunta di un elenco IP consentiti"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="Visualizzazione e aggiornamento di un elenco IP consentiti"

Per impostazione predefinita, AEM as a cloud service è accessibile tramite Internet. Mentre la sicurezza viene gestita tramite l’autenticazione e l’autorizzazione degli utenti, l’inserimento nell’elenco Consentiti IP è un modo per limitare l’accesso solo agli indirizzi IP attendibili.

I inserisce nell&#39;elenco Consentiti di IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo a tali indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono [inserire nell&#39;elenco Consentiti creare](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) di indirizzi IP attendibili da cui gli utenti del sito possono accedere ai domini AEM.

Dopo l’aggiunta, [INSERIRE NELL&#39;ELENCO CONSENTITI È possibile applicare/annullare l’applicazione dei IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) più volte come unità o entità per un servizio Author e/o Publish in un ambiente.

>[!NOTE]
>
>Se non viene applicato alcun elenco Consentiti IP, per impostazione predefinita sono consentiti tutti gli indirizzi IP. Quando viene applicato un elenco Consentiti IP dell’interfaccia utente, non sono consentiti indirizzi IP diversi da quelli presenti nell’elenco Consentiti IP dell’interfaccia utente di.

## Limitazioni {#limitations}

Ci sono diverse limitazioni ai inserisce nell&#39;elenco Consentiti di IP da tenere a mente.

* È possibile aggiungere al programma un massimo di 50 inserisce nell&#39;elenco Consentiti di IP
* È possibile aggiungere un massimo di 50 indirizzi IP/CIDR a ogni inserisco nell&#39;elenco Consentiti di IP.
* In Cloud Manager sono supportati i nomi dei inserisce nell&#39;elenco Consentiti di IP per il servizio Author, Publish o entrambi, in un ambiente.
