---
title: Aggiunta di un nome di dominio personalizzato
description: Scopri come aggiungere un nome di dominio personalizzato con Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 21496a52fbe3caa08c606ddaeb85481a9d416b3d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 98%

---

# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

In Cloud Manager è possibile aggiungere un nome di dominio personalizzato da due posizioni:

* [Dalla pagina Impostazioni dominio](#adding-cdn-settings)
* [Dalla pagina Ambienti](#adding-cdn-environments)

>[!NOTE]
>
>Per poter aggiungere un nome di dominio personalizzato in Cloud Manager, l’utente deve avere il ruolo **Proprietario business** o **Responsabile dell’implementazione**.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina **Impostazioni dominio**, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Nel pannello di navigazione a sinistra, fai clic su **Impostazioni dominio**.

   ![Finestra Impostazioni dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Per aprire la finestra di dialogo **Aggiungi nome di dominio**, fai clic sul pulsante **Aggiungi dominio** nella parte superiore destra della pagina.

   ![Finestra di dialogo Aggiungi dominio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Inserisci il nome di dominio personalizzato nel campo **Nome di dominio**.

   >[!NOTE]
   >
   >Non includere `http://`, `https://` o spazi durante l’inserimento del dominio.

1. Seleziona l’**Ambiente** di cui associare il servizio al nome di dominio.

1. Seleziona il servizio **Publish** o **Anteprima**.

1. Dall’elenco a discesa, seleziona il **certificato SSL del dominio** associato al nome di dominio, quindi **Continua**.

1. Si apre la finestra di dialogo **Aggiungi nome di dominio**, che consente di accedere al processo di verifica del nome di dominio. Per verificare la proprietà del dominio dell’ambiente, segui le istruzioni fornite. Fai clic su **Crea**.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La distribuzione CDN richiede un certificato SSL valido e una verifica TXT correttamente riuscita. Viene indicato dallo stato **Verificato e distribuito**.

Per ulteriori informazioni sui vari stati e su come risolvere i potenziali problemi, consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.
>
>Cloud Manager verificherà la proprietà del dominio e aggiornerà lo stato riportato nella tabella Impostazioni dominio. Per ulteriori informazioni, consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!TIP]
>
>Per ulteriori informazioni sui record TXT, consulta [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

Per aggiungere un nome di dominio personalizzato dalla pagina **Ambienti**, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi alla pagina **Dettagli ambienti** dell’ambiente di tuo interesse.

   ![Inserimento del nome di dominio nella pagina Dettagli dell’ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Inserisci il nome di dominio personalizzato nella tabella **Nomi di dominio**.

   1. Inserisci il nome di dominio personalizzato.
   1. Seleziona il certificato SSL associato al nome dall’elenco a discesa.
   1. Fai clic su **+Aggiungi**.

   ![Aggiungi nome di dominio personalizzato](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Verifica i valori selezionati nella finestra di dialogo **Aggiungi nome di dominio** e fai clic su **Continua**.

   ![Finestra Nome dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

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
>Cloud Manager verificherà la proprietà del dominio e aggiornerà lo stato riportato nella tabella Impostazioni dominio. Per ulteriori informazioni, consulta il documento [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

>[!TIP]
>
>Per ulteriori informazioni sui record TXT, consulta [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
