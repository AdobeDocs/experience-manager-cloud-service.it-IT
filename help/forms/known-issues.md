---
title: Problemi noti e limitazioni
description: Problemi noti e limitazioni di  [!DNL AEM Forms] ambiente as a Cloud Service
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 63f6e7c6df7404062aa0d209496506bdabcf564c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 10%

---

# Problemi noti e limitazioni {#known-issues-and-limitations}

Prima di iniziare a utilizzare [!DNL AEM Forms] as a Cloud Service, esamina i seguenti problemi noti e limitazioni:

## Problemi noti {#known-issues}

* Fino a nuovo avviso, non aggiungere ed eseguire un test che invia un modulo adattivo da un’istanza Publish a un flusso di lavoro AEM in esecuzione su un’istanza Author.

* Quando importi un modulo adattivo che utilizza un modello contenente **[!UICONTROL Salva]** pulsante, il pulsante **[!UICONTROL Salva]** continua a essere visualizzato nel modulo adattivo anche dopo essere stato rimosso dal modello corrispondente. Rimuovi il **[!UICONTROL Salva]** dal Forms adattivo prima di pubblicarlo. Tieni d’occhio le note sulla versione per verificare la disponibilità del portale Forms e della funzione Salva come bozza da ripristinare e utilizzare il pulsante.

* Il **[!UICONTROL Imposta variabile]** Il passaggio dei flussi di lavoro AEM non supporta le variabili dell’elenco di array di tipo. È possibile utilizzare il passaggio del processo per impostare variabili di tipo elenco matrice.

* Quando invii un modulo adattivo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, il contenuto del file non viene inviato e viene ricevuto un file da 0 byte all’altra estremità. Il problema si verifica in modo intermittente e solo quando si utilizza l’invio sincrono. Questo è un [problema noto](https://feedbackassistant.apple.com/feedback/9117687) in Apple iOS.

* Quando invii un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file da 0 byte all’altra estremità. Questo è un problema noto in Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service non genera miniature per i file di schema XDP e JSON. Al posto delle miniature, vengono visualizzate le icone predefinite.

  ![Problema noto della miniatura del Forms](/help/forms/assets/forms-tumbnail-known-issue.png)

* Quando si utilizza uno schema con elementi ripetibili per creare un modulo adattivo basato su Componenti core, l’opzione di trascinamento degli elementi ripetibili dalla struttura del modello dati nell’editor di Forms adattivo non funziona.

## Limitazioni {#limitations}

* Il supporto per Forms adattivo basato su XFA non è immediatamente disponibile. Se desideri utilizzare Forms adattivo basato su XFA, contatta il Supporto Adobe con i dettagli del caso d’uso e i requisiti specifici.

