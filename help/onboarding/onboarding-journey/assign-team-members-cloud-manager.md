---
title: 'Assegnazione di membri del team ai profili di prodotto di Cloud Manager '
description: Segui questa pagina per scoprire come assegnare i membri del team ai profili di prodotto di Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 8b30fc9494e152aa742cf17c02f982f5c9479473
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---


# Assegnazione di membri del team ai profili di prodotto di Cloud Manager {#assign-team-members}

Dopo aver appreso come accedere ad Admin Console e aver visualizzato i privilegi di amministratore di sistema, ora puoi assegnare i membri del team ai profili di prodotto di Cloud Manager.

## Obiettivo {#objective}

In questo documento viene riepilogato come assegnare i membri del team ai profili di prodotto di Cloud Manager dall’Admin Console.

Dopo aver letto questa sezione dovresti essere in grado di:

* Scopri perché e come aggiungere i membri del team.
* Scopri tre diversi profili di prodotto di Cloud Manager, ad esempio Proprietario business, Manager distribuzione e Sviluppatore.
* Assegna i membri del team ai profili di prodotto di Cloud Manager (Business Owner, Deployment Manager e Developer).

## Esamina i profili di prodotto di Cloud Manager {#review-product-profiles}

Dall’Admin Console è possibile visualizzare l’elenco dei profili di Cloud Manager.

>[!NOTE]
>Prima di esaminare i profili di prodotto di Cloud Manager da Admin Console, si consiglia di esaminare i profili di prodotto di Cloud Manager disponibili.

Per visualizzare l’elenco dei profili di Cloud Manager, effettua le seguenti operazioni:

1. Accedi a Adobe Admin Console. Dalla pagina **Panoramica** , seleziona Adobe Experience Manager as a Cloud Service dalla scheda Prodotti e servizi .

   >[!NOTE]
   >Per informazioni su come utilizzare Admin Console, consulta Accesso ad Admin Console .


1. Passa all’istanza di cloud manager dalla tabella con l’elenco di tutte le istanze. Verrà visualizzato l’elenco dei profili di prodotto Cloud Manager preconfigurati.


## Assegnare utenti al profilo di prodotto proprietario business {#assign-users-business-owner}

Ora puoi aggiungere utenti e assegnarli al profilo di prodotto Proprietario business di Cloud Manager.

Per eseguire correttamente questa operazione, da Admin Console di Adobe devi aggiungere un utente sia al prodotto (AEM come Cloud Service in questo caso) che al profilo di prodotto Business Owner di Cloud Manager.

I seguenti passaggi ti guideranno attraverso questo:

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Proprietario business. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina Panoramica Admin Console , seleziona Adobe Experience Manager come prodotto di Cloud Service dalla scheda prodotti e servizi come mostrato di seguito:

1. Seleziona la scheda Utenti dalla navigazione in alto, quindi seleziona Aggiungi utente .

1. Nella finestra di dialogo aggiungi utente, digita l’ID e-mail dell’utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

1. Nella selezione del prodotto, seleziona &quot;Adobe Experience Manager as a Cloud Service&quot; e assegna il profilo di prodotto &quot;Business Owner&quot; all’utente come mostrato di seguito. Fai riferimento ai profili di prodotto di Cloud Manager per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell’Admin Console, come mostrato di seguito.

1. Assegna l’utente ad almeno un profilo di prodotto in modo che l’utente possa accedere a Cloud Manager. Ricordarsi di assegnarsi (amministratore di sistema) a &quot;Proprietario business&quot;.

1. Fai clic su Salva. Viene inviata un’e-mail di benvenuto all’utente aggiunto. L’utente invitato può accedere a Cloud Manager facendo clic sul collegamento presente nell’e-mail di benvenuto e accedendo utilizzando il proprio Adobe ID.

Congratulazioni! Ora è stato configurato il team Cloud Manager di nuova formazione, incluso l’utente assegnato al ruolo &quot;Proprietario business&quot;. I membri riceveranno un’e-mail di benvenuto che li invita ad accedere e ad accedere a Cloud Manager. Nel ruolo di Business Owner (Proprietario business), ora sei a solo un passo dall’accesso a Cloud Manager e dall’abilitazione della creazione delle risorse cloud.

## Assegnare utenti al profilo di prodotto di Deployment Manager {#assign-users-deployment-manager}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Proprietario business. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina Panoramica Admin Console , seleziona Adobe Experience Manager come prodotto di Cloud Service dalla scheda prodotti e servizi come mostrato di seguito:

1. Seleziona la scheda Utenti dalla navigazione in alto, quindi seleziona Aggiungi utente .

1. Nella finestra di dialogo aggiungi utente, digita l’ID e-mail dell’utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

1. Nella selezione del prodotto, seleziona &quot;Adobe Experience Manager as a Cloud Service&quot; e assegna il profilo di prodotto &quot;Deployment Manager&quot; all’utente come mostrato di seguito. Fai riferimento ai profili di prodotto di Cloud Manager per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell’Admin Console, come mostrato di seguito.

   >[!NOTE]
   >Puoi aggiungere l’utente al profilo di prodotto di Deployment Manager dopo la creazione delle risorse di Cloud Manager.

## Assegnare utenti al profilo di prodotto per sviluppatori {#assign-users-developer}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Proprietario business. L’amministratore di sistema deve essere la prima persona ad accedere e accedere a Cloud Manager. Devi prima aggiungerti (amministratore di sistema) al profilo di prodotto Proprietario business.

1. Nella pagina Panoramica Admin Console , seleziona Adobe Experience Manager come prodotto di Cloud Service dalla scheda prodotti e servizi come mostrato di seguito:

1. Seleziona la scheda Utenti dalla navigazione in alto, quindi seleziona Aggiungi utente .

1. Nella finestra di dialogo aggiungi utente, digita l’ID e-mail dell’utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

1. Nella selezione del prodotto, seleziona &quot;Adobe Experience Manager as a Cloud Service&quot; e assegna il profilo di prodotto &quot;Sviluppatore&quot; all’utente come mostrato di seguito. Fai riferimento ai profili di prodotto di Cloud Manager per assicurarti che agli utenti giusti siano assegnati i ruoli giusti nell’Admin Console, come mostrato di seguito.

   >[!NOTE]
   >Puoi aggiungere un utente al profilo di prodotto Sviluppatore dopo la creazione delle risorse di Cloud Manager.

## Novità {#whats-next}

In qualità di amministratore di sistema assegnato al ruolo *Proprietario business* , devi accedere a Cloud Manager e accedervi.
>[!NOTE]
>Per informazioni su come accedere e accedere a Cloud Manager, consulta Navigazione in Cloud Manager .

Un utente di Cloud Manager con il ruolo Proprietario business può accedere e configurare le risorse cloud, inclusi i programmi e gli ambienti. In questo modo, il team di esperti potrà iniziare ad accedere al AEM il prima possibile.
Dopo che il proprietario business ha configurato le risorse cloud, gli sviluppatori e i gestori di distribuzione che sono stati aggiunti con successo ai profili di prodotto di Cloud Manager possono accedere a Cloud Manager e acquisire familiarità con le modalità per continuare il loro percorso di apprendimento.

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* Cloud Manager
* Profili di prodotto di Cloud Manager
* Panoramica su Admin Console Identity
