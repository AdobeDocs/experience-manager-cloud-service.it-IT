---
title: Migrazione di gruppi di utenti chiusi
description: Scopri le considerazioni speciali necessarie per abilitare i gruppi chiusi di utenti dopo la migrazione dei contenuti ad Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 12%

---


# Migrazione di gruppi di utenti chiusi {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrazione di gruppi utenti chiusi"
>abstract="La migrazione di gruppi di utenti chiusi (CUG) richiede attualmente alcuni controlli e passaggi affinché continui a essere operativa dopo una migrazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=it" text="Gruppi di utenti chiusi in AEM"

Attualmente, i gruppi chiusi di utenti (CUG) richiedono alcuni passaggi aggiuntivi per funzionare nell’ambiente di destinazione di una migrazione. Questo documento illustra lo scenario e i passaggi necessari per consentire loro di proteggere i nodi nel modo previsto.

## Migrazione di gruppi utenti chiusi (CUG)

I gruppi vengono inclusi automaticamente in una migrazione CTT/CAM ad Adobe Experience Manager as a Cloud Service se sono associati al contenuto migrato tramite l’ACL di quel contenuto o il relativo nodo di criteri CUG. La verifica dell’esistenza del gruppo e dei relativi membri deve essere eseguita prima di andare &quot;live&quot;. I gruppi a cui si fa riferimento in un criterio CUG sono denominati &quot;gruppi CUG&quot;.

Per utilizzare i gruppi utenti chiusi (CUG) in AEM as a Cloud Service, gli utenti devono essere presenti nell’istanza di authoring ed essere membri dei gruppi di utenti chiusi (CUG) pertinenti.  Questa operazione può essere eseguita utilizzando pacchetti; se gli utenti CUG sono utenti IMS, potrebbero essere già presenti.  Gli utenti dei gruppi di utenti chiusi (CUG) devono quindi essere resi membri dei gruppi di utenti chiusi (CUG) dell’AEM.

Per abilitare il comportamento dei gruppi utenti chiusi (CUG) nell’istanza Publish,
1. I gruppi CUG devono essere attivati (replicandoli insieme ai relativi membri nell’istanza Publish) e
1. Le pagine protette con i criteri per i gruppi utenti chiusi (CUG) devono essere pubblicate (in modo da abilitare l’istanza Publish e tenere traccia dei criteri).
1. Dopo la pubblicazione di tutte le pagine, verifica la funzionalità per ogni pagina protetta con gruppo utenti chiusi.

Per ulteriori informazioni, vedere [Gruppi utenti chiusi](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=it).
