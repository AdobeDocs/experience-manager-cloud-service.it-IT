---
title: Creare una comunicazione interattiva
description: Creare comunicazioni personalizzate e basate su dati. Esplora le funzioni chiave, i passaggi di onboarding e i casi d’uso reali con guide e tutorial.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 5dd94d22a2a1a2ddbfd7dee44e93e6ea0c4b7ad9
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Creare una comunicazione interattiva

La comunicazione interattiva ti consente di creare, gestire e distribuire comunicazioni personalizzate e interattive, tra cui servizio clienti, fatturazione, documenti di onboarding, lettere di offerta, aggiornamenti dell’account e altro ancora. È progettato per supportare qualsiasi scenario in cui contenuti dinamici e specifici per l’utente migliorino l’esperienza di comunicazione nei diversi settori.

Immagina di dover inviare un estratto conto bancario, una polizza assicurativa o una bolletta per migliaia di clienti. Ognuno ha lo stesso layout ma dati personalizzati. La comunicazione interattiva (IC) rende questo possibile in modo efficiente.

![Trova documento IC](/help/forms/interactive-communication/assets/Picture1.png)

La produzione manuale di questi documenti può richiedere molto tempo e spesso genera incoerenze, soprattutto quando sono necessarie personalizzazione e integrazione dei dati. Con l’Editor di comunicazione interattiva, gli utenti possono semplificare il processo di creazione della comunicazione interattiva.

## Prerequisito

* [Assicurati che l’autore sia un membro del gruppo utenti dei moduli](/help/forms/setup-forms-cloud-service.md#configure-users)

## Creare una comunicazione interattiva

Scegli tra diversi scenari per creare una comunicazione interattiva, in base al livello di riutilizzo e di integrazione dei dati richiesti:

+++ Creare una comunicazione interattiva vuota

La creazione di una comunicazione interattiva vuota ti consente di iniziare da zero, ideale quando desideri un controllo completo su layout, struttura e logica.
Passaggi successivi:

1. Apri l&#39;istanza di Forms as a Cloud Service **Adobe Experience Manager (AEM)**.
1. Passa a **Forms > Forms e documenti**.
1. Fai clic su **Crea > Comunicazione interattiva**.

   ![Trova documento IC](/help/forms/interactive-communication/assets/comm.png)

1. Nella schermata di creazione, lascia vuoto il campo **Modello**.

   ![Trova documento IC](/help/forms/interactive-communication/assets/create-ic-document.png)

1. Compila altri dettagli come Titolo, Nome, Autore, ecc.
1. Fai clic su **Crea** per accedere all&#39;interfaccia utente dell&#39;editor di comunicazioni interattive e iniziare la progettazione.
1. Viene aperto l&#39;editor IC, in cui è possibile iniziare a progettare la comunicazione.
+++

+++ Creare una comunicazione interattiva basata su modelli

L’utilizzo di un modello consente di velocizzare la progettazione riutilizzando elementi di layout coerenti come intestazioni, piè di pagina, loghi o formattazione standard.
I modelli garantiscono la coerenza del marchio e consentono di risparmiare tempo per i tipi di comunicazione più comunemente utilizzati. Effettua le seguenti operazioni:

1. Apri l’istanza di AEM Forms as a Cloud Service.
1. Vai a **Forms > Forms &amp; Documents**, fai clic su **Crea > Comunicazione interattiva**.
1. Nel modulo di creazione, **seleziona** un modello abilitato dal menu a discesa.
1. Compila altri dettagli come Titolo, Nome, Autore, ecc.
1. Fai clic su **Crea** per progettare la comunicazione con la struttura di modelli selezionata.
1. Viene aperto l&#39;editor IC, in cui è possibile iniziare a progettare la comunicazione.
+++

+++ Creare una comunicazione interattiva con interazione dei dati

Le comunicazioni con interazione dei dati personalizzano automaticamente il contenuto utilizzando dati di back-end.
Ideale per rendiconti, fatture o avvisi in cui la struttura rimane costante, ma i dati variano in base al destinatario. Passaggi successivi:

1. Apri l’istanza di AEM Forms as a Cloud Service.
1. Vai a **Forms > Forms &amp; Documents**, fai clic su **Crea > Comunicazione interattiva**.
1. Nel campo **Modello dati modulo**, collega il **FDM (Modello dati modulo) predefinito**.
1. Compila altri dettagli come Titolo, Nome, Autore, ecc.
1. Utilizza **Modello dati** all&#39;interno dell&#39;editor per associare i campi ai dati dinamici (ad esempio, nome cliente, saldo, numero account).
1. Utilizza **Aree di contenuto, Sottomoduli** e **Frammenti** per strutturare e ripetere i dati quando necessario.
1. Anteprima tramite **Anteprima PDF** e finalizzazione della comunicazione per la consegna.
1. Viene aperto l&#39;editor IC, in cui è possibile iniziare a progettare la comunicazione.

![Trova documento IC](/help/forms/interactive-communication/assets/ic-ui.png)
+++

Inizia a creare comunicazioni interattive per semplificare i flussi di lavoro e fornire esperienze significative e specifiche per gli utenti.

## Passaggi successivi

[Crea un modello di comunicazione interattivo](/help/forms/interactive-communication/create-interactive-communication-template.md)
[Crea un frammento di comunicazione interattivo](/help/forms/interactive-communication/create-interactive-communication-fragment.md)
