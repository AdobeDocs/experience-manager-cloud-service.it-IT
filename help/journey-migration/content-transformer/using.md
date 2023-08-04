---
title: Utilizzo del trasformatore di contenuti
description: Scopri come trasformare la struttura dei contenuti in preparazione alla migrazione a AEM as a Cloud Service.
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# Utilizzo del trasformatore di contenuti {#using-ct}

## Considerazioni importanti sull’utilizzo di Content Transformer {#imp-considerations-ct}

Leggi la sezione seguente per comprendere le considerazioni importanti sull’utilizzo del Content Transformer (CT):

* Per utilizzare Content Transformer, devi prima eseguire Best Practices Analyzer nell’ambiente Adobe Experience Manager (AEM).
* Anche se è possibile eseguire Content Transformer nell’ambiente di produzione, si consiglia di eseguirlo su un clone dell’ambiente di produzione. È importante assicurarsi che BPA e CT vengano eseguiti nello stesso ambiente.
* Devi essere un amministratore dell’ambiente in cui desideri eseguire Content Transformer.
* Per impostazione predefinita, qualsiasi operazione in grado di modificare il contenuto sorgente ( sposta/rimuovi/rinomina ) crea un pacchetto di backup dei percorsi sorgente in `/etc/packages/content-transformation` prima della trasformazione. Sebbene ogni finestra di dialogo delle operazioni disponga di un’opzione per disabilitare/abilitare la creazione dei pacchetti di backup, si consiglia rigorosamente di selezionare sempre l’opzione per abilitare la creazione dei pacchetti.
* Ogni pagina nel Content Transformer è configurata per elencare un massimo di 50 risultati, quindi alla volta è possibile trasformare un massimo di 50 risultati. Questa operazione viene eseguita per fornire una risposta tempestiva nell’interfaccia utente.

## Disponibilità {#availability-ct}

Il Content Transformer è fornito con [Strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) che possono essere scaricati come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nell’istanza AEM di origine.

>[!NOTE]
>Content Transformer è disponibile con lo strumento Content Transfer v2.0.20 o versione successiva.

## Apertura di Content Transformer {#opening-ct}

1. Accedi all’istanza AEM di origine come amministratore e passa alla pagina iniziale: https://host:port/aem/start.html.
1. Passa a Strumenti > Operazioni > Migrazione contenuti

   ![immagine](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > Assicurati di aver eseguito il rapporto BPA in precedenza e verificalo con l’URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html

1. Fai clic sulla scheda con il titolo **Report di Content Transformer for BPA**

   ![immagine](/help/journey-migration/content-transformer/assets/ct-2.png)

   Di seguito è riportato un esempio di come si presenterà la pagina Panoramica di Content Transformer se la creazione del rapporto BPA ha avuto esito positivo e se sono stati riscontrati problemi relativi al contenuto.

   Il tempo di scadenza rimasto per il rapporto BPA viene visualizzato sulla barra laterale. Si consiglia di eseguire Content Transformer con il report BPA più recente per evitare di perdere risultati relativi al contenuto.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-3.png)

1. Puoi filtrare i problemi in base a `Pattern Code`, `Subtype`, `Importance`, e `Source`.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-4.png)

1. Puoi selezionare tutti i problemi o alcuni problemi specifici e intraprendere azioni quali sposta, rimuovi e rinomina per risolverli. È possibile aggiungere percorsi personalizzati anche utilizzando **Aggiungi percorsi** nell&#39;angolo superiore destro.

   >[!NOTE]
   > Quando si utilizza l’operazione Sposta, si consiglia di spostare tutti i percorsi in una sola cartella (ad esempio in `/etc/packages/content-transformation/paths`), quindi quando i pacchetti di backup vengono installati per riportare l’istanza allo stato originale, la cartella (`/etc/packages/content-transformation/paths`) può essere eliminata mediante l’operazione di rimozione, per ridurre le dimensioni dell’archivio.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![immagine](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > Qualsiasi operazione che può modificare il contenuto sorgente (`move`/`remove`/`rename`) per impostazione predefinita crea un pacchetto di backup dei percorsi sorgente in `/etc/packages/content-transformation` prima della trasformazione. Sebbene ogni finestra di dialogo delle operazioni disponga di un’opzione per disabilitare/abilitare la creazione dei pacchetti di backup, si consiglia rigorosamente di selezionare sempre l’opzione per abilitare la creazione dei pacchetti.

1. Di seguito è riportato un esempio di pacchetto di backup creato per l’operazione di spostamento dei percorsi. Fai clic su Installa per ripristinare i percorsi sorgente. Si noti che l&#39;installazione riporterà solo i percorsi sorgente nella posizione originale e non eliminerà i percorsi in cui sono stati spostati durante la trasformazione. Per eliminare i percorsi nella posizione spostata, fate clic su **Aggiungi percorsi** per aggiungere la posizione (ad esempio `/etc/packages/content-transformation/paths`), seleziona il percorso e fai clic su **Rimuovi**.

   >[!CAUTION]
   > Non eliminare `/etc/packages/content-transformation` poiché è la posizione in cui risiedono i pacchetti di backup. Solo quando sei sicuro di non aver più bisogno di questi pacchetti, puoi eliminare questa posizione per ridurre le dimensioni dell’archivio.

   ![immagine](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![immagine](/help/journey-migration/content-transformer/assets/ct-8.png)
