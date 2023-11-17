---
title: Migrazione di gruppi di utenti chiusi
description: Scopri le considerazioni speciali necessarie per abilitare i gruppi chiusi di utenti dopo la migrazione dei contenuti ad Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 9%

---

# Migrazione di gruppi di utenti chiusi {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrazione di gruppi di utenti chiusi"
>abstract="La migrazione di gruppi di utenti chiusi (CUG) richiede attualmente alcuni controlli e passaggi affinché continui a essere operativa dopo una migrazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=it" text="Gruppi di utenti chiusi in AEM"

Attualmente, i gruppi chiusi di utenti (CUG) richiedono alcuni passaggi aggiuntivi per funzionare nell’ambiente di destinazione di una migrazione. Questo documento illustra lo scenario e i passaggi necessari per consentire loro di proteggere i nodi nel modo previsto.

## Migrazione dei gruppi

Le entità principali (inclusi i gruppi) vengono incluse automaticamente in una migrazione ad Adobe Experience Manager as a Cloud Service se sono associate al contenuto migrato tramite l’ACL di tale contenuto.

## Gruppi di utenti chiusi in migrazione

Attualmente, gruppi associati *solo* con un criterio Gruppo utenti chiuso (CUG) sono *non* incluso automaticamente nell’acquisizione. Come detto in precedenza, vengono migrati se associati a qualsiasi contenuto tramite un ACL. La verifica dell’esistenza del gruppo e dei suoi membri deve essere eseguita prima della pubblicazione. Il rapporto Principal (Principal Report), scaricato tramite la visualizzazione Processo di acquisizione, può essere utilizzato per verificare se il gruppo in questione è stato incluso o meno perché non si trovava in un ACL. Se il gruppo non esiste, deve essere creato nell’istanza di authoring, inclusa l’aggiunta di membri appropriati, e attivato affinché esista nell’istanza di pubblicazione. Questa operazione può essere eseguita utilizzando i pacchetti creati sull’origine.

Infine, è necessario attivare i processi e impostare le proprietà per abilitare i CUG. A questo scopo, ripubblica tutte le pagine associate a un criterio CUG. In questo modo l’istanza Publish viene calibrata per tenere traccia dei criteri.

Questo abilita i criteri CUG in Pubblicazione e il contenuto è accessibile solo agli utenti autenticati che sono membri del gruppo associato ai criteri.

## Sviluppo attivo

Il team di migrazione sta lavorando per far sì che i criteri per i gruppi utenti chiusi (CUG) migrino e funzionino automaticamente, senza alcun passaggio aggiuntivo dopo l’acquisizione del contenuto.
Includi la funzionalità per gruppi utenti chiusi (CUG) in tutti i processi di test prima di provare a eseguire la pubblicazione.

## Riepilogo

In sintesi, questi sono i passaggi per abilitare il gruppo utenti chiusi (CUG) dopo una migrazione:

1. Assicurati che ogni gruppo utilizzato nei criteri del gruppo utenti chiusi (CUG) esista al momento della pubblicazione dopo la migrazione.
   - Un gruppo può esistere se incluso nell’ACL di un contenuto migrato.
   - In caso contrario, utilizza i pacchetti per installarlo nell’istanza di destinazione (o crearlo manualmente) e attivarlo insieme ai relativi membri. Verifica che esista al momento della pubblicazione.
1. Ripubblica tutte le pagine associate a un criterio per gruppi utenti chiusi (CUG), assicurandoti che sia pubblicato, ad esempio, modificando prima la pagina. È importante ripubblicarli tutti.
   - Dopo la ripubblicazione di tutte le pagine, verifica la funzionalità per ogni pagina protetta con gruppo di utenti chiusi (CUG).
