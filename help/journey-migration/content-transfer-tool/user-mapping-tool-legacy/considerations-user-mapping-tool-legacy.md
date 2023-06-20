---
title: Considerazioni importanti per lo strumento di mappatura utenti (legacy)
description: Considerazioni importanti per lo strumento di mappatura utenti (legacy)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# Considerazioni importanti per lo strumento di mappatura utenti (legacy) {#important-considerations}

>[!INFO]
>
>Questa documentazione fa riferimento a una versione obsoleta dello strumento. Per ulteriori informazioni sull’ultima versione, consulta [Mappatura utenti e migrazione entità](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## Casi eccezionali {#exceptional-cases}

Vengono registrati i seguenti casi specifici:

1. Se un utente non ha un indirizzo e-mail nel `profile/email` campo di loro *jcr* dell&#39;utente o del gruppo in questione viene migrato ma non mappato.  Questa regola si applica anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.

1. Se non viene trovata una determinata e-mail nel sistema Identity Management System (IMS) di Adobe per l’ID organizzazione utilizzato (o se l’ID IMS non può essere recuperato per un altro motivo), l’utente o il gruppo in questione viene migrato ma non mappato.

1. Se l’utente è attualmente disattivato, viene trattato come se non lo fosse. Viene mappato e migrato come normale e rimane disabilitato nell’istanza cloud.

1. Se nell’istanza AEM Cloud Service di destinazione esiste un utente con lo stesso nome utente (rep:principalName) di uno degli utenti nell’istanza AEM di origine, l’utente o il gruppo in questione non viene migrato.

1. Se un utente viene migrato senza prima essere mappato tramite Mappatura utenti, nel sistema cloud di destinazione non potrà accedere con il proprio ID IMS.  Potrebbero essere in grado di accedere utilizzando il metodo tradizionale dell’AEM, ma tieni presente che normalmente non è ciò che si desidera o si aspetta.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** è impostato, gli utenti già trasferiti nell’istanza di Cloud Service vengono eliminati insieme all’intero archivio esistente e viene creato un nuovo archivio in cui acquisire il contenuto. Questa opzione reimposta anche tutte le impostazioni, incluse le autorizzazioni sull’istanza del Cloud Service target ed è true per un utente amministratore aggiunto al **amministratori** gruppo. L&#39;utente amministratore dovrà essere aggiunto di nuovo al **amministratori** gruppo per recuperare il token di accesso per CTT.

* Si consiglia di rimuovere qualsiasi utente esistente dall’istanza AEM del Cloud Service di destinazione prima di eseguire CTT con Mappatura utenti. In questo modo si evitano conflitti tra la migrazione degli utenti dall’istanza AEM di origine all’istanza AEM di destinazione. Se lo stesso utente esiste nell’istanza AEM di origine e nell’istanza AEM di destinazione, si verificheranno conflitti durante l’acquisizione.

* Quando si esegue l’integrazione del contenuto, se il contenuto non viene trasferito perché non è stato modificato rispetto al trasferimento precedente, non verranno trasferiti né gli utenti né i gruppi associati a tale contenuto, anche se nel frattempo gli utenti e i gruppi sono cambiati. Questo perché gli utenti e i gruppi vengono migrati insieme al contenuto a cui sono associati.

* Se l’istanza AEM Cloud Service di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell’istanza AEM di origine e la mappatura degli utenti è abilitata, nei registri viene scritto un messaggio di errore e l’utente AEM di origine non verrà trasferito, poiché nel sistema di destinazione è consentito un solo utente con un determinato indirizzo e-mail.

* Se due utenti nell’istanza AEM di origine hanno lo stesso indirizzo e-mail e la mappatura utenti è abilitata, nei registri viene scritto un messaggio di errore e uno degli utenti AEM di origine non verrà trasferito, poiché nel sistema di destinazione è consentito un solo utente con un determinato indirizzo e-mail.

### Passaggio successivo {#whats-next}

Dopo aver appreso le considerazioni importanti e i casi eccezionali, ora puoi utilizzare lo strumento. Vedi [Utilizzo dello strumento di mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) per ulteriori dettagli.
