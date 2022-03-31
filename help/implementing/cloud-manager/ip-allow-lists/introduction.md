---
title: Introduzione agli Elenchi consentiti IP
description: Scopri come gli elenchi consentiti IP possono limitare da quali indirizzi gli utenti possono accedere ai tuoi domini as a Cloud Service AEM.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introduzione agli Elenchi consentiti IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Gestire gli Elenchi consentiti IP"
>abstract="AEM as a cloud service è accessibile via Internet ed è protetto tramite autenticazione e autorizzazione degli utenti. Gli elenchi consentiti IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo agli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare elenchi consentiti di indirizzi IP affidabili da cui gli utenti del sito possono accedere ai loro domini AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Aggiungere un Elenco consentiti IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Visualizzare e aggiornare un Elenco consentiti IP"

AEM as a cloud service è accessibile via Internet ed è protetto tramite autenticazione e autorizzazione degli utenti. Gli elenchi consentiti IP di Cloud Manager possono essere utilizzati per limitare e controllare l’accesso solo agli indirizzi IP attendibili. Gli utenti di Cloud Manager con le autorizzazioni appropriate possono creare elenchi consentiti di indirizzi IP affidabili da cui gli utenti del sito possono accedere ai loro domini AEM.

Gli elenchi consentiti IP possono essere aggiunti una volta e applicati/non applicati più volte come unità o entità a un servizio di authoring e/o pubblicazione in un ambiente.

## Limitazioni  {#limitations}

Gli elenchi IP possono essere tenuti presenti in una serie di limitazioni.

* È possibile aggiungere al programma fino a 50 elenchi consentiti IP
* È possibile aggiungere a ogni elenco consentiti IP un massimo di 50 indirizzi IP/CIDR.
* I nomi degli elenchi consentiti IP sono supportati in Cloud Manager per i servizi di authoring e/o pubblicazione in un ambiente.
