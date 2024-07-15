---
title: Utilizzo di Content Transformer
description: Scopri come trasformare la struttura dei contenuti in preparazione alla migrazione ad AEM as a Cloud Service.
exl-id: 40516ff7-5686-42e6-bdd1-c9c6de432b09
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Utilizzo di Content Transformer {#using-ct}

## Considerazioni importanti sull’utilizzo di Content Transformer {#imp-considerations-ct}

Leggi la sezione seguente per comprendere le considerazioni importanti sull’utilizzo del Content Transformer (CT):

* Per utilizzare Content Transformer, devi prima eseguire Best Practices Analyzer nell’ambiente Adobe Experience Manager (AEM).
* Anche se è possibile eseguire Content Transformer nell’ambiente di produzione, si consiglia di eseguirlo su un clone dell’ambiente di produzione. È importante assicurarsi che BPA e CT vengano eseguiti nello stesso ambiente.
* Devi essere un amministratore dell’ambiente in cui desideri eseguire Content Transformer.
* Qualsiasi operazione che possa modificare il contenuto di origine ( sposta/rimuovi/rinomina ) per impostazione predefinita creerà un pacchetto di backup dei percorsi di origine in `/etc/packages/content-transformation` prima della trasformazione. Sebbene ogni finestra di dialogo delle operazioni disponga di un’opzione per disabilitare/abilitare la creazione dei pacchetti di backup, si consiglia rigorosamente di selezionare sempre l’opzione per abilitare la creazione dei pacchetti.
* Ogni pagina nel Content Transformer è configurata per elencare un massimo di 50 risultati, quindi alla volta è possibile trasformare un massimo di 50 risultati. Questa operazione viene eseguita per fornire una risposta tempestiva nell’interfaccia utente.

## Disponibilità {#availability-ct}

Il Content Transformer è incluso con lo [strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) che può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nell’istanza AEM di origine.

>[!NOTE]
>Content Transformer è disponibile con lo strumento Content Transfer v2.0.20 o versione successiva.

## Apertura di Content Transformer {#opening-ct}

1. Accedi all’istanza AEM di origine come amministratore e passa alla pagina iniziale: https://host:port/aem/start.html.
1. Passa a Strumenti > Operazioni > Migrazione contenuti

   ![immagine](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > Assicurati di aver eseguito il rapporto BPA in precedenza e verificalo con l’URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html

1. Fai clic sulla scheda con il titolo **Content Transformer for BPA report**

   ![immagine](/help/journey-migration/content-transformer/assets/ct-2.png)

   Di seguito è riportato un esempio di come si presenterà la pagina Panoramica di Content Transformer se la creazione del rapporto BPA ha avuto esito positivo e se sono stati riscontrati problemi relativi al contenuto.

   Il tempo di scadenza rimasto per il rapporto BPA viene visualizzato sulla barra laterale. Si consiglia di eseguire Content Transformer con il report BPA più recente per evitare di perdere risultati relativi al contenuto.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-3.png)

1. È possibile filtrare i problemi in base a `Pattern Code`, `Subtype`, `Importance` e `Source`.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-4.png)

1. Puoi selezionare tutti i problemi o problemi specifici e spostarli, rimuoverli o rinominarli per risolverli. Puoi aggiungere percorsi personalizzati anche utilizzando il pulsante **Aggiungi percorsi** nell&#39;angolo in alto a destra.

   >[!NOTE]
   > Quando si utilizza l&#39;operazione di spostamento, si consiglia di spostare tutti i percorsi in una sola cartella (ad esempio, in `/etc/packages/content-transformation/paths`), pertanto quando i pacchetti di backup vengono installati per riportare l&#39;istanza allo stato originale, è possibile eliminare la cartella (`/etc/packages/content-transformation/paths`) tramite l&#39;operazione di rimozione per ridurre le dimensioni dell&#39;archivio.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![immagine](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > Qualsiasi operazione in grado di modificare il contenuto di origine (`move`/`remove`/`rename`) creerà per impostazione predefinita un pacchetto di backup dei percorsi di origine in `/etc/packages/content-transformation` prima della trasformazione. Sebbene ogni finestra di dialogo delle operazioni disponga di un’opzione per disabilitare/abilitare la creazione dei pacchetti di backup, si consiglia rigorosamente di selezionare sempre l’opzione per abilitare la creazione dei pacchetti.

1. Di seguito è riportato un esempio di pacchetto di backup creato per l’operazione di spostamento dei percorsi. Fai clic su Installa per ripristinare i percorsi sorgente. L’installazione riporta solo i percorsi sorgente nella posizione originale e non elimina i percorsi in cui sono stati spostati durante la trasformazione. Per eliminare i percorsi nel percorso spostato, fare clic sul pulsante **Aggiungi percorsi** per aggiungere il percorso, ad esempio `/etc/packages/content-transformation/paths`, selezionare il percorso e fare clic su **Rimuovi**.

   >[!CAUTION]
   > Non eliminare `/etc/packages/content-transformation` perché è il percorso in cui risiedono i pacchetti di backup. Solo quando sei sicuro di non aver più bisogno di questi pacchetti, puoi eliminare questa posizione per ridurre le dimensioni dell’archivio.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![immagine](/help/journey-migration/content-transformer/assets/ct-8.png)
