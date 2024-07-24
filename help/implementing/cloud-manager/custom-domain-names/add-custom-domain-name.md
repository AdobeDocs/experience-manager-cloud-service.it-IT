---
title: Aggiunta di un nome di dominio personalizzato
description: Scopri come aggiungere un nome di dominio personalizzato con Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 35%

---


# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

Scopri come aggiungere un nome di dominio personalizzato con Cloud Manager.

## Requisiti {#requirements}

Prima di aggiungere un nome di dominio personalizzato in Cloud Manager, è necessario soddisfare questi requisiti.

* È necessario aggiungere un certificato SSL di dominio per il dominio che si desidera aggiungere prima di aggiungere un nome di dominio personalizzato come descritto nel documento [Aggiunta di un certificato SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* Per aggiungere un nome di dominio personalizzato in Cloud Manager è necessario avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.
* Devi utilizzare la rete CDN Fastly.

## Dove aggiungere nomi di dominio personalizzati {#where}

In Cloud Manager è possibile aggiungere un nome di dominio personalizzato da due posizioni:

* [Dalla pagina Impostazioni dominio](#adding-cdn-settings)
* [Dalla pagina Ambienti](#adding-cdn-environments)

Quando si aggiunge un nome di dominio personalizzato, il dominio viene gestito utilizzando il certificato valido più specifico. Se più certificati hanno lo stesso dominio, viene scelto quello aggiornato più di recente. L’Adobe consiglia di gestire i certificati in modo che non vi siano domini sovrapposti.

I passaggi descritti in questo documento si basano su Fastly. Se utilizzi una rete CDN diversa, devi configurare il dominio con la rete CDN che hai scelto di utilizzare.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina **Impostazioni dominio**, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Passa alla scheda **Impostazioni dominio** nel pannello di navigazione a sinistra.

   ![Finestra Impostazioni dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Fai clic sul pulsante **Aggiungi dominio** in alto a destra per aprire la finestra di dialogo **Aggiungi nome dominio**.

   ![Finestra di dialogo Aggiungi dominio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Nella scheda **Nome dominio** immettere il nome di dominio personalizzato nel campo **Nome dominio**.

   >[!NOTE]
   >
   >Non includere `http://`, `https://` o spazi durante l’inserimento del dominio.

1. Seleziona l’**Ambiente** il cui servizio è associato al nome di dominio.

1. Seleziona il servizio **Publish** o **Anteprima**.

1. Dall’elenco a discesa, seleziona il **certificato SSL del dominio** associato al nome di dominio, quindi **Continua**.

1. Viene visualizzata la scheda **Verifica**.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * La scheda **Verifica** descrive i passaggi successivi per configurare il nome di dominio personalizzato, che consiste nella creazione di un record TXT necessario.
   * Puoi farlo immediatamente (prima di toccare o fare clic su **Crea** nella finestra di dialogo) oppure dopo aver toccato o fatto clic su **Crea** nella finestra di dialogo.
   * Le opzioni e i passaggi successivi sono descritti di seguito.

1. Tocca o fai clic su **Crea** per salvare il nome di dominio personalizzato in Cloud Manager.

Cloud Manager attiverà automaticamente una verifica TXT quando selezioni **Crea** nel passaggio di verifica della procedura guidata **Aggiungi dominio personalizzato**, pertanto ti consigliamo di creare il record TXT al momento della creazione del nome di dominio personalizzato in Cloud Manager. Tuttavia, questo non è necessario. Per le verifiche successive, devi riselezionare attivamente l’icona di verifica accanto allo stato.

Il nome non sarà attivo finché la voce TXT non viene aggiunta e verificata da Cloud Manager. La verifica TXT corretta è indicata dallo stato **Verificato e distribuito**.

* Per ulteriori informazioni sui record TXT, consulta [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
* Per ulteriori informazioni su come Cloud Manager verifica il nome di dominio personalizzato e la relativa voce TXT, vedere [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Passaggi successivi {#next-steps}

Dopo aver creato il nome di dominio personalizzato in Cloud Manager, dovrai aggiungere una voce TXT per verificare la proprietà del dominio. Procedi al documento [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) per continuare la configurazione del nome di dominio personalizzato.

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

I passaggi per aggiungere un nome di dominio personalizzato dalla pagina **Ambienti** sono gli stessi di quando [aggiungi un nome di dominio personalizzato dalla pagina Impostazioni dominio,](#adding-cdn-settings) ma il punto di ingresso è diverso. Per aggiungere un nome di dominio personalizzato dalla pagina **Ambienti**, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi alla pagina **Dettagli ambienti** dell’ambiente di tuo interesse.

   ![Inserimento del nome di dominio nella pagina Dettagli dell’ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Inserisci il nome di dominio personalizzato nella tabella **Nomi di dominio**.

   1. Inserisci il nome di dominio personalizzato.
   1. Seleziona il certificato SSL associato al nome dall’elenco a discesa.
   1. Fai clic su **+Aggiungi**.

   ![Aggiungi nome di dominio personalizzato](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. La finestra di dialogo **Aggiungi nome dominio** si apre nella scheda **Nome dominio**. Continua come faresti per [aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio.](#adding-cdn-settings)
