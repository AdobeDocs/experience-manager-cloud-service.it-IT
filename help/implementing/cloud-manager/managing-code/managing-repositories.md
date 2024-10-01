---
title: Gestione degli archivi in Cloud Manager
description: Scopri come aggiungere, visualizzare ed eliminare gli archivi Git in Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b35b25bcd62c28f7894171b7b2269fa46d612686
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 20%

---


# Gestire archivi in Cloud Manager {#managing-repos}

Scopri come visualizzare, aggiungere ed eliminare gli archivi Git in Cloud Manager.

## Informazioni sugli archivi in Cloud Manager {#overview}

Gli archivi in Cloud Manager vengono utilizzati per memorizzare e gestire il codice del progetto utilizzando Git. Per ogni *programma* aggiunto, viene automaticamente creato un archivio gestito da Adobe.

Inoltre, puoi creare altri archivi gestiti da Adobe o aggiungere archivi privati. Tutti gli archivi collegati al programma possono essere visualizzati nella pagina **Archivi**.

Gli archivi creati all’interno di Cloud Manager possono essere selezionati anche quando si aggiungono o modificano le pipeline. Per ulteriori informazioni sulla configurazione delle pipeline, consulta [Pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Ogni pipeline è collegata a un archivio o ramo principale. Tuttavia, con il supporto per il modulo secondario [Git](git-submodules.md), è possibile includere più rami secondari durante il processo di compilazione.

## Visualizzare la pagina Archivi {#repositories-window}

Nella pagina **Archivi** è possibile visualizzare i dettagli dell&#39;archivio selezionato. Queste informazioni includono il tipo di archivio in uso. Se l&#39;archivio è contrassegnato come **Adobe**, indica che si tratta di un archivio gestito da Adobe. Se è etichettato come **GitHub**, fa riferimento a un archivio GitHub privato che gestisci. Inoltre, la pagina fornisce dettagli quali quando è stato creato l’archivio e le relative pipeline associate.

Per intervenire su un repository selezionato, è possibile fare clic su di esso e utilizzare l&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire un menu a discesa. Ad Adobe, gli archivi gestiti possono **[Controllare rami / Creare un progetto](#check-branches)**.

![Azioni archivio](assets/repository-actions.png)
*Menu a discesa nella pagina Archivi.*

Altre azioni disponibili nel menu a discesa includono **[Copia URL archivio](#copy-url)**, **[Visualizza e aggiorna](#view-update)** e **[Elimina](#delete)** l&#39;archivio.

**Per visualizzare la pagina Archivi:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nella pagina **Panoramica programma**, dal menu laterale, fare clic sull&#39;icona ![Cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Archivi**.

1. Nella pagina **Archivi** sono visualizzati tutti gli archivi associati al programma selezionato.

   ![Pagina repository](assets/repositories.png)
   *Pagina Archivi in Cloud Manager.*

## Aggiungere un archivio {#adding-repositories}

Per aggiungere un archivio, l&#39;utente deve avere il ruolo **Responsabile dell&#39;implementazione** o **Proprietario business**.

Nella pagina **Archivi**, nell&#39;angolo superiore destro, fare clic su **Aggiungi archivio**

![Finestra di dialogo Aggiungi archivio.](assets/repository-add.png)
*Finestra di dialogo Aggiungi archivio.*

Cloud Manager supporta due tipi di repository: repository gestiti da Adobe (**repository Adobe**) e repository gestiti automaticamente (**repository privato**). I campi obbligatori per l’impostazione variano a seconda del tipo di archivio scelto per l’aggiunta. Per ulteriori informazioni, consulta:

* [Aggiungere archivi Adobe in Cloud Manager](adobe-repositories.md)
* [Aggiungere archivi privati in Cloud Manager](private-repositories.md)

Per ogni azienda o organizzazione IMS, vi è un limite di 300 archivi per tutti i programmi.

## Accedere alle informazioni dell’archivio {#repo-info}

Quando visualizzi gli archivi nella finestra **Archivi**, puoi visualizzare i dettagli su come accedere agli archivi gestiti da Adobe a livello di programmazione facendo clic sul pulsante **Accedi a dati archivio** nella barra degli strumenti.

![Informazioni sull’archivio](assets/repository-access-repo-info2.png)

La finestra **Informazioni archivio** si apre con i dettagli. Per ulteriori informazioni sull’accesso alle informazioni dell’archivio, consulta [Accesso alle informazioni sull’archivio](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

## Controlla rami/Crea progetto {#check-branches}

In **AEM Cloud Manager**, l&#39;azione **Controlla rami / Crea progetto** ha due scopi, a seconda dello stato corrente dell&#39;archivio.

* Se l&#39;archivio è stato appena creato, questa azione genera un progetto di esempio utilizzando [l&#39;archetipo del progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview).
* Se il progetto di esempio è già stato creato nel repository, l’azione controlla lo stato del repository e dei relativi rami, fornendo feedback sull’esistenza del progetto di esempio.

  ![Azione Controlla rami](assets/check-branches.png)

## Copia URL archivio {#copy-url}

L&#39;azione **Copia URL archivio** copia l&#39;URL dell&#39;archivio selezionato nella pagina **Archivi** negli Appunti per utilizzarlo altrove.

## Visualizzare e aggiornare un archivio {#view-update}

L&#39;azione **Visualizza e aggiorna** apre la finestra di dialogo **Aggiorna archivio**, in cui è possibile visualizzare l&#39;anteprima dell&#39;URL del repository **Nome** e ****. Consente inoltre di aggiornare la **Descrizione** dell&#39;archivio.

![Visualizzare e aggiornare le informazioni del dell’archivio](assets/repository-view-update.png)

## Eliminare un archivio {#delete}

L’azione **Elimina** rimuove l’archivio dal progetto. Un archivio non può essere eliminato se è associato a una pipeline.

![Elimina](assets/repository-delete.png)

L’eliminazione di un archivio rende il suo nome inutilizzabile per tutti i nuovi archivi creati in futuro. Se si tenta di aggiungere un repository utilizzando lo stesso nome di un repository eliminato, viene visualizzato il seguente messaggio di errore:

`Repository name should be unique within organization.`

Inoltre, l’archivio eliminato non è più disponibile in Cloud Manager e non può essere collegato ad alcuna pipeline.

