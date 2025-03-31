---
title: Gestione delle entità principali dopo la migrazione
description: Scopri come configurare utenti e gruppi in IMS e AEM
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: 50c8dd725e20cbd372a7d7858fc67b0f53a8d6d4
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 61%

---

# Gestione delle entità principali dopo la migrazione {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Gestione delle entità principali dopo la migrazione"
>abstract="Scopri come configurare utenti e gruppi in IMS e AEM"

Questo documento descrive i passaggi di alto livello che la clientela deve compiere per configurare i propri utenti e gruppi in IMS e AEM per utilizzare il proprio ambiente AEM as a Cloud Service.

Per informazioni sulla migrazione dei gruppi e sul report di migrazione delle entità disponibile a ogni acquisizione, vedi [Migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Per una guida sull&#39;utilizzo di file di gruppi e utenti in blocco in Admin Console, consulta [Caricamento in blocco di entità in IMS dopo aver utilizzato CTT](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md).

## Gestione delle entità principali {#managing-principals}

Per AEM as a Cloud Service, gli utenti e i gruppi devono essere gestiti principalmente utilizzando Admin Console.  Quando si prende in considerazione una migrazione, alcune di queste attività possono essere eseguite prima della migrazione dei contenuti.  Essenzialmente, di questi principali gruppi di attività

* Creare utenti e gruppi in IMS
* Assegnare utenti ai gruppi in IMS
* Assegnare gruppi IMS a gruppi AEM (se necessario)

I primi due possono essere eseguiti prima o dopo la migrazione dei contenuti.  Si tratta di passaggi che interessano solo gli utenti e i gruppi in IMS, che possono includere l’integrazione con un IDP esterno come Active Directory o LDAP.  Questi passaggi sono descritti in [Gestione delle entità principali in IMS con Admin Console](/help/journey-migration/managing-principals.md).

Una volta effettuata la migrazione del contenuto all’ambiente AEM as a Cloud Service, è possibile eseguire il terzo passaggio.

### Migrazione dei gruppi

Durante la fase di acquisizione della migrazione, i gruppi vengono migrati se sono necessari per soddisfare i criteri ACL o CUG sul contenuto migrato.  Per ulteriori dettagli, consulta la sezione [Migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

I gruppi migrati (quelli non creati dalla raccolta Assets o dalla creazione di cartelle private, consulta Raccolte e cartelle private di seguito) sono configurati come gruppi IMS.  Ciò significa che qualsiasi gruppo con lo stesso nome creato in IMS (tramite Admin Console, ad esempio) sarà collegato al gruppo in AEM e gli utenti che sono membri del gruppo IMS diventeranno membri del gruppo anche in AEM.  Affinché questo collegamento si verifichi, il gruppo deve prima essere creato anche in IMS.  Utilizza Admin Console per creare i gruppi, singolarmente o in blocco, nell’istanza AEM, come descritto in [Gestione delle entità principali in IMS con Admin Console](/help/journey-migration/managing-principals.md).

Utilizza l’interfaccia utente di AEM Security per assegnare gruppi IMS a gruppi AEM locali. A questo scopo, vai alla pagina Strumenti di AEM, fai clic su Sicurezza e scegli Gruppi.

### Utenti IMS

Poiché non viene effettuata la migrazione degli utenti, è necessario crearli in IMS in modo che possano essere utilizzati in AEM.  Ci sono diversi modi per farlo, ma è importante che gli utenti creati siano assegnati ai gruppi IMS corretti affinché possano avere lo stesso accesso ai contenuti che avevano nel precedente sistema AEM.  Uno degli strumenti che possono essere utilizzati a questo scopo è la funzionalità di caricamento in blocco in Admin Console. Utilizza lo strumento di caricamento in blocco per caricare gli utenti e i gruppi di cui devono essere membri.  Prima di eseguire questa operazione, i gruppi devono essere creati in IMS, come descritto in precedenza.

Per sapere a quali gruppi ogni utente deve appartenere, puoi utilizzare il Report utente (consulta [Migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  Questo rapporto elenca i gruppi di cui ogni utente deve essere membro e questo elenco verrà normalmente incluso nel file di input dell’utente in blocco da utilizzare con la funzionalità di caricamento in blocco di Admin Console.

### Raccolte e cartelle private

La creazione di una raccolta Assets o di una cartella privata crea automaticamente anche alcuni gruppi per gestire l’accesso a tale contenuto Assets.  Questi gruppi vengono migrati se sono menzionati nel contenuto migrato, ma non sono configurati per collegarsi direttamente ai gruppi IMS; in AEM rimangono &quot;gruppi locali&quot; e non possono essere gestiti tramite IMS.

Poiché questi gruppi non sono in IMS, non è possibile utilizzare lo strumento di caricamento in blocco per creare gli utenti come membri diretti.  Gli utenti IMS che sono anche in AEM possono essere aggiunti a questi gruppi singolarmente, ma per farlo in blocco richiede un passaggio aggiuntivo.  Di seguito è riportato un modo in cui è possibile eseguire questa operazione:
* Crea un nuovo gruppo o nuovi gruppi in Admin Console/IMS per accedere a raccolte o cartelle private e configurali per AEM.
* Accedi come membro del gruppo o dei gruppi in modo che vengano creati in AEM.
* Per le raccolte o le cartelle private migrate, utilizza l’interfaccia utente di Assets per aggiungere il nuovo gruppo come editor/proprietario/visualizzatore.
* Aggiungi utenti (o carica in blocco) ai nuovi gruppi in Admin Console.
* Quando l’utente accede a per la prima volta, il suo utente IMS verrà creato in AEM e dovrebbe avere accesso ai nuovi gruppi e quindi alla raccolta originale o ai gruppi di cartelle private.

Nota: per l&#39;assegnazione in blocco degli utenti, è necessario utilizzare i passaggi precedenti per creare gli utenti in IMS; gli utenti già esistenti in IMS non possono essere creati nuovamente tramite il caricamento in blocco, anche se è possibile utilizzare l&#39;editor in blocco per apportare questo tipo di modifiche (vedi [Caricamento utenti in blocco Admin Console](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html) in **Modifica dettagli utente**).
