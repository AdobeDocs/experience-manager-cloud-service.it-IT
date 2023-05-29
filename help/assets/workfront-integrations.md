---
title: '[!DNL Experience Manager Assets] integrazione con [!DNL Adobe Workfront]'
description: Introduzione all’integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 5da4be3ec9af6a00cce8d80b8eea7f7520754a1d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] integrazione con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Workfront] è un’applicazione per la gestione dell’intero ciclo di vita del lavoro, tutto in un’unica posizione. L’integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di velocizzare le attività relative ai contenuti e il time-to-market, grazie a un collegamento intrinseco tra il lavoro e la gestione delle risorse digitali. Nel contesto della gestione del proprio lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini richiesti.

Adobe di offerte a [integrare [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] in modalità nativa (supporto di Assets Essentials e Assets as a Cloud Service) o utilizzando il connettore avanzato di Workfront ad Experience Manager](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). In caso di integrazione nativa, non è necessario un connettore per integrare le due soluzioni.

>[!NOTE]
>
>Adobe non supporta l’utilizzo parallelo di Workfront per il connettore avanzato Experience Manager e l’integrazione Experience Manager.

Con l&#39;integrazione nativa di Experience Manager e [!DNL Workfront for Experience Manager enhanced connector], è possibile:

| Nativa [!DNL Adobe Experience Manager Assets] funzioni | [!DNL Workfront for Experience Manager enhanced connector] funzioni |
|---|---|
| <ul><li>Configurazione rapida dell&#39;integrazione all&#39;interno di Workfront.</li><li>Creazione automatica di cartelle collegate tra Workfront e Experience Manager.</li><li>Sincronizza facilmente i metadati per le risorse collegate esistenti.</li><li>Aggiorna automaticamente i metadati del progetto quando vengono modificati in Workfront.</li><li>Collega in modo semplice più archivi Experience Manager Assets a un ambiente Workfront o più ambienti Workfront a un archivio Experience Manager Assets tra gli ID organizzazione.</li> | <ul><li>Creazione automatica di cartelle di Experienci Manager collegate in Workfront e organizzazione delle cartelle in base a Portfoli, programmi e progetti Workfront.</li><li>Sincronizza i metadati del progetto Workfront con le cartelle di Experienci Manager collegate.</li><li>Experience Manager di aggiornamenti dei metadati con nuove versioni.</li><li>Imposta gli stati degli oggetti di Workfront in base a condizioni configurabili utilizzando flussi di lavoro di Experience Manager.</li><li>Pubblicare risorse in un ambiente di pubblicazione Experience Manager o in Brand Portal.</li> |

