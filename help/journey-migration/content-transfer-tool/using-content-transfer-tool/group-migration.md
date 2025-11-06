---
title: Migrazione dei gruppi
description: Panoramica sulla migrazione dei gruppi in AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 3%

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

Come parte del percorso di transizione verso Adobe Experience Manager (AEM) as a Cloud Service, i gruppi devono essere migrati dai sistemi AEM esistenti ad AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring. Questo processo richiede l&#39;utilizzo di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS) che fornisce il single sign-on in tutte le applicazioni cloud Adobe. Per ulteriori dettagli, vedere [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). A causa di questa modifica, gli utenti vengono creati automaticamente su AEM al primo accesso tramite IMS.  Pertanto, CTT non esegue la migrazione degli utenti al sistema cloud.  Gli utenti IMS devono essere inseriti in gruppi IMS, che possono essere gruppi di cui è stata effettuata la migrazione o nuovi gruppi inseriti nei gruppi AEM a cui è stata concessa l’autorizzazione per accedere al contenuto di AEM da migrare.  In questo modo, gli utenti del cloud system avranno lo stesso accesso che avevano sul sistema AEM sorgente.

## Dettagli migrazione gruppo {#group-migration-detail}

Lo strumento Content Transfer (Trasferimento contenuti) e Cloud Acceleration Manager eseguiranno la migrazione dei gruppi associati al contenuto da migrare al cloud system. Lo strumento Content Transfer (Trasferimento contenuti) esegue questa operazione copiando tutti i gruppi dal sistema AEM di origine durante il processo di estrazione. CAM Ingestion seleziona e migra solo alcuni gruppi:

* Se un gruppo si trova su un criterio ACL o CUG di contenuto migrato, verrà eseguita la migrazione di tale gruppo, con alcune eccezioni elencate di seguito.
* Esistono diversi gruppi integrati e già presenti nel sistema cloud di destinazione; la migrazione di questi non avviene mai.
   * Alcuni gruppi incorporati possono includere gruppi di membri che sono _non_ incorporati. Verrà eseguita la migrazione di tutti i gruppi di membri di questo tipo (membri diretti o membri di membri, ecc.) a cui viene fatto riferimento in un criterio ACL o CUG di contenuto migrato, per garantire che gli utenti membri di questi gruppi mantengano (direttamente o indirettamente) l&#39;accesso al contenuto migrato.
* Non verrà eseguita la migrazione di altri gruppi, ad esempio quelli non trovati in un criterio ACL o CUG, quelli già presenti nel sistema di destinazione e quelli con dati con vincoli di univocità già presenti nel sistema di destinazione.

Il percorso registrato/segnalato per un gruppo è solo il primo percorso che ha attivato la migrazione del gruppo e tale gruppo potrebbe trovarsi anche in altri percorsi di contenuto.

La maggior parte dei gruppi migrati è configurata per essere gestita da IMS.  Ciò significa che un gruppo in IMS con lo stesso nome verrà collegato al gruppo in AEM e che tutti gli utenti IMS nel gruppo IMS diventeranno utenti AEM e membri del gruppo in AEM.  Questo consente agli utenti di avere accesso al contenuto in base a ACL o criteri CUG per il gruppo.

