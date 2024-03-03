---
description: Questo tutorial include istruzioni per rendere ripetibile una sezione di un modulo
title: Sezioni ripetibili in Edge Delivery Services
feature: Edge Delivery Services
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Sezioni ripetibili nella distribuzione Edge

Una sezione ripetibile è un componente di un modulo che viene duplicato o replicato più volte per raccogliere informazioni per più occorrenze degli stessi dati.

Ad esempio, si consideri un modulo utilizzato per raccogliere informazioni dagli utenti che richiedono un prestito. Il modulo consente agli utenti di fornire informazioni personali, compresi i dettagli dei co-prestatori. Gli utenti possono immettere i dettagli per i co-richiedenti; questa sezione può essere ripetuta.

![Sezioni ripetibili nei moduli](/help/forms/assets/eds-repeatable.png)

## Prerequisiti

Configura il progetto GitHub del servizio di consegna Edge (EDS) utilizzando il boilerplate AEM e clona l’archivio GitHub corrispondente sul computer locale. Consulta [tutorial per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html) per i dettagli.

## Sezioni ripetibili nella distribuzione Edge

Prendiamo un esempio di un modulo di richiesta di prestito. Il modulo consente agli utenti di inviare informazioni personali. È possibile includere dettagli co-candidato utilizzando sezioni ripetibili, con la possibilità di aggiungere un minimo e un massimo di tre sezioni co-candidato.

>[!NOTE]
>
> * Puoi creare un Microsoft Excel sul tuo sito SharePoint o Google Drive per rendere i set di campi ripetibili in un modulo.
> * In questo caso, si tratta di Microsoft SharePoint. Per impostare la cartella SharePoint come origine di contenuto, segui i passaggi descritti in [Come utilizzare Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).


Per aggiungere sezioni ripetibili in Edge Delivery:

1. [Creare un modulo con Microsoft Excel](#author-form)
2. [Anteprima e pubblicazione del modulo](#preview-form)

### Creare un modulo con Microsoft Excel {#author-form}

1. Vai al tuo account Microsoft SharePoint e apri o crea la directory del progetto AEM Edge Delivery.
2. Apri un file Microsoft Excel esistente o creane uno nuovo.
In questo esempio viene utilizzato un foglio di Excel denominato `loan-application.xlsx` creato nel sito SharePoint di Microsoft.
3. Aggiungi nuove colonne etichettate come `Repeatable`, `Min`, e `Max` nel file di Microsoft Excel.
4. Specifica il valore per `Repeatable` colonna come `True` per il set di campi che si desidera rendere ripetibile.
5. Specifica i valori per `Min` e `Max` colonne. Il `Min` rappresenta il numero minimo di occorrenze per le quali il pannello si ripete, mentre il `Max` value rappresenta il numero massimo di occorrenze per le quali il pannello si ripete.
6. Salvare il file di Microsoft Excel.

>[!NOTE]
>
> Ecco il [Richiesta di prestito](/help/forms/assets/loan-application.xlsx) foglio excel per riferimento.

### Anteprima/pubblicazione del modulo tramite il servizio di consegna Edge

1. Aprire o creare un nuovo file di documento in un sito di Microsoft SharePoint per incorporare il foglio di Excel in esso utilizzando un `Form Block`. Ad esempio, apri il `index` e aggiungere un `Form Block`.
2. Apri il prompt dei comandi, accedi alla directory del progetto AEM Edge Delivery sul computer locale ed esegui il comando come `aem up`.

Il modulo è accessibile da `https://localhost:3000`, dove si fa clic su `Add` il pulsante aggiunge una nuova sezione ripetibile per l&#39;immissione dei dettagli del co-candidato. È inoltre possibile eliminare la sezione ripetibile facendo clic sul pulsante `Delete` pulsante.

>[!NOTE]
>
> Se si verifica un errore &quot;Pagina non trovata&quot; durante l&#39;accesso al modulo in localhost, aggiungere il nome della directory del sito SharePoint di Microsoft davanti all&#39;URL in cui si trova il modulo. Ad esempio `http://localhost:3000/<dir-name>/`




