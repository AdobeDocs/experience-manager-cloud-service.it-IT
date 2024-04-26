---
title: Aggiunta di un nome di dominio personalizzato
description: Scopri come aggiungere un nome di dominio personalizzato con Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: fcb6dd8ec74446643aaef1870685d26bc138bbd7
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 70%

---


# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

In Cloud Manager è possibile aggiungere un nome di dominio personalizzato da due posizioni:

* [Dalla pagina Impostazioni dominio](#adding-cdn-settings)
* [Dalla pagina Ambienti](#adding-cdn-environments)

>[!NOTE]
>
>Un utente deve disporre di **Proprietario business** o **Responsabile dell’implementazione** per aggiungere un nome di dominio personalizzato in Cloud Manager, è necessario utilizzare la rete CDN Fastly.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Quando si aggiunge un nome di dominio personalizzato, il dominio viene gestito utilizzando il certificato valido più specifico. Se più certificati hanno lo stesso dominio, viene scelto quello aggiornato più di recente. L’Adobe consiglia di gestire i certificati in modo che non vi siano domini sovrapposti.

Per aggiungere un nome di dominio personalizzato dalla sezione **Impostazioni dominio** pagina. Questi passaggi sono basati su Fastly. Se utilizzi una rete CDN diversa, devi configurare il dominio con la rete CDN che hai scelto di utilizzare.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** , selezionare il programma.

1. Passa a seleziona la **Impostazioni dominio** nel pannello di navigazione a sinistra.

   ![Finestra Impostazioni dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Fai clic su **Aggiungi dominio** in alto a destra per aprire **Aggiungi nome dominio** .

   ![Finestra di dialogo Aggiungi dominio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Inserisci il nome di dominio personalizzato nel campo **Nome di dominio**.

   >[!NOTE]
   >
   >Non includere `http://`, `https://` o spazi durante l’inserimento del dominio.

1. Seleziona l’**Ambiente** il cui servizio è associato al nome di dominio.

1. Seleziona il servizio **Publish** o **Anteprima**.

1. Dall’elenco a discesa, seleziona il **certificato SSL del dominio** associato al nome di dominio, quindi **Continua**.

1. Si apre la finestra di dialogo **Aggiungi nome di dominio**, che consente di accedere al processo di verifica del nome di dominio. Per verificare la proprietà del dominio dell’ambiente, segui le istruzioni fornite. Fai clic su **Crea**.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La distribuzione CDN richiede un certificato SSL valido e una verifica TXT correttamente riuscita. Viene indicato dallo stato **Verificato e distribuito**.

Per ulteriori informazioni sui vari stati e su come risolvere i potenziali problemi, consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!TIP]
>
>Rivedi il seguente articolo sulla necessità di [Aggiungi un CNAME o un record](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per evitare di raddoppiare gli sforzi quando si aggiungono record DNS al dominio personalizzato. La voce TXT e il CNAME o un record possono essere impostati contemporaneamente sul server DNS che governa.

>[!TIP]
>
>Per ulteriori informazioni sui record TXT, consulta [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.
>
>Cloud Manager verificherà la proprietà del dominio e aggiornerà lo stato riportato nella tabella Impostazioni dominio. Per ulteriori dettagli, consulta [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

Per aggiungere un nome di dominio personalizzato dalla pagina **Ambienti**, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi alla pagina **Dettagli ambienti** dell’ambiente di tuo interesse.

   ![Inserimento del nome di dominio nella pagina Dettagli dell’ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Inserisci il nome di dominio personalizzato nella tabella **Nomi di dominio**.

   1. Inserisci il nome di dominio personalizzato.
   1. Seleziona il certificato SSL associato al nome dall’elenco a discesa.
   1. Clic **+Aggiungi**.

   ![Aggiungi nome di dominio personalizzato](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Verifica i valori selezionati nella finestra di dialogo **Aggiungi nome di dominio** e fai clic su **Continua**.

   ![Finestra del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >Non includere `http://`, `https://` o spazi durante l’inserimento del nome di dominio.

1. Si apre la finestra di dialogo **Aggiungi nome di dominio**, che consente di accedere al processo di verifica del nome di dominio. Per verificare la proprietà del dominio dell’ambiente, segui le istruzioni fornite. Fai clic su **Crea**.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La distribuzione CDN richiede un certificato SSL valido e una verifica TXT correttamente riuscita. Viene indicato dallo stato **Verificato e distribuito**.

Per ulteriori informazioni sui vari stati e su come risolvere i potenziali problemi, consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.
>
>Cloud Manager verificherà la proprietà del dominio e aggiornerà lo stato riportato nella tabella Impostazioni dominio. Per ulteriori dettagli, consulta [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!TIP]
>
>Per ulteriori informazioni sui record TXT, consulta [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
