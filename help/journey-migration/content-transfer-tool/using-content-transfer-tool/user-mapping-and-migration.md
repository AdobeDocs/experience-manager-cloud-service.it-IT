---
title: Mappatura utenti e migrazione delle entità principali
description: Panoramica sulla mappatura degli utenti e sulla migrazione delle entità in AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 2fdfb65543fa2942e809aa5d379f4000e40bd517
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 9%

---

# Mappatura utenti e migrazione delle entità principali {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Mappatura degli utenti"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) consente di spostare utenti e gruppi dal sistema Adobe Experience Manager (AEM) esistente ad AEM as a Cloud Service. Gli utenti esistenti devono essere mappati sui rispettivi ID IMS per evitare duplicati nell’istanza di authoring del Cloud Service."

>[!NOTE]
>Per le versioni precedenti dello strumento di mappatura utente, vedere [documentazione legacy](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduzione {#introduction}

Come parte del percorso di transizione verso Adobe Experience Manager (AEM) as a Cloud Service, gli utenti e i gruppi (o &quot;entità principali&quot;) devono essere migrati dai sistemi AEM esistenti a AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring. Questo processo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per gestire utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate nell’Adobe Identity Management System (IMS) che fornisce il single sign-on in tutte le applicazioni cloud Adobe. Per ulteriori dettagli, consulta [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). A causa di questa modifica, gli utenti esistenti devono essere mappati ai loro ID IMS per evitare la creazione di utenti duplicati nell’istanza Autore Cloud Service. Poiché i gruppi nell’AEM tradizionale sono fondamentalmente diversi dai gruppi nell’IMS, i gruppi non sono mappati, ma devono essere riconciliati dopo il completamento della migrazione.

## Dettagli migrazione entità {#principal-migration-detail}

Lo strumento Content Transfer e Cloud Acceleration Manager eseguiranno la migrazione al sistema cloud di tutte le entità associate al contenuto da migrare.  Lo strumento Content Transfer (Trasferimento contenuti) esegue questa operazione copiando tutte le entità dal sistema AEM di origine durante il processo di estrazione.  CAM Ingestion seleziona e migra solo le entità principali associate al contenuto da acquisire.

## Dettagli mappatura utenti {#user-mapping-detail}

Gli utenti AEM possono essere mappati sugli utenti Adobe IMS corrispondenti con lo stesso indirizzo e-mail.  Questa mappatura può essere eseguita automaticamente in CTT (durante il passaggio di estrazione) e, se viene eseguita o meno, può essere controllata da un interruttore prima di avviare l’estrazione. L’impostazione predefinita dell’interruttore può essere ignorata dall’utente all’avvio dell’estrazione.

* Se il sistema di origine è un’istanza di authoring, per impostazione predefinita la scelta per eseguire la mappatura è _il_, perché è il processo consigliato.
* Se il sistema di origine è un’istanza Publish, per impostazione predefinita la scelta per eseguire la mappatura è _disattivato_, poiché gli utenti non vengono normalmente migrati o utilizzati nelle istanze di pubblicazione; o se vengono utilizzati, in genere viene utilizzato un sistema di autenticazione diverso (ad esempio, non IMS).

Indipendentemente dal fatto che gli utenti siano mappati o meno durante l’estrazione, vengono migrati al sistema cloud, insieme ai gruppi, durante l’acquisizione se sono associati al contenuto di cui stai eseguendo la migrazione.

## Considerazioni importanti sulla mappatura e la migrazione degli utenti {#important-considerations}

### Casi eccezionali {#exceptional-cases}

Vengono registrati i seguenti casi specifici:

1. Se un utente non ha un indirizzo e-mail nel `profile/email` campo di loro *jcr* , l&#39;utente o il gruppo in questione può essere migrato ma non è mappato. Questo scenario si verifica anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.
2. Se l’utente è disabilitato, viene trattato come gli altri utenti; viene mappato e migrato come normale e rimane disabilitato nell’istanza cloud.
3. Se esiste un’entità principale con lo stesso nome (rep:principalName) sia sull’istanza AEM di origine che sull’istanza AEM Cloud Service di destinazione, l’entità in questione non viene migrata e l’entità esistente in precedenza sul cloud system rimane invariata.
4. Se un utente viene migrato senza essere mappato tramite Mappatura utenti, nel sistema cloud di destinazione l’utente non potrà accedere con il proprio ID IMS. Oppure, se il loro indirizzo e-mail non corrisponde a quello utilizzato per accedere a IMS, sul sistema cloud di destinazione non potranno accedere con il loro ID IMS. L&#39;accesso potrebbe essere eseguito con il metodo tradizionale AEM (accesso locale), ma questo metodo non è normalmente quello desiderato o previsto.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** è impostato, gli utenti già trasferiti nell’istanza di Cloud Service vengono eliminati insieme all’intero archivio esistente; viene creato un nuovo archivio in cui viene acquisito il contenuto. Questa procedura reimposta anche tutte le impostazioni, incluse le autorizzazioni sull’istanza del Cloud Service target ed è true per un utente amministratore aggiunto al **amministratori** gruppo. L&#39;utente amministratore deve essere aggiunto di nuovo al **amministratori** per recuperare il token di accesso per l’acquisizione CTT/CAM.
* Quando si esegue l’integrazione del contenuto, se il contenuto non viene trasferito perché non è stato modificato rispetto al trasferimento precedente, non vengono trasferiti né gli utenti né i gruppi associati a tale contenuto. Questa regola è vera anche se gli utenti e i gruppi sono cambiati nel sistema di origine. Il motivo è che utenti e gruppi vengono migrati solo insieme al contenuto a cui sono associati.
* Se l’istanza AEM Cloud Service di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell’istanza AEM di origine e la mappatura degli utenti è abilitata, i registri registrano un messaggio di errore. Inoltre, l’utente AEM di origine non viene trasferito, in quanto nel sistema di destinazione è consentito un solo utente con un determinato indirizzo e-mail.
* Consulta [Migrazione di gruppi utenti chiusi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) per ulteriori considerazioni sulle entità utilizzate in un criterio Gruppo utenti chiuso (CUG).

## Riepilogo finale e relazione {#final-report}

Una volta completate correttamente l’estrazione e l’acquisizione, viene generato un rapporto che mostra i dettagli della migrazione principale. Consulta [Convalidare la migrazione dell’entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) per i dettagli.
