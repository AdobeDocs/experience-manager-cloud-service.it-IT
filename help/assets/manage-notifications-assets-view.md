---
title: Gestire le notifiche
description: Monitora le operazioni eseguite sulle risorse o cartelle disponibili nell’archivio utilizzando le notifiche di visualizzazione di Assets.
exl-id: 1fe6a845-37d5-43c2-bb96-c5b149c238ab
feature: Assets Essentials
role: User, Leader
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 68%

---

# Osservare risorse, cartelle e raccolte {#watch-assets-folders}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Le notifiche di visualizzazione di Assets consentono di monitorare le operazioni eseguite sulle risorse, cartelle o raccolte disponibili nell’archivio. Devi selezionare e iscriverti al contenuto per il quale ti vengono inviate le notifiche. Puoi anche configurare le categorie per le quali vengono inviate le notifiche.

## Iscriversi alle categorie di notifica {#subscribe-to-notification-categories}

Puoi scegliere un elenco di categorie e iscriverti per ricevere le notifiche. La vista Assets invia le notifiche solo per le categorie selezionate tra le opzioni disponibili:

<table>
    <tbody>
     <tr>
      <th><strong>Categoria di notifica</strong></th>
      <th><strong>Descrizione</strong></th>
     </tr>
     <tr>
      <td>Richieste</td>
      <td>Quando si assegna un’attività a un utente, si riceve una notifica quando l'utente esegue un’azione su tale attività.</td>
     </tr>
     <tr>
      <td>Assegnato a me</td>
      <td>Ricevi una notifica quando un’attività ti è stata assegnata da un altro utente.</td>
     </tr>
     <tr>
      <td>Commento a contenuti sottoscritti</td>
      <td>Ricevi una notifica quando un utente aggiunge un commento alla risorsa a cui ti sei iscritto.</td>
     </tr>
     <tr>
      <td>Eliminazione di contenuti sottoscritti</td>
      <td>Ricevi una notifica quando un utente elimina la risorsa, la cartella o la raccolta a cui ti sei iscritto.</td>
     </tr>
     <tr>
      <td>Condivisione esterna di contenuti sottoscritti</td>
      <td>Ricevi una notifica quando un utente genera un collegamento pubblico per la risorsa, la cartella o la raccolta a cui ti sei iscritto.</td>
     </tr>
     <tr>
      <td>Modifica di contenuti sottoscritti</td>
      <td>Ricevi una notifica quando un utente crea una nuova versione della risorsa a cui ti sei iscritto.</td>
     </tr>
     <tr>
      <td>Spostamento o ridenominazione di contenuti sottoscritti</td>
      <td>Ricevi una notifica quando un utente sposta o rinomina la risorsa o la cartella sottoscritta.</td>
     </tr>
     <tr>
      <td>Aggiornamenti alle cartelle e alle raccolte sottoscritte</td>
      <td>Ricevi una notifica quando un utente aggiunge o rimuove una risorsa da una cartella o raccolta sottoscritta.</td>
     </tr>    
    </tbody>
   </table>

Per iscriversi alle categorie di notifica:

1. Fai clic su ![icona campanello](assets/bell-icon.svg) all&#39;estremità destra della barra dei menu nell&#39;interfaccia utente di visualizzazione di Assets.

1. Fai clic su ![icona impostazioni](assets/settings-icon.svg) per visualizzare la pagina [!UICONTROL Preferenze di Experience Cloud].

1. Fai clic sul pulsante **[!UICONTROL Notifiche]** nel riquadro a sinistra.

1. Nella sezione **[!UICONTROL Notifiche]**, passa alla sezione [!UICONTROL Visualizzazione Assets] e assicurati che l&#39;opzione di attivazione sia attivata.

   ![Notifiche nella visualizzazione Assets](assets/enable-notifications.png)

1. Fai clic su **[!UICONTROL Personalizza]** per visualizzare le categorie di notifiche.
   ![Notifiche nella visualizzazione Assets](assets/enable-notification-categories.png)

1. Seleziona le categorie di notifica per le quali vuoi ricevere una notifica.

## Osservare e non osservare più cartelle, risorse o raccolte {#watch-unwatch-assets}

Dopo l’[iscrizione alle categorie di notifica](#subscribe-to-notification-categories), devi iscriverti al contenuto per iniziare a ricevere le notifiche.

>[!NOTE]
>
>* Per le categorie di notifiche **[!UICONTROL Richieste]** e **[!UICONTROL Assegnato a me]**, non è necessario iscriversi ai contenuti dopo l’iscrizione alle categorie di notifica. Le notifiche vengono inviate automaticamente per le richieste che crei e quando un&#39;attività viene assegnata a te.
>* La vista Assets invia notifiche solo quando altri utenti eseguono azioni sui contenuti a cui si è iscritti. Non si ricevono notifiche per le azioni eseguite personalmente sui contenuti a cui si è iscritti.

Per iscriverti al contenuto, seleziona la cartella, la risorsa o la raccolta che ti interessa e fai clic su **[!UICONTROL Osserva]**.

Nella vista Assets viene visualizzato un messaggio di successo. Puoi fare clic su **[!UICONTROL Vai alle preferenze per le notifiche]** nel messaggio di successo per cambiare le [categorie di notifica che ti interessano](#subscribe-to-notification-categories).

![Notifiche nella visualizzazione Assets](assets/watch-assets.png)

La vista Assets ora invia notifiche per le categorie sottoscritte. Per risparmiare tempo, puoi anche selezionare più risorse, cartelle o raccolte e fare clic su **[!UICONTROL Osserva]**. Tuttavia, se selezioni più entità di cui alcune sono già state sottoscritte, l’opzione **[!UICONTROL Osserva]** non viene visualizzata.

Allo stesso modo, per annullare l’iscrizione a una risorsa, cartella o raccolta, selezionala e fai clic su **[!UICONTROL Non osservare più]**.

## Visualizzare le notifiche {#view-notifications}

Le notifiche vengono visualizzate all’estremità destra della barra dei menu nell’interfaccia utente di visualizzazione di Assets.

![Notifiche nella visualizzazione Assets](assets/notifications-assets-essentials.png)

Quando fai clic su una notifica, la vista Assets ti consente di passare alla risorsa o cartella appropriata a cui fa riferimento la notifica.
