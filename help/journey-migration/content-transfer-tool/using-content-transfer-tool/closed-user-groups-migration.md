---
title: Migrazione di gruppi di utenti chiusi
description: Scopri le considerazioni speciali necessarie per abilitare i gruppi chiusi di utenti dopo la migrazione dei contenuti ad Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 10%

---

# Migrazione di gruppi di utenti chiusi {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrazione di gruppi di utenti chiusi"
>abstract="La migrazione di gruppi di utenti chiusi (CUG) richiede attualmente alcuni controlli e passaggi affinché continui a essere operativa dopo una migrazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=it" text="Gruppi di utenti chiusi in AEM"

Attualmente, i gruppi chiusi di utenti (CUG) richiedono alcuni passaggi aggiuntivi per funzionare nell’ambiente di destinazione di una migrazione. Questo documento illustra lo scenario e i passaggi necessari per consentire loro di proteggere i nodi nel modo previsto.

## Migrazione dei gruppi

Gli utenti principali (inclusi i gruppi) vengono inclusi automaticamente in una migrazione ad Adobe Experience Manager as a Cloud Service se sono associati al contenuto migrato tramite l’ACL di tale contenuto e sono inclusi anche se vi si fa riferimento in un criterio CUG su tale contenuto.

## Gruppi di utenti chiusi in migrazione

La verifica dell’esistenza del gruppo e dei suoi membri deve essere eseguita prima della pubblicazione. Il rapporto Principal (Principal Report), scaricato tramite la visualizzazione Processo di acquisizione, può essere utilizzato per verificare se il gruppo in questione è stato incluso o meno perché non si trovava in un ACL o in un criterio CUG.

Successivamente, è necessario attivare i processi e impostare le proprietà per abilitare i gruppi utenti chiusi (CUG). A questo scopo, ripubblica tutte le pagine associate a un criterio CUG. In questo modo l’istanza Publish viene calibrata per tenere traccia dei criteri.

Questo abilita i criteri CUG in Pubblicazione e il contenuto è accessibile solo agli utenti autenticati che sono membri del gruppo associato ai criteri.

## Riepilogo

In sintesi, questi sono i passaggi per abilitare il gruppo utenti chiusi (CUG) dopo una migrazione:

1. Assicurati che ogni gruppo utilizzato nei criteri del gruppo utenti chiusi (CUG) esista al momento della pubblicazione dopo la migrazione.
   - Un gruppo può esistere se incluso nei criteri CUG di un contenuto migrato o nell’ACL di tale contenuto.
   - In caso contrario, utilizza i pacchetti per installarlo nell’istanza di destinazione (o crearlo manualmente) e attivarlo insieme ai relativi membri. Verifica che esista al momento della pubblicazione.
1. Ripubblica tutte le pagine associate a un criterio per gruppi utenti chiusi (CUG), assicurandoti che sia pubblicato, ad esempio, modificando prima la pagina. È importante ripubblicarli tutti.
   - Dopo la ripubblicazione di tutte le pagine, verifica la funzionalità per ogni pagina protetta con gruppo di utenti chiusi (CUG).
