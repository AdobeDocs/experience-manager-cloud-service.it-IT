---
title: '[!DNL Experience Manager Assets] integrazione con [!DNL Adobe Workfront]'
description: Introduzione all'integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 1631ec4b7174c9d98747fe290e21db3839777fcb
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] come [!DNL Cloud Service] [!DNL Assets] integrazione con [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] è un’applicazione per la gestione dell’intero ciclo di vita del lavoro, tutto in un’unica posizione. Integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di migliorare la velocità dei contenuti e il time-to-market collegando intrinsecamente il lavoro e la gestione delle risorse digitali. Nel contesto della gestione del lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini richiesti.

Adobe di offerte a [integrare [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] nativo (con supporto di Assets Essentials e Assets as a Cloud Service) o utilizzo di Workfront per Experience Manager, connettore avanzato](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). In caso di integrazione nativa, non è necessario un connettore per integrare le due soluzioni.

>[!NOTE]
>
>Adobe non supporta l’utilizzo in parallelo di Workfront, ad Experience Manager un connettore avanzato e l’integrazione con Experience Manager.

Con l’integrazione nativa Experience Manager e [!DNL Workfront for Experience Manager enhanced connector], puoi:

| Nativo [!DNL Adobe Experience Manager Assets] caratteristiche | [!DNL Workfront for Experience Manager enhanced connector] caratteristiche |
|---|---|
| <ul><li>Configura rapidamente l’integrazione all’interno di Workfront.</li><li>Crea automaticamente cartelle collegate tra Workfront e Experience Manager.</li><li>Sincronizza facilmente i metadati per le risorse collegate esistenti.</li><li>Aggiorna automaticamente i metadati del progetto quando viene modificato in Workfront.</li><li>Collega facilmente diversi archivi Experience Manager Assets a un ambiente Workfront o a più ambienti Workfront a un archivio Experience Manager Assets in tutti gli ID organizzazione.</li> | <ul><li>Crea automaticamente cartelle di Experienci Manager collegate in Workfront e organizza le cartelle in base a Portfoli, programmi e progetti Workfront.</li><li>Sincronizza i metadati del progetto Workfront con le cartelle di Experience Manager collegate.</li><li>Experience Manager di aggiornamenti dei metadati con nuove versioni.</li><li>Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite i flussi di lavoro Experience Manager.</li><li>Pubblicare risorse nell’ambiente di pubblicazione Experience Manager o in Brand Portal.</li> |

