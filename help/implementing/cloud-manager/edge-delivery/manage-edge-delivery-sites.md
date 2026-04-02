---
title: Gestire i siti Edge Delivery in Cloud Manager
description: Scopri come aggiungere una configurazione CDN a un sito Edge Delivery o eliminare un sito di Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: fc9f7f10d1797bda5f31d82005b0afbb6ea1e644
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 64%

---

# Gestire i siti di Edge Delivery in Cloud Manager {#manage-edge-delivery-sites}

Scopri come gestire i siti di Edge Delivery in Cloud Manager aggiungendo una configurazione CDN a un sito esistente. In alternativa, elimina un sito di Edge Delivery.

## Aggiungere una mappatura di dominio a un sito Edge Delivery esistente {#add-cdn-to-edge-delivery-site}

Consulta [Aggiungere una mappatura di dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Rinominare un sito di Edge Delivery (#rename-edge-delivery-site)

In Adobe Cloud Manager, potrebbe essere utile rinominare un sito di Edge Delivery per diversi motivi:

* **Chiarezza e organizzazione**: descrivere meglio lo scopo del sito o l’ambiente ad esso associato (ad esempio, produzione, staging).
* **Evitare confusione**: se sono in uso più siti, rinominarli consente di distinguerli facilmente, riducendo la possibilità di applicare configurazioni o aggiornamenti al sito errato.
* **Standardizzazione**: seguire una convenzione di denominazione coerente che sia in linea con le linee guida della propria organizzazione per semplificare la gestione e il controllo.

**Per rinominare un sito di Edge Delivery:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito di Edge Delivery.
1. Effettua una delle operazioni seguenti:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Nella tabella del sito di Edge Delivery, fai clic sui puntini di sospensione alla fine di una riga di cui desideri rinominare il sito.
Fai clic su **Rinomina**.
   * Nell’angolo superiore sinistro della pagina fai clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu sul lato sinistro. Nell’intestazione **Servizi** fai clic sull’![icona Pagine web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.
Nella tabella del sito di Edge Delivery, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui vuoi rinominare il sito. Fai clic su **Rinomina**.

1. Nella finestra di dialogo **Modifica sito Edge Delivery** immetti il nuovo nome del sito nel campo di testo **Nome sito**.
1. Fai clic su **Modifica**.


## Attivare il livello di pubblicazione per un sito Edge Delivery (Beta) {#activate-publish-tier-for-eds}

>[!NOTE]
>
>La funzione di pubblicazione qui descritta è in Beta. Per partecipare a Beta, invia un&#39;e-mail a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con il tuo ID organizzazione Adobe e l&#39;ID programma.

Questa funzionalità si applica solo ai siti Edge Delivery creati con l&#39;opzione **Authoring di AEM** nei programmi in cui è abilitata la funzione del livello di pubblicazione flessibile.

Se il sito Edge Delivery utilizza l’authoring di AEM, per impostazione predefinita non viene eseguito il provisioning del livello di pubblicazione perché Edge Delivery gestisce la distribuzione dei contenuti. Tuttavia, puoi attivare il livello di pubblicazione in qualsiasi momento, se il sito lo richiede. Ad esempio, se devi supportare la pubblicazione tradizionale AEM insieme ad Edge Delivery.

Dopo aver creato il sito Edge Delivery e aver visualizzato il relativo stato **Verificato** in Cloud Manager, puoi creare e pubblicare contenuti con AEM Universal Editor.

**Per accedere all&#39;editor universale da Cloud Manager:**

1. Nell’elenco Siti Edge Delivery della scheda Edge Delivery individua il tuo sito.

   ![Pubblicazione di contenuto da AEM Author ad Edge Delivery.](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. Fare clic sul collegamento **Source dei contenuti** nella riga del sito. Il collegamento consente di aprire la pagina AEM Universal Editor, da cui è possibile creare e modificare i contenuti del sito.—>

**Per attivare il livello di pubblicazione per un sito Edge Delivery:**

1. Nella pagina **Panoramica programma**, nella scheda **Consegna pubblicazione**, nella scheda **Ambiente**, fai clic sull&#39;icona Informazioni.

1. Nel pop-up informativo, in **URL pubblicazione**, seleziona **Fai clic per attivare** per abilitare il provisioning del livello di pubblicazione nell&#39;interfaccia utente di Cloud Manager.

   ![Fare clic per attivare il provisioning del livello di pubblicazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

1. Nella finestra di dialogo Attiva livello di pubblicazione fare clic su **Attiva**.

   ![Finestra di dialogo Attiva livello di pubblicazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

   Una volta attivato, il livello di pubblicazione viene fornito automaticamente. In alternativa, è possibile eseguire automaticamente il provisioning del livello di pubblicazione se l’autore tenta di pubblicare contenuti direttamente dall’interfaccia utente di AEM.

   Dopo l&#39;attivazione e il provisioning del livello di pubblicazione, il collegamento **Fai clic per attivare** diventa inattivo/non disponibile.

* **Da AEM Author**: nell&#39;interfaccia di authoring di AEM, fai clic su **Pubblicazione rapida** per pubblicare i contenuti direttamente sul tuo sito Edge Delivery. Il livello di pubblicazione non è necessario per questa operazione quando Edge Delivery gestisce la consegna.

Dopo la pubblicazione, visualizza l&#39;anteprima del contenuto all&#39;URL `.page` del sito o in tempo reale all&#39;URL `.live`.—>

>[!NOTE]
>
>L’attivazione del livello di pubblicazione aggiunge l’infrastruttura di pubblicazione all’ambiente. Questa funzionalità può influire sul consumo di risorse del programma. Per configurare se il livello di pubblicazione è obbligatorio a livello di programma, vedere [Livello di pubblicazione flessibile (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).


## Eliminare un sito di Edge Delivery {#delete-edge-delivery-site}

Se elimini un sito Edge Delivery Services, vengono rimosse anche le configurazioni CDN associate. Questa azione interrompe la connessione tra i domini personalizzati e il sito. Per ulteriori dettagli, consulta Configurazioni CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Per eliminare un sito di Edge Delivery:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma con Edge Delivery Services configurati, in cui si desidera aggiungere un sito di Edge Delivery.
1. Effettua una delle operazioni seguenti:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Nella tabella del sito di Edge Delivery, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui vuoi rimuovere il sito.
Fai clic sull’![icona Elimina sito Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Elimina**, quindi fai di nuovo clic su **Elimina** per confermare la rimozione del sito.

     ![Aggiungere un sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra. Sotto l’intestazione **Servizi**, fai clic sull’![icona Pagina web per siti Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.
Nella tabella del sito Edge Delivery, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui vuoi rimuovere il sito. Fai clic sull’![icona Elimina sito di Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Elimina**, quindi fai di nuovo clic su **Elimina** per confermare la rimozione del sito.

     ![Aggiungere un sito di Edge Delivery dal pulsante Siti di Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Gestire un sito Edge Delivery da Helix 4 a Helix 5

Utilizzare l’endpoint API `/program/{programId}/site/{siteId}` per eseguire la migrazione di un sito Edge Delivery da Helix 4 a Helix 5.

>[!IMPORTANT]
>
>Le configurazioni CDN per i siti web Helix 4 non possono essere migrate automaticamente a Helix 5. Questo limite esiste perché i siti in produzione della clientela possono ancora essere eseguiti su Helix 4, mentre le versioni Helix 5 sono ancora in fase di sviluppo.

**Prerequisiti**

* `sitename` deve esistere già.
* Conoscere i valori `branchName`, Helix `version` e `repo` appropriati.
* La migrazione modifica solo `branchName`, Helix `version` e `repo`. Il campo proprietario non può essere modificato.

**Formato API**

```http
PUT /api/program/{programId}/site/{siteId}
```

**Parametri corpo richiesta**
Crea una sostituzione di un sito Edge Delivery per applicare l’origine specificata nel corpo della richiesta.

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### Esempio 1: migrazione a Helix 5

**HTTP**

```http
PUT /api/program/{programId}/site/{siteId}
```

**JSON**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**Risultato URL origine**
Restituisce un sito Edge Delivery con il seguente URL di origine:

`"origin": "branch--my-website–Teo48.aem.live"`


### Esempio 2: migrazione a Helix 4

**HTTP**

```http
PUT /api/program/{programId}/site/{siteId}
```

**JSON**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**Risultato URL origine**
Restituisce un sito Edge Delivery con il seguente URL di origine:

`"origin": "branch--my-website--Teo48.hlx.live"`

### Esempio 3: migrazione di un sito senza archivio a Helix 5

**HTTP**

```http
PUT /api/program/{programId}/site/{siteId}
```

**JSON**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**Risultato URL origine**
Restituisce un sito Edge Delivery con il seguente URL di origine:

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## Registrare un ticket di supporto {#eds-support-ticket}

{{support-ticket}}