Tieni presente che i gruppi migrati non sono più considerati &quot;gruppi locali&quot; di AEM; sono gruppi pronti per IMS in AEM anche se potrebbero non esistere ancora in IMS.  Devono essere ricreati separatamente in IMS in modo che possano essere sincronizzati tra AEM e IMS.  I gruppi possono essere creati in IMS tramite Admin Console, tra gli altri metodi, singolarmente o in blocco.  Consulta [Gestione dei gruppi di utenti](https://helpx.adobe.com/it/enterprise/using/user-groups.html) per informazioni dettagliate sulla creazione di gruppi singolarmente o in blocco in Admin Console.

L’eccezione a questa configurazione IMS si verifica con i gruppi creati dalle raccolte Assets e dalle cartelle private. Quando si crea una raccolta o una cartella privata in AEM, vengono creati dei gruppi per l’accesso a tale contenuto; tali gruppi vengono migrati nel cloud system, ma non sono configurati per essere gestiti da IMS.  Per aggiungere utenti IMS a questi gruppi, è necessario aggiungerli nella pagina Proprietà gruppo dell’interfaccia utente di Assets, singolarmente o collettivamente, come parte di un altro gruppo IMS.


## Migrazione del gruppo di rinuncia {#group-migration-option}

CTT versione 3.0.20 e successive include un’opzione per disabilitare la migrazione dei gruppi.  Questa funzione è configurata nella console OSGI come segue:

* Apri la configurazione OSGI `(http://<server>/system/console/configMgr)`
* Fai clic sulla configurazione denominata **Configurazione del servizio di estrazione dello strumento Content Transfer**
* Deseleziona **Includi gruppi nella migrazione** per disabilitare le migrazioni dei gruppi
* Fai clic su **Salva** per salvare e attivare la configurazione nel server

Se questa impostazione è disabilitata, i gruppi non verranno migrati e non verranno generati rapporti sulla migrazione delle entità o sugli utenti (vedi sotto).

## Rapporto sulla migrazione principale e rapporto sugli utenti {#principal-migration-report}

Quando i gruppi vengono inclusi durante la migrazione (impostazione predefinita), viene salvato un rapporto sulla migrazione principale che illustra cosa accade a ciascun gruppo durante la migrazione.  Per scaricare questo rapporto dopo una corretta acquisizione:

* In CAM, vai a Trasferimento contenuti e seleziona Processi di acquisizione.
* Fai clic sui puntini di sospensione (...) nella riga dell’acquisizione in questione e scegli &quot;Visualizza riepilogo entità&quot;.
* Nella finestra di dialogo visualizzata, seleziona &quot;Report migrazione entità&quot; dall’elenco a discesa in &quot;Scarica un file...&quot; e fai clic sul pulsante Scarica.
* Salva il file CSV risultante.

Alcune delle informazioni registrate per gruppo sono:

* Se migrato, il percorso del primo ACL o CUG che ha causato la migrazione del gruppo.
* Indica se il gruppo è stato migrato in precedenza; se l’acquisizione corrente era un’acquisizione non wipe, alcuni gruppi potrebbero essere stati migrati durante un’acquisizione precedente.
* Se il gruppo è un gruppo integrato; questi gruppi non vengono migrati perché si trovano sempre nell’ambiente AEMaaCS di destinazione.
* Se il gruppo non faceva parte di un ACL o di un CUG nel contenuto migrato, non sarebbe stata eseguita la migrazione.
* Se il gruppo era locale, ad esempio un gruppo creato da una raccolta Assets, è possibile che sia stata eseguita la migrazione del gruppo e in questo caso viene aggiunta la parola &quot;locale&quot; al rapporto relativo al gruppo.

Durante la migrazione, gli utenti non vengono migrati, ma le relazioni utente-gruppo sul sistema di origine andrebbero perse a meno che non vengano in qualche modo acquisite. Il processo di acquisizione acquisisce alcune di queste informazioni in formato testo in un rapporto utente, che si trova alla fine del rapporto di migrazione principale.

### Report utente {#user-report}

Nella sezione Report utente vengono segnalati gli utenti (uno per riga) insieme al loro indirizzo e-mail e a un elenco di gruppi abilitati per IMS migrati durante questa acquisizione.  I gruppi che non sono stati migrati, che sono stati migrati durante un’acquisizione precedente o che sono gruppi locali non sono inclusi nell’elenco.   Se un utente non fa parte di alcun gruppo abilitato per IMS migrato e non dispone di note aggiuntive che indicano che si tratta di un caso speciale (vedi **Note** di seguito), tale utente non visualizza _not_ nel report. I gruppi riportati insieme a ogni utente sono quelli di cui l’utente è membro, direttamente o indirettamente, nel sistema di origine; poiché i gruppi nel sistema di origine possono essere nidificati mentre nel sistema di destinazione non lo sono, questo elenco di gruppi supporta la nuova struttura di gruppi appiattiti in IMS.

Nel caso di un’acquisizione wipe e quindi non wipe, i gruppi nell’elenco di un utente dall’acquisizione non wipe saranno solo quelli migrati durante la fase non wipe.

#### Note {#user-report-notes}

Oltre ai gruppi per ogni utente, nel Rapporto utente è presente un campo in cui è possibile fornire note sull’utente (e una descrizione dettagliata del significato della nota è presente anche nel rapporto) a scopo informativo.  Le note possibili sono:

* **Nota-A** Gli utenti a cui si fa riferimento direttamente in un ACL avranno *Nota-A* nella sezione delle note, in quanto non si tratta di un caso d&#39;uso consigliato o di una best practice.
* **Nota-B** Gli utenti che sono membri diretti di un gruppo predefinito avranno *Nota-B* nella sezione delle note, poiché non si tratta di un caso d&#39;uso consigliato o di una best practice.
* **Nota-C** Gli utenti che sono membri indiretti di un gruppo locale migrato (ad esempio un gruppo creato da una raccolta Assets) avranno *Nota-C* nella sezione delle note, poiché i gruppi locali non sono configurati per essere gestiti da IMS.

Questi casi possono verificarsi simultaneamente e contemporaneamente ai casi precedenti.  _Per ulteriori informazioni sui gruppi a cui ogni nota fa riferimento per ogni utente, controllare il registro di acquisizione, che riporta queste informazioni per ogni utente._

Il report utente viene aggiunto alla fine (e fa quindi parte) del report di migrazione principale (vedi [Riepilogo finale e report](#final-summary-and-report) di seguito) per fornire ai clienti una comprensione più completa dei gruppi e degli utenti e delle loro relazioni.

## File di caricamento in blocco {#bulk-upload-files}

Poiché la migrazione dei gruppi viene eseguita solo in AEM as a Cloud Service, è comunque necessario aggiungerli a IMS in modo che possano funzionare correttamente con AEM nel cloud. Inoltre, poiché non viene effettuata la migrazione degli utenti, è necessario aggiungerli a IMS. Questo passaggio non viene eseguito dagli strumenti di migrazione CTT/CAM, ma il processo di acquisizione crea due file di caricamento in blocco, uno per i gruppi e uno per gli utenti. Questi file possono essere modificati e quindi utilizzati, insieme alla funzionalità di caricamento in blocco di Admin Console, per creare gruppi IMS e utenti in base ai gruppi e agli utenti AEM.

Consulta [Caricamento di utenti e gruppi in blocco in IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md) per informazioni dettagliate su come utilizzare i file di caricamento in blocco per creare utenti e gruppi utilizzando Admin Console.

Vedi anche [Gestione utenti](https://helpx.adobe.com/ca/enterprise/using/users.html) per ulteriori dettagli sulla gestione degli utenti di AEM as a Cloud Service.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella contenuto esistente nell&#39;istanza Cloud prima dell&#39;acquisizione** è impostata, i gruppi precedentemente trasferiti all&#39;istanza Cloud Service vengono eliminati insieme all&#39;intero archivio esistente; viene creato un nuovo archivio in cui viene acquisito il contenuto. Questo processo reimposta anche tutte le impostazioni, incluse le autorizzazioni sull&#39;istanza di Cloud Service di destinazione, ed è true per tutti gli utenti aggiunti al gruppo **amministratori**. L&#39;utente amministratore deve essere aggiunto nuovamente al gruppo **amministratori** per recuperare il token di accesso per l&#39;acquisizione CTT/CAM.
* Quando si eseguono acquisizioni senza cancellazione (**Il contenuto esistente** non viene impostato), se il contenuto non viene trasferito perché non è stato modificato dal trasferimento precedente, i gruppi associati a tale contenuto non vengono trasferiti. Questa regola è vera anche se i gruppi sono cambiati nel sistema di origine. Questo perché i gruppi vengono migrati solo insieme al contenuto a cui sono associati. Per questo motivo, in questo caso non verrà eseguita la migrazione dei gruppi che sono membri di un gruppo nel sistema di origine, a meno che non facciano parte di un gruppo diverso di cui è in corso la migrazione o nell&#39;ACL di contenuti diversi di cui è in corso la migrazione. Per migrare successivamente questi gruppi, puoi utilizzare i pacchetti, eliminare i gruppi dalla destinazione e migrare nuovamente il contenuto pertinente o eseguire nuovamente la migrazione utilizzando un’acquisizione wipe.
* Durante un&#39;acquisizione senza cancellazione del contenuto, se esiste un gruppo con gli stessi dati con vincoli di univocità (rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId) sia sull&#39;istanza AEM di origine che sull&#39;istanza AEM Cloud Service di destinazione, il gruppo in questione è _not_ migrato e il gruppo esistente in precedenza sul cloud rimane invariato. Questa operazione viene registrata nel report di migrazione dell’entità.
* Vedere [Migrazione di gruppi utenti chiusi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) per ulteriori considerazioni sui gruppi utilizzati in un criterio Gruppo utenti chiuso (CUG).

## Riepilogo finale e relazione

Una volta completate correttamente l’estrazione e l’acquisizione, viene generato un rapporto che mostra i dettagli della migrazione del gruppo. Per informazioni dettagliate, consulta [Come convalidare la migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration).
