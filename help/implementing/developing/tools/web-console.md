---
title: Console web
description: Scopri come utilizzare la console web di Adobe Experience Manager (AEM) per gestire le impostazioni OSGi e i bundle per lo sviluppo locale.
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 3aaa615f-d3bf-4d1a-9dff-b6e271f0e9a6
source-git-commit: 3995e0090e1b0be1cbc430c3da7458b6ce867e09
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---


# Console web {#web-console}

Scopri come utilizzare la console web di Adobe Experience Manager (AEM) per gestire le impostazioni OSGi e i bundle per lo sviluppo locale.

## Panoramica {#overview}

AEM as a Cloud Service tratta la configurazione e il codice [ come immutabili in fase di esecuzione.](/help/release-notes/aem-cloud-changes.md#apps-libs-immutable) Ciò significa che tutte le configurazioni devono essere distribuite come si farebbe con il codice in un ambiente di produzione. Per le istanze di produzione, questo assicura il superamento dei gate di qualità e offre un livello di stabilità e chiarezza dell’ambiente corrente.

Tuttavia, per testare gli sviluppi locali sono spesso necessari aggiornamenti e modifiche al bundle della [configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) ad hoc. Come parte di [AEM as a Cloud Service SDK,](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) la console Web abilita tali aggiornamenti in tempo reale.

Con AEM as a Cloud Service eseguito localmente, è possibile accedere alla console da `http://<host>:<port>/system/console`.

La console web offre una selezione di schermate e opzioni per la gestione dei bundle OSGi, tra cui:

* [Configurazione](#configuration): per la configurazione dei bundle OSGi ed è quindi il meccanismo sottostante per la configurazione dei parametri di sistema di AEM
* [Bundle](#bundles): per l&#39;installazione dei bundle
* [Componenti](#components): per controllare lo stato dei componenti necessari per AEM
* [Generazione configurazioni OSGi](#generating-osgi-configurations): per generare automaticamente configurazioni OSGi come JSON

Tutte le modifiche apportate vengono immediatamente applicate al SDK in esecuzione. Non è richiesto alcun riavvio.

Nella console web, tutte le descrizioni che menzionano le impostazioni predefinite si riferiscono alle impostazioni predefinite di Sling. AEM dispone di proprie impostazioni predefinite; pertanto, le impostazioni predefinite potrebbero essere diverse da quelle documentate dalla console.

La console Web in Adobe Experience Manager (AEM) si basa sulla [console di gestione Web Apache Felix.](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html) Apache Felix è uno sforzo della community per implementare la piattaforma di servizio OSGi R4, che include il framework OSGi e i servizi standard.

>[!NOTE]
>
>La console web è disponibile solo in AEM as a Cloud Service SDK a scopo di sviluppo locale. Non è disponibile in produzione.

>[!TIP]
>
>Per verificare lo stato delle configurazioni, dei bundle e dei componenti OSGi in un ambiente di produzione, utilizza [Developer Console.](/help/implementing/developing/introduction/aem-developer-console.md)

## Configurazione {#configuration}

La schermata **Configurazione** viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare i parametri di sistema di AEM. È possibile accedere alla scheda **Configurazione** da:

* Menu a discesa: **OSGi -> Configurazione**
* URL: `http://<host>:<port>/system/console/configMgr`

Viene visualizzato un elenco di configurazioni:

![Schermata Configurazione](assets/configuration.png)

Dall’elenco di questa schermata sono disponibili due tipi di configurazioni:

* **Le configurazioni** ti consentono di aggiornare le configurazioni esistenti. Questi hanno un’identità persistente (PID) e possono essere:
   * Standard e integrale in AEM: se eliminati, i valori tornano alle impostazioni predefinite.
   * Istanze create da configurazioni di fabbrica: queste istanze vengono create dall’utente e l’eliminazione comporta la rimozione dell’istanza.
* **Le configurazioni di fabbrica** consentono di creare un&#39;istanza dell&#39;oggetto funzionalità richiesto. Viene allocata a un’identità persistente e quindi elencata nell’elenco Configurazioni.

Selezionando una voce dall’elenco vengono visualizzati i parametri relativi a tale configurazione:

![Parametri di configurazione](assets/configuration-parameters.png)

Puoi quindi aggiornare i parametri come richiesto e:

* **Salva** per salvare le modifiche apportate.
   * Per una configurazione di fabbrica, viene creata un’istanza con un’identità persistente.
   * La nuova istanza viene quindi elencata in Configurazioni.
* **Ripristina** per ripristinare i parametri visualizzati sullo schermo agli ultimi salvati.
* **Elimina** per eliminare la configurazione corrente.
   * Se standard, i parametri vengono ripristinati alle impostazioni predefinite.
   * Se viene creata da una configurazione di fabbrica, l&#39;istanza specifica viene eliminata.
* **Annulla associazione** per annullare l&#39;associazione della configurazione corrente dal bundle.
* **Annulla** per annullare le modifiche correnti.

>[!TIP]
>
>Per ulteriori dettagli sulle configurazioni OSGi, vedi [Configurazione di OSGi per Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Bundle {#bundles}

La schermata **Bundle** viene utilizzata per installare i bundle OSGi necessari per AEM. Lo schermo è accessibile tramite uno dei seguenti metodi:

* Menu a discesa: **OSGi -> Bundle**
* URL: `http://<host>:<port>/system/console/bundles`

Viene visualizzato un elenco di bundle:

![Bundle](assets/bundles.png)

Utilizzando questa schermata è possibile:

* **Installa o aggiorna** per installare un nuovo bundle o aggiornare un bundle esistente.
   * Puoi **Sfogliare** per trovare il file contenente il bundle e specificare se deve **Iniziare** immediatamente e a quale **Livello Inizio**.
* **Ricarica** per aggiornare l&#39;elenco visualizzato.
* **Aggiorna pacchetti** per controllare i riferimenti di tutti i pacchetti e aggiornarli, se necessario.
   * Ad esempio, dopo un aggiornamento, la vecchia e la nuova versione potrebbero essere ancora in esecuzione a causa di riferimenti precedenti. Questa opzione controlla e sposta tutti i riferimenti alla nuova versione, consentendo l’interruzione della versione precedente.
* **Inizia** per avviare un bundle in base al livello iniziale specificato.
* **Interrompi** per arrestare il bundle.
* **Disinstalla** per disinstallare il bundle dal sistema.

L’elenco specifica lo stato del bundle. facendo clic sul nome di un bundle specifico con vengono visualizzate ulteriori informazioni.

>[!TIP]
>
>Dopo **Aggiornamento**, Adobe consiglia di fare clic su **Aggiorna pacchetti**.

## Componenti {#components}

La schermata **Componenti** consente di abilitare e disabilitare i componenti. È accessibile da:

* Menu a discesa: **Principale -> Componenti**
* URL: `http://<host>:<port>/system/console/components`

Viene visualizzato un elenco di componenti. Sono disponibili icone per ogni riga che consentono di abilitare, disabilitare o (se appropriato) aprire i dettagli di configurazione di un componente specifico.

![Componenti](assets/components.png)

Facendo clic sul nome di un particolare componente vengono visualizzate ulteriori informazioni sul suo stato. Qui puoi anche abilitare, disabilitare o ricaricare il componente.

![Dettagli componente](assets/component-details.png)

>[!NOTE]
>
>L’attivazione o la disattivazione di un componente si applica solo fino al riavvio di SDK.
>
>Lo stato iniziale è definito all’interno del descrittore del componente, che viene generato durante lo sviluppo e memorizzato nel bundle al momento della creazione del bundle.

## Generazione di configurazioni OSGi {#generating-osgi-configs}

La console web può essere utilizzata per configurare i componenti OSGi ed esportare le configurazioni OSGi come JSON. Questo è utile per configurare i componenti OSGi forniti da AEM le cui proprietà e formati di valore OSGi potrebbero non essere familiari durante la definizione delle configurazioni OSGi nel progetto AEM.

Per ulteriori informazioni, consulta il documento [Configurazione di OSGi per Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-web-console).
