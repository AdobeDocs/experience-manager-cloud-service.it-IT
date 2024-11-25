---
title: Gestione delle entità principali dopo la migrazione
description: Scopri come configurare utenti e gruppi in IMS e AEM
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: ht
source-wordcount: '773'
ht-degree: 100%

---

# Gestione delle entità principali dopo la migrazione {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Gestione delle entità principali dopo la migrazione"
>abstract="Scopri come configurare utenti e gruppi in IMS e AEM"

Questo documento descrive i passaggi di alto livello che la clientela deve compiere per configurare i propri utenti e gruppi in IMS e AEM per utilizzare il proprio ambiente AEM as a Cloud Service.

## Gestione delle entità principali {#managing-principals}

Per AEM as a Cloud Service, gli utenti e i gruppi devono essere gestiti principalmente utilizzando Admin Console.  Quando si prende in considerazione una migrazione, alcune di queste attività possono essere eseguite prima della migrazione dei contenuti.  Essenzialmente, di questi principali gruppi di attività

* Creare utenti e gruppi in IMS
* Assegnare utenti ai gruppi in IMS
* Assegnare gruppi IMS a gruppi AEM (se necessario)

i primi due possono essere eseguiti prima o dopo la migrazione dei contenuti.  Si tratta di passaggi che interessano solo gli utenti e i gruppi in IMS, che possono includere l’integrazione con un IDP esterno come Active Directory o LDAP.  Questi passaggi sono descritti in [Gestione delle entità principali in IMS con Admin Console](/help/journey-migration/managing-principals.md).

Una volta effettuata la migrazione del contenuto all’ambiente AEM as a Cloud Service, è possibile eseguire il terzo passaggio.

### Migrazione dei gruppi

Durante la fase di acquisizione della migrazione, i gruppi vengono migrati se sono necessari per soddisfare i criteri ACL o CUG sul contenuto migrato.  Per ulteriori dettagli, consulta la sezione [Migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

I gruppi migrati (quelli che non sono stati creati tramite la creazione di raccolte di risorse, consulta Raccolte di seguito) sono configurati come gruppi IMS.  Ciò significa che qualsiasi gruppo con lo stesso nome creato in IMS (tramite Admin Console, ad esempio) sarà collegato al gruppo in AEM e gli utenti che sono membri del gruppo IMS diventeranno membri del gruppo anche in AEM.  Affinché questo collegamento si verifichi, il gruppo deve prima essere creato anche in IMS.  Utilizza Admin Console per creare i gruppi, singolarmente o in blocco, nell’istanza AEM, come descritto in [Gestione delle entità principali in IMS con Admin Console](/help/journey-migration/managing-principals.md).

Utilizza l’interfaccia di Sicurezza AEM per assegnare gruppi IMS a gruppi AEM locali.  Consulta [Creazione e configurazione dei gruppi](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group).  Sebbene questo documento sia destinato ad AEM 6.5, si applica anche all’aggiunta di gruppi ad altri gruppi in AEM as a Cloud Service.

### Utenti IMS

Poiché non viene effettuata la migrazione degli utenti, è necessario crearli in IMS in modo che possano essere utilizzati in AEM.  Ci sono diversi modi per farlo, ma è importante che gli utenti creati siano assegnati ai gruppi IMS corretti affinché possano avere lo stesso accesso ai contenuti che avevano nel precedente sistema AEM.  Uno degli strumenti che possono essere utilizzati a questo scopo è la funzionalità di caricamento in blocco in Admin Console. Utilizza lo strumento di caricamento in blocco per caricare gli utenti e i gruppi di cui devono essere membri.  Prima di eseguire questa operazione, i gruppi devono essere creati in IMS, come descritto in precedenza.

Per sapere a quali gruppi ogni utente deve appartenere, puoi utilizzare il Report utente (consulta [Migrazione dei gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  Questo report elenca i gruppi di cui ogni utente deve essere membro e tale elenco può essere incluso nel file di input della funzionalità di caricamento in blocco di Admin Console.

### Raccolte

La creazione di una raccolta di risorse crea automaticamente anche alcuni gruppi per gestire l’accesso a tale raccolta.  Questi gruppi vengono migrati se sono menzionati nelle raccolte migrate, ma non sono configurati per collegarsi direttamente ai gruppi IMS. In AEM rimangono “gruppi locali” e non possono essere gestiti tramite IMS.

Poiché questi gruppi non sono in IMS, non è possibile utilizzare lo strumento di caricamento in blocco per creare gli utenti come membri diretti.  Gli utenti IMS che sono anche in AEM possono essere aggiunti a questi gruppi singolarmente, ma per farlo in blocco richiede un passaggio aggiuntivo.  Di seguito è riportato un modo in cui è possibile eseguire questa operazione:
* Crea uno o più nuovi gruppi in Admin Console/IMS per accedere alle raccolte e configurali per AEM.
* Accedi come membro del gruppo o dei gruppi in modo che vengano creati in AEM.
* Per le raccolte migrate, utilizza l’interfaccia utente Raccolte di risorse per aggiungere il nuovo gruppo come editor/proprietario/visualizzatore.
* Aggiungi utenti (o carica in blocco) ai nuovi gruppi in Admin Console.
* Quando l’utente accede per la prima volta, il relativo utente IMS verrà creato in AEM e deve avere accesso ai nuovi gruppi e quindi ai gruppi di raccolta originali.

Nota: per l’assegnazione in blocco degli utenti, è necessario utilizzare i passaggi precedenti per creare gli utenti in IMS. Gli utenti già esistenti in IMS non possono essere creati nuovamente tramite il caricamento in blocco.
