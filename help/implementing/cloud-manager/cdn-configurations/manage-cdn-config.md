---
title: Gestire configurazioni CDN
description: Scopri come utilizzare Cloud Manager per modificare, aggiornare o eliminare configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 42b30c12f17106610cfb7f7b4c04c5ab703bab45
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 9%

---


# Gestione configurazioni CDN (Content Delivery Network) {#manage-cdn-configurations}

Scopri come utilizzare Cloud Manager per modificare, aggiornare o eliminare configurazioni CDN per un sito Edge Delivery o un ambiente Cloud Manager.

## Modificare una configurazione CDN dalla pagina Configurazioni CDN {#edit-cdn}

Ad Adobe, in Cloud Manager potrebbe essere utile modificare una configurazione CDN, incluso il livello di ambiente (Publish o Anteprima) e il certificato SSL, per diversi motivi.

* **Modifiche all&#39;ambiente**: la regolazione del livello consente di far corrispondere le impostazioni CDN con l&#39;ambiente corretto, sia per la produzione live (Publish) che per il test (Anteprima).
* **Miglioramenti della sicurezza**: potrebbe essere necessario selezionare un certificato SSL diverso durante l&#39;aggiornamento dei certificati o per soddisfare le esigenze di conformità e sicurezza.
* **Ottimizzazione delle prestazioni**: la modifica della configurazione garantisce le impostazioni CDN corrette per la distribuzione dei contenuti in base alle esigenze operative in continua evoluzione.

È possibile modificare una configurazione senza rimuovere completamente la configurazione esistente. Le modifiche vengono applicate all’ambiente selezionato, ad esempio staging o produzione, e possono influenzare il modo in cui il contenuto viene distribuito e protetto.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per modificare una configurazione CDN dalla pagina Configurazioni CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nel pannello laterale, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Configurazioni CDN**.
1. Nella tabella **Configurazioni CDN**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui desideri aggiornare la configurazione CDN.

   ![Modifica di una configurazione CDN](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Dal menu a discesa, fare clic su **Modifica**.
1. Nella finestra di dialogo **Modifica configurazione CDN**, imposta una o più opzioni nel rispettivo elenco a discesa.

   Le opzioni visualizzate nella finestra di dialogo dipendono dal fatto che si stia utilizzando una **rete CDN gestita di Adobe** o un **altro provider CDN** (rete CDN gestita dal cliente).

1. Fai clic su **Aggiorna**.

   Lo stato del CDN modificato viene aggiornato nella tabella **Configurazioni CDN** per riflettere le modifiche apportate.

## Modificare una configurazione CDN dalla pagina Ambienti

I passaggi per modificare una configurazione CDN dalla pagina **Ambienti** sono quasi gli stessi di quando si [modifica una configurazione CDN dalla pagina Configurazioni CDN](#edit-cdn), ma il punto di ingresso è diverso.

**Per modificare una configurazione CDN dalla pagina Ambienti:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel menu a sinistra, fai clic su **Ambienti**.

1. Nella pagina **Ambienti** selezionare un ambiente di interesse.

1. Nella pagina dei dettagli dell&#39;ambiente, nel raggruppamento Configurazioni CDN, fare clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) che corrisponde alla configurazione CDN che si desidera modificare.

   ![Inserimento del nome di dominio nella pagina Dettagli dell’ambiente](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)

1. Nel menu popup, fare clic su **Modifica**.

1. Nella finestra di dialogo **Modifica configurazione**, imposta una o più opzioni nel rispettivo elenco a discesa.

Le opzioni visualizzate nella finestra di dialogo dipendono dal fatto che si stia utilizzando una **rete CDN gestita di Adobe** o un **altro provider CDN** (rete CDN gestita dal cliente).

1. Fai clic su **Aggiorna**.


<!-- ## Go live readiness {#go-live-readiness} 

1. ADD STEPS -->


## Eliminare una configurazione CDN {#delete-cdn}

Quando elimini una configurazione CDN gestita dal cliente o gestita dall’Adobe in Cloud Manager, le impostazioni del routing e del certificato SSL del dominio associato vengono rimosse. Il dominio non utilizza più la rete CDN per la distribuzione del traffico e tutti i miglioramenti a livello di sicurezza e prestazioni forniti dalla rete CDN vengono persi. Potresti riscontrare un’interruzione del servizio fino a quando non viene configurata una nuova configurazione, sia che si aggiunga di nuovo la rete CDN eliminata che quella nuova.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

**Per eliminare una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nel pannello a sinistra, in **Servizi**, fai clic su **Configurazioni CDN**.

1. Nella tabella Configurazioni CDN, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rimuovere la CDN.

   ![Eliminazione di una configurazione CDN](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Fai clic su **Elimina**.

1. Fai di nuovo clic su **Elimina** per confermare la rimozione del CDN del sito.


