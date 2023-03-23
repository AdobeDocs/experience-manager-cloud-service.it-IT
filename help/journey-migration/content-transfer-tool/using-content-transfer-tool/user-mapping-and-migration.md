---
title: Mappatura utente e migrazione principale
description: Panoramica della mappatura degli utenti e della migrazione principale
source-git-commit: aeb8f633b45908a87f15f9feeb3723f90470be92
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 22%

---

# Mappatura utente e migrazione principale {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Mappatura utenti"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) consente di spostare gli utenti e i gruppi dal sistema AEM esistente ad AEM as a Cloud Service. Gli utenti esistenti devono essere mappati secondo i loro ID IMS per evitare di esssere duplicati nell’istanza di authoring del Cloud Service."

>[!NOTE]
>Per le versioni precedenti dello strumento User Mapping (Mappatura utente), consulta la sezione [documentazione legacy](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduzione {#introduction}

Come parte del percorso di transizione ad Adobe Experience Manager (AEM) as a Cloud Service, devi spostare gli utenti e i gruppi dal sistema AEM esistente ad AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring. A tal fine è necessario utilizzare [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce un accesso singolo a tutte le applicazioni cloud di Adobe. Per ulteriori informazioni, consultare [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=it#identity-management). A causa di questa modifica, gli utenti esistenti devono essere mappati ai loro ID IMS per evitare di duplicare gli utenti nell’istanza di authoring del Cloud Service. Poiché i gruppi nelle AEM tradizionali sono fondamentalmente diversi dai gruppi in IMS, i gruppi non vengono mappati, ma i due gruppi devono essere riconciliati al termine della migrazione.

## Mappatura degli utenti e dettagli sulla migrazione {#user-mapping-detail}

Lo strumento Content Transfer (Trasferimento contenuti) e Cloud Acceleration Manager eseguiranno la migrazione degli utenti associati al contenuto in corso di migrazione. Questa mappatura viene eseguita automaticamente e se viene eseguito può essere controllato da un interruttore prima dell’avvio dell’estrazione. L’utente può ignorare l’impostazione predefinita dell’interruttore quando avvia l’estrazione.

* Se il sistema di origine è un&#39;istanza dell&#39;autore, per impostazione predefinita la scelta per eseguire la mappatura è _su_, poiché si tratta del processo consigliato.
* Se il sistema di origine è un&#39;istanza di pubblicazione, per impostazione predefinita la scelta per eseguire la mappatura è _off_, poiché normalmente gli utenti non vengono migrati o utilizzati nelle istanze di pubblicazione.

## Considerazioni importanti per la mappatura e la migrazione di utenti {#important-considerations}


### Casi eccezionali {#exceptional-cases}

Vengono registrati i seguenti casi specifici:

1. Se un utente non dispone di un indirizzo e-mail nel `profile/email` campo di applicazione *jcr* il nodo dell&#39;utente o del gruppo in questione può essere migrato ma non verrà mappato. Ciò vale anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.

1. Se l’utente è disabilitato, viene trattato come se non fosse disabilitato. Viene mappata e migrata come normale e rimane disabilitata sull’istanza cloud.

1. Se un utente esiste nell’istanza AEM Cloud Service di destinazione con lo stesso nome utente (rep:principalName) di uno degli utenti nell’istanza AEM di origine, l’utente o il gruppo in questione non verrà migrato.

1. Se un utente viene migrato senza prima essere mappato tramite User Mapping, o se il suo indirizzo e-mail non corrisponde all’indirizzo e-mail utilizzato per accedere a IMS, sul sistema cloud di destinazione non sarà in grado di accedere utilizzando il proprio IMS ID. Potrebbero essere in grado di accedere utilizzando il metodo tradizionale AEM, ma tenete presente che questo non è normalmente ciò che si vuole o si aspetta.


## Considerazioni aggiuntive {#additional-considerations}

* Se l’impostazione **Cancella il contenuto esistente sull’istanza Cloud prima dell’acquisizione** è impostato, gli utenti già trasferiti nell’istanza di Cloud Service verranno eliminati insieme all’intero archivio esistente e verrà creato un nuovo archivio per acquisire il contenuto in. Questo ripristina anche tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione ed è true per un utente amministratore aggiunto al **amministratori** gruppo. L&#39;utente amministratore deve essere letto nella sezione **amministratori** gruppo per recuperare il token di accesso per CTT.
* Quando si eseguono operazioni di integrazione dei contenuti, se il contenuto non viene trasferito perché non è stato modificato dal trasferimento precedente, gli utenti e i gruppi associati a tale contenuto non vengono trasferiti, anche se nel frattempo gli utenti e i gruppi sono cambiati. Questo perché gli utenti e i gruppi vengono migrati insieme al contenuto a cui sono associati.
* Se l’istanza AEM Cloud Service di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell’istanza AEM di origine e la mappatura utente è abilitata, nei registri viene scritto un messaggio di errore e l’utente AEM di origine non viene trasferito, in quanto sul sistema di destinazione è consentito un solo utente con un dato indirizzo e-mail.
