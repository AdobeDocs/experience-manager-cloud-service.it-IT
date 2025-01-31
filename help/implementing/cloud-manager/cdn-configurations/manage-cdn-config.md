---
title: Gestire le mappature del dominio
description: Scopri come utilizzare Cloud Manager per modificare, aggiornare o eliminare configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 8%

---

# Gestire le mappature del dominio {#manage-cdn-configurations}

Scopri come utilizzare Cloud Manager per modificare o eliminare le configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.

## Modificare una configurazione CDN dalla pagina Mappature dominio {#edit-cdn}

In Adobe Cloud Manager, potrebbe essere utile modificare la configurazione di una rete CDN (Content Delivery Network), incluso il livello di ambiente (Publish o Anteprima) e il certificato SSL, per diversi motivi.

* **Modifiche all&#39;ambiente**: la regolazione del livello consente di far corrispondere le impostazioni CDN con l&#39;ambiente corretto, sia per la produzione live (Publish) che per il test (Anteprima).
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

   Le opzioni visualizzate nella finestra di dialogo dipendono dal fatto che si stia utilizzando una **rete CDN gestita dall&#39;Adobe** o un **altro provider della rete CDN** (rete CDN gestita dal cliente).

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

1. Nella finestra di dialogo **Modifica configurazione CDN**, imposta una o più opzioni nel rispettivo elenco a discesa.

   Le opzioni visualizzate nella finestra di dialogo dipendono dal fatto che si stia utilizzando una **rete CDN gestita dall&#39;Adobe** o un **altro provider della rete CDN** (rete CDN gestita dal cliente).

1. Fai clic su **Aggiorna**.


<!-- ## Go live readiness {#go-live-readiness} 

1. ADD STEPS -->


## Eliminare una configurazione CDN {#delete-cdn}

Quando elimini una configurazione CDN gestita dal cliente o gestita dall’Adobe in Cloud Manager, le impostazioni del routing e del certificato SSL del dominio associato vengono rimosse. Il dominio non utilizza più la rete CDN per la distribuzione del traffico e tutti i miglioramenti a livello di sicurezza e prestazioni forniti dalla rete CDN vengono persi. Potresti riscontrare un’interruzione del servizio fino a quando non viene configurata una nuova configurazione, sia che si aggiunga di nuovo la rete CDN eliminata che quella nuova.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per eliminare una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mappature dominio**.

1. Nella tabella Mapping di dominio, fai clic su ![Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga corrispondente a un CDN che desideri rimuovere, quindi fai clic su **Elimina**.

1. Nella finestra di dialogo **Elimina configurazione CDN**, fare clic su **Elimina**.

1. Fai di nuovo clic su **Elimina** per confermare la rimozione del CDN del sito.


## Eliminare una configurazione CDN dalla pagina Ambienti

I passaggi per eliminare una configurazione CDN dalla pagina **Ambienti** sono quasi gli stessi di quando si [elimina una configurazione CDN dalla pagina Mapping domini](#edit-cdn), ma il punto di ingresso è diverso.

**Per eliminare una configurazione CDN dalla pagina Ambienti:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel menu a sinistra, fai clic sull&#39;icona ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**.

1. Nella pagina **Ambienti** selezionare un ambiente di interesse.

1. Nel raggruppamento **Mapping dominio** della pagina dei dettagli dell&#39;ambiente fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) corrispondente alla configurazione CDN da rimuovere, quindi fare clic su **Elimina**.

1. Nella finestra di dialogo **Elimina configurazione CDN**, fare clic su **Elimina**.

1. Fai di nuovo clic su **Elimina** per confermare la rimozione del CDN del sito.