Consulta la sezione [funzioni supportate di seguito per un confronto](#feature-parity-matrix) tra l’integrazione nativa o un’integrazione utilizzando i connettori tra le due soluzioni.



Consulta il supporto per la piattaforma e [prerequisiti per il connettore avanzato](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* L&#39;Adobe richiede la distribuzione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono tale connettore ridondante; in questo caso, potrebbe essere richiesto ai clienti di effettuare la transizione dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni di connettore avanzate 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, vedi il punto 5, lettera a), del [istruzioni per l&#39;installazione di un connettore avanzato](workfront-connector-install.md).
>
>* Vedi [Esame di certificazione dei partner per Workfront per il connettore avanzato Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedi [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Confrontare diverse integrazioni tra [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Di seguito sono riportati i dettagli delle funzionalità disponibili attraverso vari tipi di integrazioni tra [!DNL Assets] e [!DNL Workfront].

| Funzione obsoleta | Descrizione | [!DNL Workfront] e [!DNL Assets Essentials] *Nessun connettore (OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Richiede connettore* | Workfront e [!DNL Experience Manager as a Cloud Service] *Nessun connettore (OOTB)* |
|----|----|----|-----|-----|
| Metodi di distribuzione | Adeguata per la quale [!DNL Assets] offerta. | Assets Essentials | Adobe Managed Services, on-premise | Servizio cloud |
| **Generale** |
| Invia file digitali da [!DNL Workfront] a [!DNL Assets] | È possibile caricare in AEM Assets l’ultima versione di un documento WF, che verrà collegata come nuova versione del documento. | ✓ | ✓ | ✓ |
| Collegamento manuale di cartelle AEM a oggetti Workfront | Le cartelle AEM esistenti possono essere collegate come cartella Workfront e le relative risorse secondarie sono collegate come nuovi documenti Workfront. | ✓ | ✓ | ✓ |
| Collegamento [!DNL Assets] a oggetti Workfront | Le risorse esistenti in AEM possono essere collegate a un nuovo documento Workfront o a una nuova versione di un documento esistente. | ✓ | ✓ | ✓ |
| Le risorse aggiunte alle cartelle collegate vengono inviate automaticamente a AEM | Se il documento viene aggiunto a una cartella collegata, la risorsa associata viene caricata automaticamente in AEM Assets come nuova risorsa. | ✓ | ✓ | ✓ |
| Scarica AEM Assets collegato da Workfront | Quando una risorsa è collegata in Workfront, l&#39;utente può scaricare i byte della risorsa. | ✓ | ✓ | ✓ |
| Ricerca di AEM Assets da Workfront | Il selettore AEM Assets in Workfront consente la ricerca full-text delle risorse. | ✓ | ✓ | ✓ |
| Ricerca di cartelle AEM in Workfront | Il selettore AEM Assets in Workfront consente ricerche full-text per le cartelle. | ✓ | ✓ | ✓ |
| Visualizza e naviga AEM gerarchia cartelle da Workfront | Il selettore AEM Assets in Workfront consente di esplorare la gerarchia AEM Assets limitata dai controlli di accesso e dalle autorizzazioni associati dell’utente impostati in AEM. | ✓ | ✓ | ✓ |
| Tracciare le versioni di Assets nelle timeline AEM | Gestisci la cronologia della versione del documento tra Workfront e AEM. | ✓ | ✓ | ✓ |
| Scollegare risorse da AEM Assets in Workfront | Una risorsa collegata esistente da AEM può essere scollegata dal documento Workfront associato. La risorsa originale non viene eliminata all’interno di AEM. | ✓ | ✓ | ✓ |
| Aggiungere una risorsa di nuova versione ad AEM Assets da Workfront | Quando in un documento di Workfront viene aggiunta una nuova versione, un utente può inviare la nuova versione per AEM per sostituire la versione esistente. | ✓ | ✓ | ✓ |
| Risorse collegate in Workfront quando si fa clic su Utente diretto in AEM | Gli utenti vengono invitati a AEM di visualizzare in anteprima una risorsa collegata da Workfront. | ✓ | ✓ | Prossima |
| Crea automaticamente cartelle AEM collegate in Workfront | Crea automaticamente cartelle AEM collegate in Workfront utilizzando gli stati del progetto. Configura automaticamente AEM cartelle in base a Portfoli, programmi e progetti Workfront. | No | ✓ | No |
| Passa direttamente agli archivi AEM da Workfront | Consente agli utenti di passare agli archivi AEM disponibili configurati in Workfront. | ✓ | No | ✓ |
| Creare cartelle AEM collegate in Workfront | Creare manualmente cartelle AEM collegate in Workfront utilizzando l’opzione disponibile nella scheda Documenti. | ✓ | No | ✓ |
| Sincronizzazione dei commenti | Sincronizza automaticamente i commenti delle risorse da [!DNL Workfront] a [!DNL Assets] | No | ✓ | No |
| Supporto di più ambienti Workfront che si connettono a un unico ambiente AEM | Gli utenti di più ambienti Workfront possono connettersi a un singolo ambiente AEM. | ✓ | No | ✓ |
| Supporto di più ambienti AEM che si connettono a un unico ambiente Workfront | Gli utenti all’interno di un singolo ambiente Workfront possono inviare o collegare risorse tra più ambienti AEM. | ✓ | ✓ | ✓ |
| **Metadati** |
| Mappatura dei metadati delle risorse Workfront su AEM Assets | Le proprietà dell’oggetto Workfront e del modulo personalizzato possono essere mappate AEM proprietà dei metadati delle risorse. I valori verranno inviati al caricamento/collegamento iniziale. | ✓ | ✓ | ✓ |
| Crea automaticamente un documento personalizzato Forms in Workfront | Allegare moduli personalizzati a documenti, attività e problemi di Workfront utilizzando i flussi di lavoro AEM. | No | ✓ | No |
| Aggiornamento automatico bidirezionale dei metadati tra AEM Assets e Workfront | Aggiorna automaticamente i metadati tra AEM Assets e Workfront. La risorsa deve essere inizialmente inviata da Workfront a AEM e i metadati della risorsa Workfront devono essere mappati su AEM risorse per il corretto funzionamento degli aggiornamenti dei metadati bidirezionali. | No | ✓ | No |
| Visualizzazione in tempo reale in Workfront per metadati mappati a AEM | Visualizza i metadati mappati aggiornati da AEM nei pannelli Dettagli documento e Riepilogo documento di Workfront. | ✓ | No | ✓ |
| Invio in tempo reale di metadati Workfront aggiornati a AEM | Aggiorna automaticamente i metadati Workfront mappati in AEM senza dover ripetere l&#39;invio di una risorsa o di una nuova versione di una risorsa. | ✓ | No | ✓ |
| Mappare metadati Workfront nelle cartelle AEM Assets | Sincronizza i metadati del progetto Workfront con le cartelle AEM collegate. | No | ✓ | ✓ |
| Aggiornamenti AEM metadati con nuove versioni | È possibile effettuare una configurazione in AEM per determinare se una risorsa con nuove versioni in Workfront invia anche le modifiche apportate ai suoi metadati. | No | ✓ | No |
| Aggiorna automaticamente i metadati AEM in caso di modifiche a Forms personalizzato in Workfront | AEM ti consente di abbonarti agli aggiornamenti dei moduli del documento in Workfront. Di conseguenza, qualsiasi aggiornamento dei metadati del modulo personalizzato del documento Workfront modifica i valori dei campi di metadati AEM mappati. | No | ✓ | No |
| **Flussi di lavoro (preconfigurati)** |
| Creare una nuova versione di prova sulle risorse collegate | Al collegamento di una risorsa in Workfront è possibile generare automaticamente una bozza. | No | Personalizzati | No |
| Imposta stato su oggetti Workfront | Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite flussi di lavoro AEM | No | ✓ | Prossima |
| Pubblicare risorse in AEM Publish Environment o Brand Portal | Consenti agli utenti di Workfront di pubblicare automaticamente le risorse collegate in un ambiente di pubblicazione AEM o Brand Portal. | No | ✓ | Prossima |
