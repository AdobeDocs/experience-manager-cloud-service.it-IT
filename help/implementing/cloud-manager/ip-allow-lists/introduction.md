---
title: Introduzione agli elenchi IP consentiti
description: Scopri come limitare gli indirizzi da cui gli utenti possono accedere ai domini di AEM as a Cloud Service con gli elenchi IP consentiti.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: ht
source-wordcount: '306'
ht-degree: 100%

---


# Introduzione agli elenchi IP consentiti {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gestione elenco IP Consentiti"
>abstract="AEM as a Cloud Service è accessibile tramite Internet ed è protetto tramite autenticazione e autorizzazione degli utenti. È possibile utilizzare gli elenchi IP Consentiti di Cloud Manager per controllare l’accesso e limitarlo ai soli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare degli elenchi di indirizzi IP consentiti attendibili da cui gli utenti del sito possono accedere ai domini AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=it" text="Aggiungere un elenco IP consentiti"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html?lang=itl" text="Visualizzare e aggiornare un elenco IP consentiti"

Per impostazione predefinita, AEM as a cloud service è accessibile tramite Internet. Mentre la sicurezza viene gestita tramite l’autenticazione e l’autorizzazione degli utenti, l’inserimento nell’elenco Consentiti IP è un modo per limitare l’accesso solo agli indirizzi IP attendibili.

È possibile utilizzare gli elenchi IP Consentiti di Cloud Manager per controllare l’accesso e limitarlo ai soli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono [creare degli elenchi](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) di indirizzi IP consentiti attendibili da cui gli utenti del sito possono accedere ai domini AEM.

Una volta aggiunti, [gli elenchi IP consentiti possono essere applicati/rimossi](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) più volte come unità o entità da un servizio di authoring e/o pubblicazione in un ambiente.

>[!NOTE]
>
>Se non viene applicato alcun elenco IP consentiti, per impostazione predefinita sono consentiti tutti gli indirizzi IP. Quando viene applicato un elenco IP consentiti, non sono consentiti indirizzi IP diversi da quelli presenti nell’elenco IP consentiti.

## Limitazioni {#limitations}

Ci sono diverse limitazioni nell’elenco IP consentiti da tenere a mente.

* È possibile aggiungere al programma fino a 50 elenchi IP consentiti
* A ogni elenco IP consentiti è possibile aggiungere un massimo di 50 indirizzi IP/CIDR.
* In Cloud Manager, in un ambiente sono supportati i nomi nell’elenco IP consentiti per il servizio di authoring, pubblicazione o entrambi.
