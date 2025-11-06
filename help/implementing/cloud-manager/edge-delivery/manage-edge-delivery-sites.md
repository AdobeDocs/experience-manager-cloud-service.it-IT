---
title: Gestire i siti Edge Delivery in Cloud Manager
description: Scopri come aggiungere una configurazione CDN a un sito Edge Delivery o eliminare un sito di Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 100%

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
