---
title: Mappatura utenti e migrazione delle entità principali
description: Panoramica sulla mappatura degli utenti e sulla migrazione delle entità in AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: bf1260f9a49012bbcb4138e0a5498d8dda451b6a
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 5%

---

# Mappatura utenti e migrazione delle entità principali {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Migrazione utente"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) consente di spostare utenti e gruppi dal sistema Adobe Experience Manager (AEM) esistente ad AEM as a Cloud Service. Gli utenti esistenti devono essere mappati in modo che possano accedere tramite i loro ID IMS."

>[!NOTE]
>Per le versioni precedenti dello strumento di mappatura utente, vedere [documentazione legacy](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduzione {#introduction}

Come parte del percorso di transizione verso Adobe Experience Manager (AEM) as a Cloud Service, gli utenti e i gruppi (o &quot;entità principali&quot;) devono essere migrati dai sistemi AEM esistenti a AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante all’AEM as a Cloud Service è l’uso completamente integrato degli ID Adobi per accedere al livello di authoring. Questo processo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per gestire utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce il single sign-on in tutte le applicazioni cloud Adobe. Per ulteriori dettagli, consulta [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). A causa di questa modifica, gli utenti esistenti devono essere mappati sui loro ID IMS in modo che possano accedere a AEMaaCS utilizzando i loro profili IMS. Poiché i gruppi nell’AEM tradizionale sono fondamentalmente diversi dai gruppi nell’IMS, i gruppi non sono mappati, ma devono essere riconciliati dopo il completamento della migrazione.

## Dettagli migrazione entità {#principal-migration-detail}

Lo strumento Content Transfer e Cloud Acceleration Manager eseguiranno la migrazione al sistema cloud di tutte le entità associate al contenuto da migrare. Lo strumento Content Transfer (Trasferimento contenuti) esegue questa operazione copiando tutte le entità dal sistema AEM di origine durante il processo di estrazione. CAM Ingestion seleziona e migra solo le entità principali associate al contenuto da acquisire. Se un&#39;entità si trova in un criterio ACL o CUG di contenuto migrato, tale entità e tutti i gruppi in cui si trova verranno migrati i relativi gruppi predecessori (padre). Inoltre, se un’entità sul contenuto è un gruppo, verranno migrati anche tutti i suoi gruppi discendenti (figlio) e gli utenti.

## Dettagli mappatura utenti {#user-mapping-detail}

Gli utenti AEM possono essere mappati sugli utenti Adobe IMS corrispondenti con lo stesso indirizzo e-mail. Questa mappatura può essere eseguita automaticamente in CTT (durante il passaggio di estrazione) e, se viene eseguita o meno, può essere controllata da un interruttore prima di avviare l’estrazione. L’impostazione predefinita dell’interruttore può essere ignorata dall’utente all’avvio dell’estrazione.

* Se il sistema di origine è un’istanza di authoring, per impostazione predefinita la scelta per eseguire la mappatura è _il_, perché è il processo consigliato.
* Se il sistema di origine è un’istanza Publish, per impostazione predefinita la scelta per eseguire la mappatura è _disattivato_, poiché normalmente gli utenti non vengono migrati o utilizzati nelle istanze di pubblicazione; o se vengono utilizzati, in genere viene utilizzato un sistema di autenticazione diverso (ovvero, non IMS).

Indipendentemente dal fatto che gli utenti siano mappati o meno durante l’estrazione, vengono migrati al sistema cloud, insieme ai gruppi, durante l’acquisizione se sono associati al contenuto di cui stai eseguendo la migrazione.

## Considerazioni importanti sulla mappatura e la migrazione degli utenti {#important-considerations}

### Casi eccezionali {#exceptional-cases}

Vengono registrati i seguenti casi specifici:

1. Se un utente non ha un indirizzo e-mail nel `profile/email` campo di loro *jcr* , l&#39;utente in questione può essere migrato ma non è mappato. Questo scenario si verifica anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.
2. Se l’utente è disabilitato, viene trattato come gli altri utenti; viene mappato e migrato come normale e rimane disabilitato nell’istanza cloud.
3. Se esiste un’entità principale con gli stessi dati vincolati all’univocità (rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId) sia nell’istanza AEM di origine che nell’istanza AEM Cloud Service di destinazione, l’entità in questione non viene migrata e l’entità esistente in precedenza sul cloud system rimane invariata. Questa operazione viene registrata nel report di migrazione dell’entità.
4. Se un utente non è mappato a IMS tramite mappatura utenti, il profilo utente sul sistema cloud AEM non sarà riconosciuto da IMS; in questo caso, se accede tramite IMS, verrà creato un nuovo profilo (duplicato) su AEM, ma non conterrà le informazioni precedenti sul profilo. Il profilo utente originale sarà presente nel sistema cloud AEM, ma non sarà possibile accedervi tramite IMS, utilizzando solo il metodo AEM tradizionale (accesso locale). Per questo motivo, la mappatura di tutti gli utenti è vivamente consigliata per tutte le migrazioni degli autori.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** è impostato, le entità precedentemente trasferite all’istanza di Cloud Service vengono eliminate insieme all’intero archivio esistente; viene creato un nuovo archivio in cui viene acquisito il contenuto. Questa procedura reimposta anche tutte le impostazioni, incluse le autorizzazioni sull’istanza del Cloud Service target ed è true per un utente amministratore aggiunto al **amministratori** gruppo. L&#39;utente amministratore deve essere aggiunto di nuovo al **amministratori** per recuperare il token di accesso per l’acquisizione CTT/CAM.
* Quando vengono eseguite acquisizioni senza cancellazione (**Cancella contenuto esistente** non è impostato), se il contenuto non viene trasferito perché non è stato modificato dopo il trasferimento precedente, non vengono trasferiti né gli utenti né i gruppi associati a tale contenuto. Questa regola è vera anche se gli utenti e i gruppi sono cambiati nel sistema di origine. Questo perché gli utenti e i gruppi vengono migrati solo insieme al contenuto a cui sono associati. Per questo motivo, la migrazione di tutte le entità principali nuove di un gruppo nel sistema di origine verrà eseguita solo se fanno parte di un gruppo diverso di cui è in corso la migrazione o nell&#39;ACL di contenuti diversi di cui è in corso la migrazione. Per migrare successivamente queste entità, è consigliabile utilizzare i pacchetti oppure eliminare le entità principali dal target e migrare nuovamente il contenuto rilevante (Estrai con sovrascrivi e Acquisisci con cancellazione).
* Gli indirizzi e-mail duplicati non sono consentiti in IMS, ma sono consentiti in AEM (sia on-premise che nel cloud). Un utente può accedere all’AEM tramite IMS utilizzando il proprio indirizzo e-mail e verrà registrato nel profilo utente a cui fa riferimento IMS.
* Consulta [Migrazione di gruppi utenti chiusi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) per ulteriori considerazioni sulle entità utilizzate in un criterio Gruppo utenti chiuso (CUG).

## Riepilogo finale e relazione {#final-report}

Una volta completate correttamente l’estrazione e l’acquisizione, viene generato un rapporto che mostra i dettagli della migrazione principale. Consulta [Convalidare la migrazione dell’entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) per i dettagli.
