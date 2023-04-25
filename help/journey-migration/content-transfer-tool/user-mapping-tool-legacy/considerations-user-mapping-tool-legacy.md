---
title: Considerazioni importanti sullo strumento di mappatura utente (legacy)
description: Considerazioni importanti sullo strumento di mappatura utente (legacy)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: f7be351c85b8db6d11033c7cf064529a46c2802a
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---

# Considerazioni importanti sullo strumento di mappatura utente (legacy) {#important-considerations}


## Casi eccezionali {#exceptional-cases}

Verranno registrati i seguenti casi specifici:

1. Se un utente non dispone di un indirizzo e-mail nel `profile/email` campo di applicazione *jcr* verrà effettuata la migrazione dell&#39;utente o del gruppo in questione, ma non verrà eseguita la mappatura.  Ciò avverrà anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.

1. Se una data e-mail non viene trovata nel sistema Adobe Identity Management System (IMS) per l’ID organizzazione utilizzato (o se l’ID IMS non può essere recuperato per un altro motivo), l’utente o il gruppo in questione verrà migrato ma non mappato.

1. Se l’utente è attualmente disattivato, viene trattato come se non fosse disabilitato. Sarà mappato e migrato normalmente e rimarrà disattivato nell’istanza cloud.

1. Se un utente esiste nell’istanza AEM Cloud Service di destinazione con lo stesso nome utente (rep:principalName) di uno degli utenti nell’istanza AEM di origine, l’utente o il gruppo in questione non verrà migrato.

1. Se un utente viene migrato senza prima essere mappato tramite User Mapping, nel sistema cloud di destinazione non sarà in grado di accedere utilizzando il proprio IMS ID.  Potrebbero essere in grado di accedere utilizzando il metodo tradizionale AEM, ma tenete presente che questo non è normalmente ciò che si vuole o si aspetta.

## Considerazioni aggiuntive {#additional-considerations}

* Se l’impostazione **Cancella il contenuto esistente sull’istanza Cloud prima dell’acquisizione** è impostato, gli utenti già trasferiti nell’istanza di Cloud Service verranno eliminati insieme all’intero archivio esistente e verrà creato un nuovo archivio per acquisire il contenuto in. Questo ripristina anche tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione ed è true per un utente amministratore aggiunto al **amministratori** gruppo. L’utente amministratore dovrà essere aggiunto di nuovo al **amministratori** gruppo per recuperare il token di accesso per CTT.

* Si consiglia di rimuovere qualsiasi utente esistente dal Cloud Service di destinazione AEM&#39;istanza prima di eseguire CTT con User Mapping. In questo modo si evita qualsiasi conflitto tra la migrazione degli utenti dall’istanza AEM di origine all’istanza AEM di destinazione. I conflitti si verificheranno durante l’acquisizione se lo stesso utente esiste nell’istanza AEM di origine e nell’istanza AEM di destinazione.

* Quando vengono eseguiti gli integratori di contenuto, se il contenuto non viene trasferito perché non è cambiato dal trasferimento precedente, gli utenti e i gruppi associati a tale contenuto non verranno trasferiti, anche se nel frattempo gli utenti e i gruppi sono cambiati. Questo perché gli utenti e i gruppi vengono migrati insieme al contenuto a cui sono associati.

* Se l’istanza AEM Cloud Service di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell’istanza AEM di origine e la mappatura utente è abilitata, nei registri verrà scritto un messaggio di errore e l’utente AEM di origine non verrà trasferito, in quanto sul sistema di destinazione è consentito un solo utente con un dato indirizzo e-mail.

* Se due utenti nell&#39;istanza AEM di origine hanno lo stesso indirizzo e-mail e User Mapping è abilitato, nei registri verrà scritto un messaggio di errore e uno degli utenti AEM di origine non verrà trasferito, in quanto sul sistema di destinazione è consentito un solo utente con un dato indirizzo e-mail.

### Passaggio successivo {#whats-next}

Dopo aver appreso le considerazioni importanti e i casi eccezionali, è ora possibile utilizzare lo strumento. Vedi [Utilizzo dello strumento di mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) per ulteriori dettagli.
