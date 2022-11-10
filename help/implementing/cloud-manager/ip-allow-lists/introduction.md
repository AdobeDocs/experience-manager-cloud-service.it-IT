---
title: Introduzione agli elenchi IP consentiti
description: Scopri come limitare gli indirizzi da cui gli utenti possono accedere ai domini di AEM as a Cloud Service con gli elenchi IP consentiti.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 18ecf3394ff575213756fced84a3b08795188240
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 56%

---


# Introduzione agli elenchi IP consentiti {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gestione degli elenchi IP consentiti"
>abstract="AEM as a Cloud Service è accessibile tramite Internet ed è protetto tramite autenticazione e autorizzazione degli utenti. È possibile utilizzare gli elenchi IP consentiti di Cloud Manager per controllare l’accesso e limitarlo ai soli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare degli elenchi di indirizzi IP consentiti affidabili da cui gli utenti del sito possono accedere ai domini AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=it" text="Aggiunta di un elenco IP consentiti"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=it" text="Visualizzazione e aggiornamento di un elenco IP consentiti"

AEM as a cloud service è per impostazione predefinita accessibile tramite Internet. Mentre la sicurezza viene gestita tramite l’autenticazione e l’autorizzazione degli utenti, l’inserimento nell’elenco Consentiti IP è un modo per limitare l’accesso solo agli indirizzi IP attendibili.

Gli elenchi consentiti IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo a tali indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono [creare elenchi consentiti](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) degli indirizzi IP affidabili da cui gli utenti del sito possono accedere ai loro domini AEM.

Una volta aggiunto, [Gli elenchi consentiti IP possono essere applicati/non applicati](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) più volte come unità o entità a un servizio di authoring e/o pubblicazione in un ambiente.

>[!NOTE]
>
>Se non viene applicato alcun elenco consentiti IP, per impostazione predefinita sono consentiti tutti gli indirizzi IP. Non appena viene applicato un elenco consentiti IP, non sono consentiti indirizzi IP, tranne quelli nell’elenco consentiti IP.

## Limitazioni {#limitations}

Vi sono diverse limitazioni degli elenchi IP consentiti da considerare.

* È possibile aggiungere al programma fino a 50 elenchi IP consentiti.
* A ogni elenco IP consentiti è possibile aggiungere un massimo di 50 indirizzi IP/CIDR.
* I nomi degli elenchi IP consentiti sono supportati in Cloud Manager per il servizio Author e/o Publish in un ambiente.
