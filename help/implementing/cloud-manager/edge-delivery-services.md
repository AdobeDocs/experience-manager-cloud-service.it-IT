---
title: Supporto per Edge Delivery Services in Cloud Manager
description: Scopri come distribuire i progetti Cloud Manager utilizzando i Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4e887b753eaf09e104c68484792f00dcb08ee304
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 5%

---

# Supporto per Edge Delivery Services in Cloud Manager {#edge-delivery-services}

Scopri come utilizzare la licenza di Edge Delivery Services per creare un sito Edge Delivery Services.

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->

## Edge Delivery Services in breve {#edge-overview}

Edge Delivery Services è un set di sevizi componibili che consente un elevato grado di flessibilità per quanto riguarda la creazione di contenuti sul sito web. Questa funzionalità consente di effettuare le seguenti operazioni:

* Crea siti veloci con un punteggio perfetto Lighthouse.
* Monitoraggio continuo delle prestazioni tramite RUM (Real Use Monitoring).
* Aumentare l’efficienza di authoring disaccoppiando le origini di contenuto.

Puoi utilizzare sia la gestione dei contenuti AEM che l’authoring WYSIWYG utilizzando l’editor universale e l’authoring basato su documenti.

Cloud Manager in AEM as a Cloud Service consente di abilitare il servizio Edge Delivery per il progetto.

>[!TIP]
>
>Per informazioni dettagliate sui Edge Delivery Services e su come utilizzarli con AEM, consulta il documento [Panoramica sui Edge Delivery Services](/help/edge/overview.md).

## Edge Delivery Services in Cloud Manager {#edge-in-cloud-manager}

