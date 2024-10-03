---
title: Gestire configurazioni CDN
description: Scopri come utilizzare Cloud Manager per modificare, aggiornare o eliminare configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 7%

---


# Gestione configurazioni CDN (Content Delivery Network) {#manage-cdn-configurations}

Scopri come utilizzare Cloud Manager per modificare, aggiornare o eliminare configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.

## Modificare una configurazione CDN {#edit-cdn}

Ad Adobe, in Cloud Manager potrebbe essere utile modificare una configurazione CDN, incluso il livello di ambiente (Publish o Anteprima) e il certificato SSL, per diversi motivi.

* **Modifiche all&#39;ambiente**: la regolazione del livello consente di far corrispondere le impostazioni CDN con l&#39;ambiente corretto, sia per la produzione live (Publish) che per il test (Anteprima).
* **Miglioramenti della sicurezza**: potrebbe essere necessario selezionare un certificato SSL diverso durante l&#39;aggiornamento dei certificati o per soddisfare le esigenze di conformità e sicurezza.
* **Ottimizzazione delle prestazioni**: la modifica della configurazione garantisce le impostazioni CDN corrette per la distribuzione dei contenuti in base alle esigenze operative in continua evoluzione.

È possibile modificare una configurazione senza rimuovere completamente la configurazione esistente. Le modifiche vengono applicate all’ambiente selezionato, ad esempio staging o produzione, e possono influenzare il modo in cui il contenuto viene distribuito e protetto.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per modificare una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nel pannello laterale, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Configurazioni CDN**.
1. Nella tabella **Configurazioni CDN**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui desideri aggiornare la configurazione CDN.

   ![Modifica di una configurazione CDN](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Dal menu a discesa, fare clic su **Modifica**.
1. Nella finestra di dialogo **Modifica configurazione CDN**, imposta una o più opzioni nel rispettivo elenco a discesa.

   Le opzioni visualizzate nella finestra di dialogo possono variare a seconda che si utilizzi una rete CDN gestita da Adobe o una rete CDN gestita dal cliente.

1. Fai clic su **Aggiorna**.

   Lo stato del CDN modificato viene aggiornato nella tabella **Configurazioni CDN** per riflettere le modifiche apportate.

<!-- ## ALTERNATE METHOD FOR EDITING A CDN CONFIGURATION from the Environments page
    
    The steps for adding a custom domain name from the **Environments** page are the same as when [adding a custom domain name from the Domain Settings page](#adding-cdn-settings), but the entry point differs. Follow these steps to add a custom domain name from the **Environments** page.
    
    1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.
    
    1. Navigate to the **Environments Detail** detail page for the environment of interest.
    
       ![Entering domain name on the Environment Details page](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)
    
    1. Use the **Domain Names** table to submit the custom domain name.
    
       1. Enter the custom domain name.
       1. Select the SSL certificate associated with this name from the drop-down list.
       1. Click ![Add icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Add**.
    
       ![Add a custom domain name](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)
    
    1. The **Add domain name** dialog box opens to the **Domain Name** tab. Continue as you would for [adding a custom domain name from the Domain Settings page](#adding-cdn-settings). -->

## Eliminare una configurazione CDN {#delete-cdn}

Quando elimini una configurazione CDN gestita dall’Adobe o dal cliente in Adobe Cloud Manager, le impostazioni del routing e del certificato SSL del dominio associato vengono rimosse. Il dominio non utilizza più la rete CDN per la distribuzione del traffico e tutti i miglioramenti a livello di sicurezza e prestazioni forniti dalla rete CDN vengono persi. Potresti riscontrare un’interruzione del servizio fino a quando non viene configurata una nuova configurazione, sia che si aggiunga di nuovo la rete CDN eliminata che quella nuova.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per eliminare una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel pannello di navigazione a sinistra, in **Servizi**, fai clic su **Configurazioni CDN**.

1. Nella tabella Configurazioni CDN, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rimuovere la CDN.

   ![Eliminazione di una configurazione CDN](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Fai clic su **Elimina**.
1. Fai di nuovo clic su **Elimina** per confermare la rimozione del CDN del sito.


