---
title: Mappatura utenti e migrazione delle entità principali
description: Panoramica sulla mappatura degli utenti e sulla migrazione delle entità
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 22%

---

# Mappatura utenti e migrazione delle entità principali {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Mappatura degli utenti"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) consente di spostare gli utenti e i gruppi dal sistema AEM esistente ad AEM as a Cloud Service. Gli utenti esistenti devono essere mappati sui rispettivi ID IMS per evitare duplicati nell’istanza di authoring del Cloud Service."

>[!NOTE]
>Per le versioni precedenti dello strumento di mappatura utente, vedere [documentazione legacy](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introduzione {#introduction}

Come parte del percorso di transizione ad Adobe Experience Manager (AEM) as a Cloud Service, devi spostare gli utenti e i gruppi dal sistema AEM esistente ad AEM as a Cloud Service. Questa operazione viene eseguita dallo strumento Content Transfer (Trasferimento contenuti).

Una modifica importante per AEM as a Cloud Service è l’utilizzo completamente integrato degli Adobe ID per accedere al livello di authoring. A tal fine è necessario utilizzare [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html) per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate in Adobe Identity Management System (IMS), che fornisce un accesso singolo a tutte le applicazioni cloud di Adobe. Per ulteriori informazioni, consultare [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management). A causa di questa modifica, gli utenti esistenti devono essere mappati sui loro ID IMS per evitare utenti duplicati nell’istanza Autore Cloud Service. Poiché i gruppi nell’AEM tradizionale sono fondamentalmente diversi dai gruppi nell’IMS, i gruppi non sono mappati, ma devono essere riconciliati dopo il completamento della migrazione.

## Dettagli di mappatura utenti e migrazione {#user-mapping-detail}

Lo strumento Content Transfer (Trasferimento contenuti) e Cloud Acceleration Manager eseguiranno la migrazione di tutti gli utenti associati al contenuto da migrare. Questa mappatura viene eseguita automaticamente e, se viene eseguita, può essere controllata da un interruttore prima dell’avvio dell’estrazione. L’impostazione predefinita dell’interruttore può essere ignorata dall’utente all’avvio dell’estrazione.

* Se il sistema di origine è un’istanza di authoring, per impostazione predefinita la scelta per eseguire la mappatura è _il_, in quanto si tratta del processo consigliato.
* Se il sistema di origine è un’istanza Publish, per impostazione predefinita la scelta per eseguire la mappatura è _disattivato_, poiché di norma gli utenti non vengono migrati o utilizzati nelle istanze di pubblicazione.

## Considerazioni importanti sulla mappatura e la migrazione degli utenti {#important-considerations}


### Casi eccezionali {#exceptional-cases}

Vengono registrati i seguenti casi specifici:

1. Se un utente non ha un indirizzo e-mail nel `profile/email` campo di loro *jcr* nodo di cui è possibile eseguire la migrazione dell&#39;utente o del gruppo, ma non verrà mappato. Questo vale anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.

1. Se l’utente è disabilitato, viene trattato come se non lo fosse. Viene mappato e migrato come normale e rimane disabilitato nell’istanza cloud.

1. Se nell’istanza AEM Cloud Service di destinazione è presente un utente con lo stesso nome utente (rep:principalName) di uno degli utenti nell’istanza AEM di origine, la migrazione dell’utente o del gruppo in questione non verrà eseguita.

1. Se un utente viene migrato senza prima essere mappato tramite Mappatura utenti, o se il suo indirizzo e-mail non corrisponde a quello utilizzato per accedere a IMS, sul sistema cloud di destinazione non potrà accedere con il suo ID IMS. Potrebbero essere in grado di accedere utilizzando il metodo tradizionale dell’AEM, ma tieni presente che normalmente non è ciò che si desidera o si aspetta.


## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** è impostato, gli utenti già trasferiti nell’istanza di Cloud Service verranno eliminati insieme all’intero archivio esistente e verrà creato un nuovo archivio in cui acquisire il contenuto. Questa opzione reimposta anche tutte le impostazioni, incluse le autorizzazioni sull’istanza del Cloud Service target ed è true per un utente amministratore aggiunto al **amministratori** gruppo. L&#39;utente amministratore deve essere aggiunto di nuovo al **amministratori** gruppo per recuperare il token di accesso per CTT.
* Quando si esegue l’integrazione del contenuto, se il contenuto non viene trasferito perché non è stato modificato rispetto al trasferimento precedente, non vengono trasferiti né gli utenti né i gruppi associati a tale contenuto, anche se nel frattempo gli utenti e i gruppi sono cambiati. Questo perché gli utenti e i gruppi vengono migrati insieme al contenuto a cui sono associati.
* Se l’istanza AEM Cloud Service di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell’istanza AEM di origine e la mappatura degli utenti è abilitata, nei registri viene scritto un messaggio di errore e l’utente AEM di origine non viene trasferito, poiché nel sistema di destinazione è consentito un solo utente con un determinato indirizzo e-mail.
