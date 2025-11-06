---
title: Gestire le mappature di dominio
description: Scopri come utilizzare Cloud Manager per modificare, aggiornare o eliminare configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 8%

---

# Gestire le mappature di dominio {#manage-domain-mappings}

Scopri come utilizzare Cloud Manager per modificare o eliminare le configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.

## Modificare una configurazione CDN dalla pagina Mappature dominio {#edit-domain-mapping}

In Adobe Cloud Manager, potrebbe essere utile modificare la configurazione di una rete CDN (Content Delivery Network), incluso il livello di ambiente (Pubblicazione o Anteprima) e il certificato SSL, per diversi motivi.

* **Modifiche all&#39;ambiente**: la regolazione del livello consente di far corrispondere le impostazioni CDN con l&#39;ambiente corretto, sia per la produzione live (pubblicazione) che per il test (anteprima).
* **Miglioramenti della sicurezza**: potrebbe essere necessario selezionare un certificato SSL diverso durante l&#39;aggiornamento dei certificati o per soddisfare le esigenze di conformità e sicurezza.
* **Ottimizzazione delle prestazioni**: la modifica della configurazione garantisce le impostazioni CDN corrette per la distribuzione dei contenuti in base alle esigenze operative in continua evoluzione.

È possibile modificare una configurazione senza rimuovere completamente la configurazione esistente. Le modifiche vengono applicate all’ambiente selezionato, ad esempio staging o produzione, e possono influenzare il modo in cui il contenuto viene distribuito e protetto.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per modificare una configurazione CDN dalla pagina Mapping domini:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mappature dominio**.
1. Nella tabella **Mappature dominio**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui desideri aggiornare la configurazione CDN.

1. Dal menu a discesa, fare clic su **Modifica**.

1. Nella finestra di dialogo **Modifica configurazione CDN**, imposta una o più opzioni nel rispettivo elenco a discesa.

   Le opzioni visualizzate nella finestra di dialogo dipendono dal fatto che si stia utilizzando una **rete CDN gestita da Adobe** o un **altro provider CDN** (rete CDN gestita dal cliente).

1. Fai clic su **Aggiorna**.

   Lo stato del CDN modificato viene aggiornato nella tabella **Mapping dominio** per riflettere le modifiche apportate.


## Modificare una configurazione CDN dalla pagina Ambienti

I passaggi per modificare una configurazione CDN dalla pagina **Ambienti** sono quasi gli stessi di quando si [modifica una configurazione CDN dalla pagina Mapping domini](#edit-cdn), ma il punto di ingresso è diverso.

**Per modificare una configurazione CDN dalla pagina Ambienti:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel menu a sinistra, fai clic sull&#39;icona ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**.

1. Nella pagina **Ambienti** selezionare un ambiente di interesse.

1. Nel raggruppamento Mapping di dominio della pagina dei dettagli dell&#39;ambiente fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) corrispondente alla configurazione CDN che si desidera modificare.

1. Nel menu popup, fare clic su **Modifica**.

1. Nella finestra di dialogo **Modifica mapping di dominio**, impostare una o più opzioni nel rispettivo elenco a discesa.

   Le opzioni visualizzate nella finestra di dialogo dipendono dal fatto che si stia utilizzando una **rete CDN gestita da Adobe** o un **altro provider CDN** (rete CDN gestita dal cliente).

1. Fai clic su **Aggiorna**.


## Preparazione Go Live: configurazione delle impostazioni DNS per un dominio personalizzato {#go-live-readiness}

Prima che un dominio personalizzato possa gestire il traffico, è necessario completare la configurazione DNS con il provider DNS. Dopo aver distribuito una mappatura di dominio e aver fatto clic su **Go live**, Cloud Manager visualizza una finestra di dialogo che ti guida attraverso il processo di configurazione dei record DNS. È possibile attivare l’opzione aggiungendo un tipo di record CNAME o A.

<!-- See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record). -->

**Per configurare lo stato di preparazione al lancio:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mappature dominio**.
1. Nella tabella Mapping di dominio, fai clic su **Pubblica** alla fine di una riga corrispondente a una rete CDN di cui desideri configurare la disponibilità.

   ![Finestra di dialogo Preparazione pubblicazione](/help/implementing/cloud-manager/assets/domain-mappings-go-live-readiness.png)

1. Nella finestra di dialogo **Preparazione pubblicazione** eseguire una delle operazioni seguenti:

   | Opzione | Passaggi |
   | --- | --- |
   | Configurare RECORD A | Consigliato per domini radice come `example.com`<br><ol><li>Accedere al portale del provider di servizi DNS.<li>Passare alla sezione Record DNS.<li>Crea un record A che punti a tutti gli indirizzi IP elencati.</li></ol> |
   | Configura CNAME | Consigliato per domini personalizzati come `www.example.com`<br><ol><li>Accedere al portale del provider di servizi DMS.<li>Passare alla sezione Record DNS.<li>Mappa `cdn.adobeaemcloud.com` (record CNAME) nel record DNS del provider di servizi DNS (dominio personalizzato). Questa mappatura assicura che le richieste ricevute al dominio personalizzato vengano reindirizzate al CDN di Adobe.</li></ol> |

1. Nella finestra di dialogo **Preparazione pubblicazione** fare clic su **OK** per salvare il record.

   Attendere la propagazione DNS; potrebbero essere necessari alcuni minuti o alcune ore.

   Quando la colonna **[!UICONTROL Stato]** nella tabella Mappature dominio viene aggiornata a **[!UICONTROL Verificato]**, il dominio personalizzato è pronto per l&#39;uso. Potrebbe essere necessario fare clic sull&#39;icona ![Aggiorna](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) per aggiornare lo stato.

## Eliminare una configurazione CDN {#delete-cdn}

Quando elimini una configurazione CDN gestita da Adobe o dal cliente in Cloud Manager, le impostazioni del routing e del certificato SSL del dominio associato vengono rimosse. Il dominio non utilizza più la rete CDN per la distribuzione del traffico e tutti i miglioramenti a livello di sicurezza e prestazioni forniti dalla rete CDN vengono persi. Potresti riscontrare un’interruzione del servizio fino a quando non viene configurata una nuova configurazione, sia che si aggiunga di nuovo la rete CDN eliminata che quella nuova.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per eliminare una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mappature dominio**.

1. Nella tabella Mapping di dominio, fai clic su ![Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga corrispondente a un CDN che desideri rimuovere, quindi fai clic su **Elimina**.

1. Nella finestra di dialogo **Elimina mapping di dominio** fare clic su **Elimina**.

1. Fai di nuovo clic su **Elimina** per confermare la rimozione del CDN del sito.


## Eliminare una configurazione CDN dalla pagina Ambienti

I passaggi per eliminare una configurazione CDN dalla pagina **Ambienti** sono quasi gli stessi di quando si [elimina una configurazione CDN dalla pagina Mapping domini](#edit-cdn), ma il punto di ingresso è diverso.

**Per eliminare una configurazione CDN dalla pagina Ambienti:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel menu a sinistra, fai clic sull&#39;icona ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**.

1. Nella pagina **Ambienti** selezionare un ambiente di interesse.

1. Nel raggruppamento **Mapping dominio** della pagina dei dettagli dell&#39;ambiente fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) corrispondente alla configurazione CDN da rimuovere, quindi fare clic su **Elimina**.

1. Nella finestra di dialogo **Elimina mapping di dominio** fare clic su **Elimina**.

1. Fai di nuovo clic su **Elimina** per confermare la rimozione del CDN del sito.