Se disponi di Edge Delivery Services con licenza come parte di Adobe Experience Manager Sites, puoi accedere al tuo sito tramite Edge Delivery Services direttamente in Cloud Manager e andare in diretta [tramite un&#39;esperienza guidata e autonoma](/help/implementing/cloud-manager/managing-code/private-repositories.md).

Inoltre, puoi accedere a un’esperienza unificata per gestire tutte le proprietà dell’AEM e al contempo garantire la coerenza tra i flussi di lavoro chiave. Tra questi sono inclusi la gestione dei nomi di dominio, la gestione dei certificati SSL e le mappature CDN.

## Aggiungere Edge Delivery Services a un programma di produzione o sandbox

Per aggiungere o modificare programmi, è necessario essere membri del ruolo **Proprietario business** o disporre dell&#39;autorizzazione necessaria.
Prima di poter applicare la licenza a un programma di produzione, la tua organizzazione deve disporre di una licenza per Edge Delivery Services non utilizzata.

>[!NOTE]
>
>Una volta che la licenza Edge Delivery Services viene applicata o rimossa da un programma, la modifica ha effetto immediato senza la necessità di eseguire una pipeline. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

A seconda del caso d’uso, effettua una delle seguenti operazioni:

| Caso d’uso | Descrizione |
| --- | --- |
| Voglio aggiungere dei Edge Delivery Services a un nuovo programma di produzione. | Consulta [Creare programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>Nella procedura guidata, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere Edge Delivery Services a un programma di produzione esistente. | Consulta [Modifica programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>Nella finestra di dialogo **Modifica programma**, nella scheda **Soluzioni e componenti aggiuntivi**, seleziona **Edge Delivery Services**. |
| Desidero aggiungere Edge Delivery Services a un programma sandbox nuovo o esistente. | Consulta [Creare programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Quando si crea un programma sandbox, i Edge Delivery Services vengono aggiunti al programma per impostazione predefinita; non è necessario selezionarlo.<br>I programmi sandbox esistenti ereditano automaticamente i Edge Delivery Services. |

## Adobe di percorso consigliato per i clienti con contratto {#recommended-path-eds}

In qualità di cliente a contratto, assicurati di trarre il massimo vantaggio da Adobe accedendo e utilizzando la licenza del Edge Delivery Services tramite Cloud Manager. Questo approccio consente di utilizzare [CDN gestita da Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) e di sfruttare i vantaggi principali, quali la gestione CDN self-service, inclusa la configurazione e l&#39;installazione di certificati DV o EV/OV. Se non disponi di una licenza di Edge Delivery Services con Adobe e decidi di ignorare tali vantaggi, puoi utilizzare solo una rete CDN gestita dal cliente. Questa configurazione deve essere sulla piattaforma aem.live.

Se hai stipulato un contratto con le licenze dei Edge Delivery Services AEM as a Cloud Service Sites, accedi a Cloud Manager per assicurarti di poter eseguire le seguenti operazioni:

* Utilizzare la licenza per il programma scelto.
* Sfrutta i vantaggi di [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) per eseguire operazioni CRUD (Create, Read, Update, Delete).
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* Accedi ai report di SLA (*presto disponibile*) <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Supporto Adobe. Assicurati che i siti dei Edge Delivery Services siano registrati tramite un programma di produzione in Cloud Manager per ottenere il riconoscimento e il supporto corretti da parte di Adobe.

## Aggiungere un sito Edge Delivery Services {#eds-add-site}

Dopo aver aggiunto i Edge Delivery Services a un programma di produzione, viene applicata la licenza per i Edge Delivery Services.

Nella pagina Panoramica viene visualizzata una nuova scheda selezionabile denominata **Edge Delivery**. Facendo clic sulla scheda viene visualizzata una tabella in cui sono elencati tutti i siti Edge Delivery aggiunti. Nel pannello di navigazione a sinistra, nel raggruppamento **Servizi**, noterai un&#39;opzione di menu denominata **Edge Delivery Sites**.

![Pagina Panoramica che mostra i siti Edge Delivery nel pannello di navigazione a sinistra e la scheda Edge Delivery a destra della scheda Consegna Publish](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Per aggiungere un sito Edge Delivery:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito Edge Delivery.
1. Effettuare una delle seguenti operazioni:
   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Quindi, nell&#39;angolo inferiore destro della pagina, fare clic su **Aggiungi sito Edge Delivery**.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     L&#39;**elenco attività di Edge Delivery**, come illustrato nell&#39;immagine precedente, è una guida opzionale all&#39;onboarding che ti aiuta a iniziare a utilizzare Edge Delivery. Consulta [Informazioni sull&#39;elenco attività di Edge Delivery](#ed-todo-list).

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**. Fai clic su **Aggiungi sito** nell&#39;angolo superiore destro della pagina.

     ![Aggiungi sito Edge Delivery dal pulsante Siti Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Nella finestra di dialogo **Aggiungi sito Edge Delivery** eseguire le operazioni seguenti:

   | Campo di testo | Cosa fare |
   | --- | --- |
   | Nome sito | Immetti il nome del sito Edge Delivery che stai aggiungendo. Il nome funge da identificatore univoco del sito all’interno di Cloud Manager. |
   | URL archivio | Questo campo si riferisce all’archivio Git in cui è memorizzato il codice del sito web.<br>Immetti l&#39;URL dell&#39;archivio Git che contiene i file e le risorse necessarie (ad esempio HTML, CSS, JavaScript e altre risorse Web) per il tuo sito Edge Delivery. Questa disposizione consente a Cloud Manager di estrarre il codice da tale archivio durante il processo di distribuzione. |
   | Descrizione sito (facoltativa) | Immetti una breve descrizione del sito Edge Delivery che stai aggiungendo.<br>Questa descrizione consente di identificare e differenziare il sito, semplificandone la gestione e il riconoscimento tra gli altri siti aggiunti. È possibile includere dettagli sullo scopo del sito, sul contenuto o su qualsiasi altra informazione rilevante che possa aiutare a chiarirne la funzione o l’ambito. |

1. Nell&#39;angolo inferiore destro della finestra di dialogo fare clic su **Aggiungi**.

1. Nella finestra di dialogo **Verifica proprietà repository** eseguire una delle operazioni seguenti:

   | Passaggio | Descrizione |
   | --- | --- |
   | 1 | Aggiungere un file con il percorso al ramo `main` dell&#39;archivio Git elencato nel campo **URL archivio**. Se necessario, fate clic sull&#39;icona Copia per copiare il percorso negli Appunti.<br> Percorso: <br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>Non *aggiungere* un punto all&#39;inizio del percorso, in:<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | Aggiungi il codice generato al file creato nel passaggio 1. Se necessario, fai clic sull’icona Copia per copiare il codice negli Appunti. |
   | 3 | Nell’archivio Git, crea una richiesta di pull, quindi uniscila per eseguire il commit del codice. |

1. Fare clic su **Verifica**. Dopo la verifica dell’archivio, il suo stato nella tabella Edge Deliver Sites cambia in un cerchio verde con un segno di spunta bianco all’interno.

## Informazioni sull’elenco delle attività di Edge Delivery {#ed-todo-list}

L&#39;**elenco attività di Edge Delivery** è un elenco di controllo delle attività di onboarding che ti guiderà attraverso l&#39;onboarding e la gestione del tuo sito Edge Delivery fino al [lancio](/help/journey-onboarding/go-live-checklist.md).

|  | Attività | Descrizione |
| --- | --- | --- |
| 1 | Partecipa al canale di collaborazione sui prodotti | Facendo clic su **Invia richiesta ora**, invia una richiesta ad Adobe per la creazione di un canale per la società. Se il canale esiste già, viene effettuato l’inoltro al canale della tua azienda. |
| 2 | Completa i prerequisiti | Facendo clic su **Visualizza esercitazione introduttiva**, si accede alla [Guida introduttiva - Esercitazione per sviluppatori](https://www.aem.live/developer/tutorial). |
| 3 | Aggiungi sito Edge Delivery | Consulta [Aggiungere un sito Edge Delivery](#eds-add-site). |
| 4 | Aggiungi dominio | Vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Aggiungi certificato SSL | Vedi [Aggiungi certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configurare la rete CDN del sito Edge Delivery | Vedere [Aggiungere una configurazione CDN](#add-cdn). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on) (2 minuti, 13 secondi)

## Aggiungere una configurazione CDN al sito Edge Delivery {#add-cdn}

Vedere [Aggiungere una configurazione CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Eliminare un sito Edge Delivery {#eds-site-delete}

>[!IMPORTANT]
>
>Se elimini un sito Edge Delivery Services, vengono rimosse anche le configurazioni CDN associate. Questa azione interrompe la connessione tra i domini personalizzati e il sito. Per ulteriori dettagli, consulta Configurazioni CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Per eliminare un sito Edge Delivery:**

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nella console **[Programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito Edge Delivery.
1. Effettuare una delle seguenti operazioni:
   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Nella tabella del sito di Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rimuovere il sito. Fai clic su **Elimina**, quindi fai di nuovo clic su **Elimina** per confermare la rimozione del sito.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**. Nella tabella del sito di Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rimuovere il sito. Fai clic su **Elimina**, quindi fai di nuovo clic su **Elimina** per confermare la rimozione del sito.


     ![Aggiungi sito Edge Delivery dal pulsante Siti Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)


<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
