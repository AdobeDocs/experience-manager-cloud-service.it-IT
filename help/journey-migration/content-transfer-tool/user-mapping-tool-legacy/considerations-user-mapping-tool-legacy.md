---
title: Considerazioni importanti per lo strumento di mappatura utenti (legacy)
description: Considerazioni importanti per lo strumento di mappatura utenti (legacy)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: 13a2386c099624a46e84126a939a9470e9b3a5f2
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# Considerazioni importanti per lo strumento di mappatura utenti (legacy) {#important-considerations}

>[!INFO]
>
>Questa documentazione fa riferimento a una versione obsoleta dello strumento. Per ulteriori informazioni sull&#39;ultima versione, vedere [Migrazione gruppo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

## Casi eccezionali {#exceptional-cases}

Vengono registrati i seguenti casi specifici:

1. Se un utente non dispone di un indirizzo e-mail nel campo `profile/email` del nodo *jcr*, l&#39;utente o il gruppo in questione viene migrato ma non mappato. Questa regola si applica anche se l’indirizzo e-mail viene utilizzato come nome utente per l’accesso.

1. Se non viene trovata un’e-mail nel sistema Identity Management System (IMS) di Adobe per l’ID organizzazione utilizzato (o se non è possibile recuperare l’ID IMS), viene eseguita la migrazione dell’utente o del gruppo, ma non viene eseguito il mapping.

1. Se l’utente è disabilitato, viene trattato come se non lo fosse. Viene mappato e migrato come normale e rimane disabilitato nell’istanza cloud.

1. Se nell’istanza AEM Cloud Service di destinazione esiste un utente con lo stesso nome utente (rep:principalName) di uno degli utenti nell’istanza AEM di origine, la migrazione dell’utente o del gruppo non viene eseguita.

1. Se un utente viene migrato senza prima essere mappato tramite Mappatura utenti, nel sistema cloud di destinazione non può accedere con il proprio ID IMS. L&#39;accesso potrebbe essere eseguito con il metodo AEM tradizionale, ma questo flusso di lavoro non corrisponde a quello desiderato o previsto.

## Considerazioni aggiuntive {#additional-considerations}

* Se l&#39;impostazione **Cancella contenuto esistente nell&#39;istanza Cloud prima dell&#39;acquisizione** è impostata, gli utenti già trasferiti nell&#39;istanza di Cloud Service vengono eliminati. Viene eliminato anche l’intero archivio esistente e viene creato un nuovo archivio in cui viene acquisito il contenuto. Questa azione reimposta anche tutte le impostazioni, incluse le autorizzazioni sull&#39;istanza del Cloud Service di destinazione, ed è true per un utente amministratore aggiunto al gruppo **amministratori**. L&#39;utente amministratore deve essere letto al gruppo **amministratori** per recuperare il token di accesso per CTT.

* L’Adobe consiglia di rimuovere qualsiasi utente esistente dall’istanza AEM del Cloud Service di destinazione prima di eseguire CTT con Mapping utente. Questa azione è necessaria per evitare conflitti tra la migrazione degli utenti dall’istanza AEM di origine all’istanza AEM di destinazione. Possono verificarsi conflitti durante l’acquisizione se lo stesso utente esiste nell’istanza AEM di origine e nell’istanza AEM di destinazione.

* Quando si esegue l’integrazione del contenuto, se il contenuto non viene trasferito perché non è stato modificato rispetto al trasferimento precedente, non vengono trasferiti né gli utenti né i gruppi associati a tale contenuto. Questa regola è valida anche se nel frattempo gli utenti e i gruppi sono cambiati. Il motivo è che utenti e gruppi vengono migrati insieme al contenuto a cui sono associati.

* Se l’AEM Cloud Service ha un utente con un nome utente diverso ma lo stesso indirizzo e-mail di un utente nell’istanza AEM di origine e la mappatura degli utenti è abilitata, viene registrato un messaggio di errore. Inoltre, l’utente AEM di origine non viene trasferito, in quanto nel sistema di destinazione è consentito un solo utente con un determinato indirizzo e-mail.

* Se due utenti nell’istanza AEM di origine hanno lo stesso indirizzo e-mail e Mappatura utenti è abilitata, viene registrato un messaggio di errore. Inoltre, viene trasferito uno degli utenti AEM di origine perché nel sistema di destinazione è consentito un solo utente con un determinato indirizzo e-mail.

### Passaggio successivo {#whats-next}

Dopo aver appreso le considerazioni importanti e i casi eccezionali, ora puoi utilizzare lo strumento. Vedi [Utilizzo dello strumento di mappatura utente](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) per ulteriori dettagli.
