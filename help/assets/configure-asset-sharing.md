---
title: Condivisione di risorse, cartelle e raccolte come collegamento
description: Questo articolo descrive come condividere risorse, cartelle e raccolte in Experience Manager Assets come collegamento ipertestuale.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Configurare la condivisione dei collegamenti delle risorse {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura sul `/var/dam/share` posto possono visualizzare i collegamenti condivisi con tali utenti. La condivisione di risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili a soggetti esterni senza dover prima accedere a Risorse AEM.

>[!NOTE]
>
>Se desiderate condividere i collegamenti dall&#39;istanza di AEM Author a entità esterne, accertatevi di esporre solo i seguenti URL per `GET` le richieste. Bloccate altri URL per garantire la protezione dell&#39;istanza di AEM Author.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## Configurare il servizio di posta di CQ Day {#configmailservice}

Prima di poter condividere le risorse come collegamenti, configurate il servizio e-mail.

1. Tocca o fai clic sul logo AEM, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Dall&#39;elenco dei servizi, individuare il servizio **[!UICONTROL di posta]** Day CQ.
1. Fai clic sull’icona **[!UICONTROL Modifica]** posta accanto al servizio e configura i seguenti parametri per **Day CQ Mail Service]** con i dettagli indicati insieme ai relativi nomi:

   * Nome host del server SMTP: nome host del server di posta elettronica
   * Porta server SMTP: porta del server di posta elettronica
   * Utente SMTP: nome utente del server di posta elettronica
   * Password SMTP: password del server di posta elettronica

1. Click/tap **Save**.

## Configurare la dimensione massima dei dati {#maxdatasize}

Quando scaricate le risorse dal collegamento condiviso mediante la funzione Condivisione collegamenti, AEM comprime la gerarchia delle risorse dall’archivio e quindi restituisce la risorsa in un file ZIP. Tuttavia, in assenza di limiti alla quantità di dati che possono essere compressi in un file ZIP, enormi quantità di dati sono soggetti a compressione, il che causa errori di memoria insufficiente in JVM. Per proteggere il sistema da un potenziale attacco di negazione di servizio a causa di questa situazione, configurate la dimensione massima utilizzando il parametro **Max Content Size (non compresso)** per Day CQ DAM Adhoc Asset Share Proxy Servlet in Configuration Manager. Se le dimensioni non compresse della risorsa superano il valore configurato, le richieste di download delle risorse vengono rifiutate. Il valore predefinito è 100 MB.

1. Tocca o fai clic sul logo AEM, quindi passa a **Strumenti** > **Operazioni** > **Console web**.
1. Dalla console Web, individua la configurazione **Day CQ DAM Adhoc Asset Share Proxy Servlet** .
1. Apri la configurazione **Day CQ DAM Adhoc Asset Share Proxy Servlet** in modalità di modifica e cambia il valore del parametro in **Max Content Size (uncompressed)**.
1. Salva le modifiche.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
