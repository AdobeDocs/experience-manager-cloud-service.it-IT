---
title: Migrazione di gruppi utenti chiusi
description: Questa pagina fornisce le considerazioni speciali necessarie per abilitare i gruppi chiusi di utenti dopo la migrazione dei contenuti ad Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
source-git-commit: ca3c4bae2e652d75190d68c76b1dd4e09239f16c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Migrazione di gruppi utenti chiusi {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrazione di gruppi di utenti chiusi"
>abstract="La migrazione di gruppi chiusi di utenti (CUG) richiede attualmente alcuni controlli e passaggi per essere operativa dopo una migrazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="Gruppi di utenti chiusi nell’AEM"

Attualmente, i gruppi chiusi di utenti (CUG) richiedono alcuni passaggi aggiuntivi per funzionare nell’ambiente di destinazione di una migrazione.  Questo documento illustra lo scenario e i passaggi necessari per consentire loro di proteggere i nodi nel modo previsto.

## Migrazione dei gruppi

Le entità principali (inclusi i gruppi) vengono incluse automaticamente in una migrazione ad Adobe Experience Manager as a Cloud Service se sono associate al contenuto migrato tramite l’ACL di tale contenuto.

## Gruppi di utenti chiusi in migrazione

Attualmente, gruppi associati *solo* con un criterio Gruppo utenti chiuso (CUG) sono *non* incluso automaticamente nell’acquisizione. Se sono associati a qualsiasi contenuto tramite un ACL, come detto in precedenza, verranno migrati. La verifica dell’esistenza del gruppo deve essere eseguita prima di andare &quot;live&quot;. Il rapporto Principal (Principal Report), scaricato tramite la visualizzazione Processo di acquisizione, può essere utilizzato per verificare se il gruppo in questione è stato incluso o meno perché non si trovava in un ACL. Se il gruppo non esiste, deve essere creato nell’istanza di authoring, inclusa l’aggiunta di membri appropriati, e attivato affinché esista nell’istanza di pubblicazione.

Infine, è necessario attivare i processi per abilitare il gruppo utenti chiusi. Per eseguire questa operazione, ripubblica uno dei contenuti che contengono il criterio del gruppo utenti chiusi. Pertanto, nei normali processi di test, se si riscontra che il gruppo utenti chiusi non funziona, ripubblica quel contenuto (assicurandoti che sia pubblicato anche se non modificato).

Questo dovrebbe abilitare i criteri del gruppo utenti chiusi (CUG) alla pubblicazione e il contenuto sarà accessibile solo agli utenti autenticati che sono membri del gruppo associato ai criteri.

## Sviluppo attivo

Il team di migrazione sta lavorando per far sì che i criteri per i gruppi utenti chiusi (CUG) migrino e funzionino automaticamente, senza passaggi aggiuntivi dopo l’acquisizione del contenuto.
È consigliabile includere la funzionalità per gruppi utenti chiusi (CUG) in tutti i processi di test prima di provare a eseguire la pubblicazione.

## Riepilogo

In sintesi, questi sono i passaggi per abilitare il gruppo utenti chiusi (CUG) dopo una migrazione:

1. Assicurati che ogni gruppo utilizzato nei criteri del gruppo utenti chiusi (CUG) esista al momento della pubblicazione dopo la migrazione.
   - Un gruppo può già esistere se incluso nell’ACL di un contenuto migrato.
   - In caso contrario, utilizza i pacchetti per installarlo nell’istanza di destinazione (o crearlo manualmente lì) e attivarlo con i relativi membri. Verifica che esista al momento della pubblicazione.
1. Se il criterio del gruppo utenti chiusi non protegge ancora il nodo, ripubblica la pagina (assicurandosi che venga pubblicata anche se non sono state apportate modifiche a tale pagina).
   - Verifica ogni nodo protetto da CUG.
