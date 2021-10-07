---
title: Considerazioni importanti sullo strumento di mappatura degli utenti
description: Considerazioni importanti sullo strumento di mappatura degli utenti
source-git-commit: 9d131daf5b6a0b1530ebff48627f6130ef716f3e
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Considerazioni importanti sullo strumento di mappatura degli utenti {#important-considerations}


## Casi eccezionali {#exceptional-cases}

Verranno registrati i seguenti casi specifici:

1. Se un utente non ha un indirizzo e-mail nel campo `profile/email` del proprio nodo *jcr*, l&#39;utente o il gruppo in questione verrà migrato ma non mappato.

1. Se una data e-mail non viene trovata nel sistema Adobe Identity Management System (IMS) per l’ID organizzazione utilizzato (o se l’ID IMS non può essere recuperato per un altro motivo), l’utente o il gruppo in questione verrà migrato ma non mappato.

1. Se l’utente è attualmente disattivato, viene trattato come se non fosse disabilitato. Sarà mappato e migrato normalmente e rimarrà disattivato nell’istanza cloud.

1. Se un utente esiste nell’istanza AEM Cloud Service di destinazione con lo stesso nome utente (rep:principalName) di uno degli utenti nell’istanza AEM di origine, l’utente o il gruppo in questione non verrà migrato.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella il contenuto esistente sull&#39;istanza Cloud prima dell&#39;acquisizione** è impostata, gli utenti già trasferiti sull&#39;istanza del Cloud Service verranno eliminati insieme all&#39;intero archivio esistente e verrà creato un nuovo archivio per l&#39;acquisizione del contenuto in. Questo ripristina anche tutte le impostazioni, comprese le autorizzazioni sull&#39;istanza del Cloud Service di destinazione ed è true per un utente amministratore aggiunto al gruppo **administrators** . L’utente amministratore dovrà essere aggiunto nuovamente al gruppo **administrators** per recuperare il token di accesso per CTT.

* Si consiglia di rimuovere qualsiasi utente esistente dal Cloud Service di destinazione AEM&#39;istanza prima di eseguire CTT con User Mapping. In questo modo si evita qualsiasi conflitto tra la migrazione degli utenti dall’istanza AEM di origine all’istanza AEM di destinazione. I conflitti si verificheranno durante l’acquisizione se lo stesso utente esiste nell’istanza AEM di origine e nell’istanza AEM di destinazione.

* Quando vengono eseguiti gli integratori di contenuto, se il contenuto non viene trasferito perché non è cambiato dal trasferimento precedente, gli utenti e i gruppi associati a tale contenuto non verranno trasferiti, anche se nel frattempo gli utenti e i gruppi sono cambiati. Questo perché gli utenti e i gruppi vengono migrati insieme al contenuto a cui sono associati.

* Se l’istanza AEM Cloud Service di destinazione ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di uno degli utenti nell’istanza AEM di origine e la mappatura utente è abilitata, nei registri verrà scritto un messaggio di errore e l’utente AEM di origine non verrà trasferito, in quanto sul sistema di destinazione è consentito un solo utente con un dato indirizzo e-mail.

* Se due utenti nell&#39;istanza AEM di origine hanno lo stesso indirizzo e-mail e User Mapping è abilitato, nei registri verrà scritto un messaggio di errore e uno degli utenti AEM di origine non verrà trasferito, in quanto sul sistema di destinazione è consentito un solo utente con un dato indirizzo e-mail.