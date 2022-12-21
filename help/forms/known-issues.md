---
title: Problemi noti e limitazioni
description: Problemi noti e limitazioni di  [!DNL AEM Forms] Ambiente as a Cloud Service
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 94825e3b60d970fec5bf696d932ca66bb83fd2f3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 11%

---

# Problemi noti e limitazioni {#known-issues-and-limitations}

Prima di iniziare a utilizzare [!DNL AEM Forms] as a Cloud Service, controlla i seguenti problemi noti e limitazioni:

## Problemi noti {#known-issues}

* Non aggiungere ed eseguire un test per l’invio di un modulo adattivo da un’istanza di pubblicazione a un flusso di lavoro AEM in esecuzione su un’istanza di authoring fino a nuovo avviso.

* Quando si importa un modulo adattivo che utilizza un modello contenente **[!UICONTROL Salva]** il pulsante **[!UICONTROL Salva]** Il pulsante continua a essere visualizzato nel modulo adattivo anche dopo essere stato rimosso dal modello corrispondente. Rimuovi **[!UICONTROL Salva]** dal Forms adattivo prima di pubblicarlo. Controlla le note sulla versione per verificare la disponibilità del portale Forms e la funzione Salva come bozza per ripristinare e utilizzare il pulsante .

* La **[!UICONTROL Imposta variabile]** passaggio di flussi di lavoro AEM non supporta le variabili di tipo elenco array. È possibile utilizzare il passaggio del processo per impostare variabili di tipo elenco array.

* Quando si invia un modulo adattivo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altra parte. Il problema si verifica a intermittenza e solo quando si utilizza l’invio sincrono. Questa è una [problema noto](https://feedbackassistant.apple.com/feedback/9117687) in Apple iOS.

* Quando si invia un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altro lato. Questo è un problema noto in Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service non genera miniature per i file di schema XDP e JSON. Il servizio visualizza le icone predefinite al posto delle miniature.

   ![Problema noto della miniatura di Forms](/help/forms/assets/forms-tumbnail-known-issue.png)


## Limitazioni {#limitations}

* Il supporto per Forms adattivo basato su XFA non è immediatamente disponibile. Se desideri utilizzare Forms adattivo basato su XFA, contatta il Supporto Adobe con i dettagli del caso d’uso e i requisiti specifici.

