---
title: Introduzione ai nomi di dominio personalizzati
description: L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e di marchio in modo self-service.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: fe08925c86a82a600eabd5a7d4ad6e38b3e76dfe
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 8%

---


# Introduzione ai nomi di dominio personalizzati {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gestisci nomi di dominio personalizzati"
>abstract="L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e di marchio in modo self-service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="Aggiunta di un nome di dominio personalizzato"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="Visualizza e aggiorna nome di dominio personalizzato"

L’interfaccia utente di Cloud Manager consente di aggiungere un dominio personalizzato per identificare il sito con un nome univoco e di marchio in modo self-service. Adobe Experience Manager as a Cloud Service viene fornito con un nome di dominio predefinito che termina con `*.adobeaemcloud.com`. Questo nome di dominio predefinito rimane, anche dopo aver associato i nomi di dominio personalizzati al sito web.

## Cosa sono i nomi di dominio personalizzati? {#what-are-custom-domain-names}

A ciascun sito web è associato un indirizzo numerico unico, leggibile da una macchina, ad esempio `184.33.123.64`. Il DNS (Domain Name System) è ciò che ti consente di avere domini personalizzati con brand collegati ai siti web traducendo indirizzi numerici in indirizzi memorabili come `wknd.com`.

È buona prassi avere un nome di dominio per il tuo sito che sia memorabile per i tuoi clienti e rifletta il tuo marchio.

È possibile acquistare un nome di dominio da un registrar di nomi di dominio, da un&#39;azienda o un&#39;organizzazione che gestisce e vende nomi di dominio. I registrar dei nomi di dominio gestiscono i nomi di dominio sui server DNS.

>[!IMPORTANT]
>
>Cloud Manager non è un registrar di nomi di dominio e non fornisce servizi DNS.

## Limitazioni  {#limitations}

L’utilizzo di nomi di dominio personalizzati con AEMaaCS presenta diverse limitazioni.

* I nomi di dominio personalizzati sono supportati in Cloud Manager sia per i programmi di pubblicazione che per quelli di anteprima. I domini personalizzati lato autore non sono supportati.
* Ogni ambiente Cloud Manager può ospitare fino a un massimo di 500 domini personalizzati per ambiente.
* AEM as a Cloud Service non supporta i domini con caratteri jolly.
* Prima di aggiungere un nome di dominio personalizzato, è necessario installare un certificato SSL valido contenente il nome di dominio personalizzato per il programma. Per ulteriori informazioni, consulta Aggiunta di un certificato SSL .
* Impossibile aggiungere i nomi di dominio agli ambienti mentre è presente una pipeline in esecuzione corrente collegata a tali ambienti.
* È possibile aggiungere un solo nome di dominio alla volta.
* Lo stesso nome di dominio non può essere utilizzato in più di un ambiente.

>[!NOTE]
>
>I domini personalizzati sono supportati in Cloud Manager **only** se utilizzi la rete CDN gestita AEM. Se porti il tuo CDN e [puntare alla CDN gestita AEM](/help/implementing/dispatcher/cdn.md) per gestire i domini non Cloud Manager dovrai usare quel CDN specifico.

## Flusso di lavoro {#workflow}

L’aggiunta di un nome di dominio personalizzato richiede l’interazione tra il servizio DNS e Cloud Manager. Per questo motivo sono necessari diversi passaggi per installare, configurare e verificare i nomi di dominio personalizzati. La tabella seguente fornisce una panoramica dei passaggi necessari, tra cui le operazioni da eseguire quando si verificano errori comuni.

| Incremento | Descrizione | Responsabilità | Ulteriori informazioni |
|--- |--- |--- |---|
| 1 | Aggiungere un certificato SLL a Cloud Manager | Cliente | [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Aggiungi un record TXT per verificare il dominio | Cliente | [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Verifica stato di verifica del dominio | Cliente | [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3 bis | Se la verifica del dominio non riesce con lo stato `Domain Verification Failure` | Cliente | [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3 ter | Se la verifica del dominio non riesce con lo stato `Verified, Deployment Failed`, Adobe di contatto | Adobe Customer Care | [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Configura le impostazioni DNS aggiungendo i record CNAME DNS o APEX che puntano a AEM as a Cloud Service | Cliente | [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Verifica lo stato dei record DNS | Cliente | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5 bis | Se lo stato del record DNS non riesce con `DNS status not detected` | Cliente | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5 ter | Se lo stato del record DNS non riesce con `DNS resolves incorrectly` | Cliente | [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
