---
title: Migrazione dei gruppi
description: Panoramica sulla migrazione dei gruppi in AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 7e7b311d425ae6cdee9eb9311c0a12af84f81096
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 4%

---


# Migrazione dei gruppi {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="Migrazione dei gruppi"
>abstract="Lo strumento di trasferimento contenuti consente di copiare utenti e gruppi dal sistema Adobe Experience Manager (AEM) esistente ad AEM as a Cloud Service."

>[!NOTE]
>Per le versioni precedenti dello strumento di mappatura utenti, consulta la [documentazione legacy](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduzione {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="Utenti non migrati"
>abstract="Lo strumento di trasferimento contenuti non esegue più la migrazione degli utenti. Gli utenti devono essere gestiti in Admin Console."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentazione di AEM Admin Console"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

Nell’ambito del percorso di transizione verso l’as a Cloud Service Adobe Experience Manager (AEM), è necessario migrare i gruppi dagli AEM esistenti ad AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli ID Adobe per accedere al livello di authoring. Questo processo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce il single sign-on in tutte le applicazioni cloud Adobe. Per ulteriori dettagli, vedere [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). A causa di questa modifica, gli utenti vengono creati automaticamente sull’AEM al primo accesso tramite IMS.  Pertanto, CTT non esegue la migrazione degli utenti al sistema cloud.  Gli utenti IMS devono essere inseriti in gruppi IMS, che possono essere gruppi migrati o nuovi gruppi inseriti nei gruppi AEM a cui è stata concessa l’autorizzazione per accedere al contenuto AEM da migrare.  In questo modo, gli utenti del sistema cloud avranno lo stesso accesso che avevano sul loro sistema AEM sorgente.

## Dettagli migrazione gruppo {#group-migration-detail}

Lo strumento Content Transfer (Trasferimento contenuti) e Cloud Acceleration Manager eseguiranno la migrazione dei gruppi associati al contenuto da migrare al cloud system. Lo strumento Content Transfer (Trasferimento contenuti) esegue questa operazione copiando tutti i gruppi dal sistema AEM di origine durante il processo di estrazione. CAM Ingestion seleziona e migra solo alcuni gruppi:

* Esistono diversi gruppi integrati e già presenti nel sistema cloud di destinazione; la migrazione di questi non avviene mai.
* Verrà effettuata la migrazione dei gruppi di membri diretti di qualsiasi gruppo incorporato a cui viene fatto riferimento direttamente o indirettamente in un criterio ACL o CUG di contenuti migrati, per garantire che gli utenti membri diretti o indiretti di tali gruppi mantengano l’accesso ai contenuti migrati.
* Se un gruppo si trova su un criterio ACL o CUG di contenuto migrato, verrà eseguita la migrazione di tale gruppo.
* Non verrà eseguita la migrazione di altri gruppi, ad esempio quelli non trovati in un criterio ACL o CUG, quelli già presenti nel sistema di destinazione e quelli con dati con vincoli di univocità già presenti nel sistema di destinazione.

Il percorso registrato/segnalato per un gruppo è solo il primo percorso che ha attivato la migrazione del gruppo e tale gruppo potrebbe trovarsi anche in altri percorsi di contenuto.

La maggior parte dei gruppi migrati è configurata per essere gestita da IMS.  Ciò significa che un gruppo in IMS con lo stesso nome sarà collegato al gruppo in AEM e tutti gli utenti IMS nel gruppo IMS diventeranno utenti AEM e membri del gruppo in AEM.  Questo consente agli utenti di avere accesso al contenuto in base a ACL o criteri CUG per il gruppo.

I gruppi migrati non sono più considerati &quot;gruppi locali&quot;; sono gruppi IMS e devono essere ricreati in IMS in modo da poter essere sincronizzati tra AEM e IMS.  Admin Console I gruppi possono essere creati in IMS tramite, tra gli altri metodi, singolarmente o in blocco.  Consulta [Gestione dei gruppi di utenti](https://helpx.adobe.com/ca/enterprise/using/user-groups.html) per informazioni dettagliate sulla creazione di gruppi singolarmente o in blocco nell&#39;Admin Console.

L’eccezione a questa configurazione IMS si verifica con i gruppi creati dalle raccolte Assets. Quando una raccolta viene creata su AEM, vengono creati gruppi per l’accesso a tale raccolta; tali gruppi vengono migrati al sistema cloud, ma non sono configurati per essere gestiti da IMS.  Per aggiungere utenti IMS a questi gruppi, è necessario aggiungerli nella pagina Proprietà gruppo dell’interfaccia utente di Assets, singolarmente o collettivamente, come parte di un altro gruppo IMS.


## Migrazione del gruppo di rinuncia {#group-migration-option}

CTT versione 3.0.20 e successive include un’opzione per disabilitare la migrazione dei gruppi.  Questa funzione è configurata nella console OSGI come segue:

* Apri la configurazione OSGI `(http://<server>/system/console/configMgr)`
* Fai clic sulla configurazione denominata **Configurazione del servizio di estrazione dello strumento Content Transfer**
* Deseleziona **Includi gruppi nella migrazione** per disabilitare le migrazioni dei gruppi
* Fai clic su **Salva** per salvare e attivare la configurazione nel server

Se questa impostazione è disabilitata, i gruppi non verranno migrati e non verrà generato alcun report di migrazione utenti/gruppi/ruoli né alcun report utente.

## Report utente {#user-report}

Durante la migrazione, gli utenti non vengono migrati, ma le relazioni utente-gruppo sul sistema di origine vengono perse a meno che non vengano in qualche modo acquisite.  Il report utente acquisisce alcune di queste informazioni in formato testo in un report utente. In esso, ogni utente viene segnalato (uno per riga) insieme a un elenco di gruppi di cui è membro (ma i gruppi non migrati non vengono inseriti in questo elenco), a meno che il suo elenco di gruppi non sia vuoto, nel qual caso l’utente non viene visualizzato. I gruppi segnalati insieme a ogni utente sono quelli di cui l’utente è membro direttamente o indirettamente nel sistema di origine; poiché i gruppi nel sistema di origine possono essere nidificati mentre nel sistema di destinazione non lo sono, questo elenco di gruppi supporta la nuova struttura di gruppi appiattiti in IMS.

In caso di acquisizione wipe e non wipe, i gruppi nell’elenco di un utente includeranno i gruppi migrati in entrambe le fasi.

Oltre ai gruppi per ogni utente, nel rapporto è presente un campo in cui è possibile aggiungere note per l’utente (e una descrizione dettagliata del significato della nota è presente anche nel rapporto).  Le note possibili sono:

* Gli utenti a cui viene fatto riferimento direttamente in un ACL avranno *Nota-A* nella sezione delle note, in quanto non si tratta di un caso d&#39;uso consigliato o di una best practice.
* Gli utenti che sono membri diretti di un gruppo predefinito avranno *Note-B* nella sezione delle note, poiché non si tratta di un caso d&#39;uso consigliato o di una best practice.

Questi casi possono verificarsi simultaneamente e contemporaneamente ai casi precedenti.

Il report utente viene aggiunto alla fine (e fa quindi parte) del report di migrazione principale (vedi [Riepilogo finale e report](#final-summary-and-report) di seguito).  Le informazioni contenute in questo rapporto, inclusi i gruppi segnalati per ogni utente, possono essere utilizzate per creare un file di caricamento di utenti in blocco che può essere utilizzato, ad Admin Console, per creare più utenti in IMS in blocco.  È possibile modificare in blocco anche gli utenti IMS esistenti.

Vedi [Gestione di più utenti | Caricamento in blocco CSV](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html) per dettagli sulla creazione o modifica in blocco di utenti tramite l&#39;Admin Console.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella contenuto esistente nell&#39;istanza Cloud prima dell&#39;acquisizione** è impostata, i gruppi precedentemente trasferiti all&#39;istanza di Cloud Service vengono eliminati insieme all&#39;intero archivio esistente; viene creato un nuovo archivio in cui viene acquisito il contenuto. Questa procedura consente inoltre di ripristinare tutte le impostazioni, incluse le autorizzazioni sull&#39;istanza del Cloud Service di destinazione, ed è true per tutti gli utenti aggiunti al gruppo **amministratori**. L&#39;utente amministratore deve essere aggiunto nuovamente al gruppo **amministratori** per recuperare il token di accesso per l&#39;acquisizione CTT/CAM.
* Quando si eseguono acquisizioni senza cancellazione (**Il contenuto esistente** non viene impostato), se il contenuto non viene trasferito perché non è stato modificato dal trasferimento precedente, i gruppi associati a tale contenuto non vengono trasferiti. Questa regola è vera anche se i gruppi sono cambiati nel sistema di origine. Questo perché i gruppi vengono migrati solo insieme al contenuto a cui sono associati. Per questo motivo, in questo caso non verrà eseguita la migrazione dei gruppi che sono membri di un gruppo nel sistema di origine, a meno che non facciano parte di un gruppo diverso di cui è in corso la migrazione o nell&#39;ACL di contenuti diversi di cui è in corso la migrazione. Per migrare successivamente questi gruppi, puoi utilizzare i pacchetti, eliminare i gruppi dalla destinazione e migrare nuovamente il contenuto pertinente o eseguire nuovamente la migrazione utilizzando un’acquisizione wipe.
* Durante un&#39;acquisizione non wipe, se esiste un gruppo con gli stessi dati vincolati all&#39;univocità (rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId) sia sull&#39;istanza AEM di origine che sull&#39;istanza AEM Cloud Service di destinazione, il gruppo in questione è _not_ migrato e il gruppo esistente in precedenza sul cloud rimane invariato. Questa operazione viene registrata nel report di migrazione dell’entità.
* Vedere [Migrazione di gruppi utenti chiusi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) per ulteriori considerazioni sui gruppi utilizzati in un criterio Gruppo utenti chiuso (CUG).

## Riepilogo finale e relazione

Una volta completate correttamente l’estrazione e l’acquisizione, viene generato un rapporto che mostra i dettagli della migrazione del gruppo. Per informazioni dettagliate, consulta [Come convalidare la migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration).