Consulta la [funzioni supportate di seguito per un confronto](#feature-parity-matrix) tra un’integrazione nativa o un’integrazione tramite connettori tra le due soluzioni.



Consulta Supporto della piattaforma e [prerequisiti per il connettore avanzato](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* L’Adobe richiede l’implementazione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono questo connettore ridondante; in tal caso, i clienti potrebbero dover passare dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, vedere il punto 5(a) di [istruzioni per l&#39;installazione del connettore avanzato](workfront-connector-install.md).
>
>* Consulta [Connettore avanzato per la certificazione dei partner per Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Confrontare diverse integrazioni tra [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Di seguito sono riportati i dettagli delle funzionalità disponibili tramite vari tipi di integrazioni tra [!DNL Assets] e [!DNL Workfront].

| Funzione obsoleta | Descrizione | [!DNL Workfront] e [!DNL Assets Essentials] *Nessun connettore (OTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Richiede il connettore* | WORKFRONT e [!DNL Experience Manager as a Cloud Service] *Nessun connettore (OTB)* |
|----|----|----|-----|-----|
| Metodi di implementazione | Appropriato per cui [!DNL Assets] offerta. | Assets Essentials | Adobe Managed Services, On-Premise | Servizio cloud |
| **Generale** |
| Invia file digitali da [!DNL Workfront] a [!DNL Assets] | L’ultima versione di un documento WF può essere caricata in AEM Assets e collegata come nuova versione del documento. | ✓ | ✓ | ✓ |
| Collegare manualmente le cartelle AEM agli oggetti Workfront | Le cartelle AEM esistenti possono essere collegate come una cartella Workfront e le relative risorse secondarie vengono collegate come nuovi documenti Workfront. | ✓ | ✓ | ✓ |
| Collegamento [!DNL Assets] a oggetti Workfront | Le risorse esistenti in AEM possono essere collegate a un nuovo documento Workfront o come nuova versione di un documento esistente. | ✓ | ✓ | ✓ |
| Le risorse aggiunte alle cartelle collegate vengono inviate automaticamente all’AEM | Se un documento viene aggiunto a una cartella collegata, la risorsa associata viene caricata automaticamente in AEM Assets come nuova risorsa. | ✓ | ✓ | ✓ |
| Scaricare Linked AEM Assets da Workfront | Quando una risorsa è collegata in Workfront, l’utente può scaricarne i byte. | ✓ | ✓ | ✓ |
| Cerca AEM Assets da Workfront | Il selettore AEM Assets in Workfront consente ricerche full-text nelle risorse. | ✓ | ✓ | ✓ |
| Cerca cartelle AEM da Workfront | Il selettore AEM Assets in Workfront consente ricerche full-text nelle cartelle. | ✓ | ✓ | ✓ |
| Visualizzare e navigare nella gerarchia di cartelle AEM da Workfront | Il selettore AEM Assets in Workfront consente di esplorare la gerarchia AEM Assets limitata dai controlli di accesso e dalle autorizzazioni associati dell’utente impostati in AEM. | ✓ | ✓ | ✓ |
| Tracciare le versioni delle risorse nelle timeline AEM | Gestisce la cronologia delle versioni dei documenti tra Workfront e AEM. | ✓ | ✓ | ✓ |
| Scollegare risorse da AEM Assets in Workfront | È possibile scollegare una risorsa collegata esistente dall’AEM dal documento Workfront associato. Ciò non elimina la risorsa originale all’interno dell’AEM. | ✓ | ✓ | ✓ |
| Aggiungi risorsa con nuove versioni ad AEM Assets da Workfront | Quando in Workfront viene aggiunta una nuova versione a un documento, l’utente può inviare la nuova versione all’AEM per sostituirla. | ✓ | ✓ | ✓ |
| Risorse collegate in Workfront quando si fa clic su Utente diretto all’AEM | Gli utenti vengono indirizzati all’AEM per visualizzare in anteprima una risorsa collegata da Workfront. | ✓ | ✓ | Prossimo |
| Creazione automatica di cartelle AEM collegate in Workfront | Creazione automatica di cartelle AEM collegate in Workfront utilizzando gli stati del progetto. Configurare automaticamente le cartelle AEM in base ai Portfoli, ai programmi e ai progetti Workfront. | No | ✓ | No |
| Passa direttamente agli archivi AEM da Workfront | Consenti agli utenti di passare agli archivi AEM disponibili configurati in Workfront. | ✓ | No | ✓ |
| Creare cartelle AEM collegate in Workfront | Crea manualmente cartelle AEM collegate in Workfront utilizzando l’opzione disponibile nella scheda Documenti. | ✓ | No | ✓ |
| Sincronizzazione commenti | Sincronizza automaticamente i commenti per le risorse da [!DNL Workfront] a [!DNL Assets] | No | ✓ | No |
| Supporto di più ambienti Workfront collegati a un unico ambiente AEM | Gli utenti di più ambienti Workfront possono connettersi a un unico ambiente AEM. | ✓ | No | ✓ |
| Supporto di più ambienti AEM collegati a un unico ambiente Workfront | Gli utenti all’interno di un singolo ambiente Workfront possono inviare o collegare risorse tra più ambienti AEM. | ✓ | ✓ | ✓ |
| **Metadati** |
| Mappare i metadati delle risorse Workfront su AEM Assets | Le proprietà dell’oggetto Workfront e del modulo personalizzato possono essere mappate alle proprietà dei metadati delle risorse AEM. I valori verranno inviati al caricamento/collegamento iniziale. | ✓ | ✓ | ✓ |
| Creazione automatica di un documento Forms personalizzato in Workfront | Allega i moduli personalizzati ai documenti, alle attività e ai problemi di Workfront utilizzando i flussi di lavoro AEM. | No | ✓ | No |
| Aggiornamento automatico bidirezionale dei metadati tra AEM Assets e Workfront | Aggiorna automaticamente i metadati tra AEM Assets e Workfront. La risorsa deve essere inizialmente inviata da Workfront all’AEM e i metadati della risorsa Workfront devono essere mappati sulle risorse AEM affinché gli aggiornamenti bidirezionali dei metadati funzionino correttamente. | No | ✓ | No |
| Visualizzazione in tempo reale in Workfront per metadati mappati su AEM | Visualizzare i metadati mappati aggiornati all’AEM nei pannelli Dettagli documento e Riepilogo documento di Workfront. | ✓ | No | ✓ |
| Invio in tempo reale di metadati Workfront aggiornati all’AEM | Aggiorna automaticamente all’AEM i metadati Workfront mappati senza eseguire il repushing di una risorsa o di una nuova versione di una risorsa. | ✓ | No | ✓ |
| Mappare i metadati di Workfront alle cartelle di AEM Assets | Sincronizza i metadati del progetto Workfront con le cartelle AEM collegate. | No | ✓ | ✓ |
| Aggiornamenti dei metadati AEM con nuove versioni | È possibile effettuare una configurazione in AEM per determinare se anche una risorsa con nuove versioni in Workfront deve essere sottoposta a push a seguito di eventuali modifiche apportate ai relativi metadati. | No | ✓ | No |
| Aggiornamento automatico dei metadati AEM in caso di modifiche al Forms personalizzato in Workfront | AEM consente di iscriversi agli aggiornamenti ai moduli dei documenti in Workfront. Di conseguenza, eventuali aggiornamenti ai metadati del modulo personalizzato del documento di Workfront modificano i valori dei campi di metadati dell’AEM mappati. | No | ✓ | No |
| **Flussi di lavoro (pronti all’uso)** |
| Creare una nuova versione di bozza su risorse collegate | Quando si collega una risorsa in Workfront, è possibile generare automaticamente una bozza. | No | Personalizzati | No |
| Imposta stato su oggetti Workfront | Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite flussi di lavoro AEM | No | ✓ | Prossimo |
| Pubblicare risorse in AEM Publish Environment o Brand Portal | Offri agli utenti di Workfront la possibilità di pubblicare automaticamente le risorse collegate in un ambiente di pubblicazione AEM o in un Brand Portal. | No | ✓ | Prossimo |
