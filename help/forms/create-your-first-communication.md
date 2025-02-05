---
title: Creare la prima comunicazione interattiva
description: Progettazione di comunicazioni dinamiche e basate su dati con facilità grazie alle comunicazioni interattive AEM Forms
feature: Release Information
role: Admin
hide: true
hidefromtoc: true
source-git-commit: a771aa7e683cfbcacc8a9d5765c63d50169a2756
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 3%

---


# Creare la prima comunicazione interattiva


>[!VIDEO](https://video.tv.adobe.com/v/3444094/)

## Passaggio 1: pianificare la comunicazione interattiva

Il primo passo nella pianificazione di una comunicazione interattiva è finalizzare il contenuto della comunicazione interattiva. Dopo aver finalizzato il contenuto, devi analizzarlo per identificare i vari tipi di risorse necessari per creare la comunicazione interattiva.

### Considerazioni sulla pianificazione

Una comunicazione interattiva include i seguenti elementi:

* **Il testo statico** include principalmente le parti della comunicazione interattiva che sono di natura generica e sono incluse nella comunicazione a tutti i clienti. Ad esempio, intestazione, piè di pagina, formula introduttiva o disclaimer.

* **I dati originati da un sistema back-end (modello dati modulo)** sono specifici del cliente e vengono uniti in modo dinamico alla comunicazione interattiva. Ad esempio, il numero o l’indirizzo del criterio può essere originato utilizzando il modello dati del modulo.

* **Layout o modelli** per la versione per la stampa e per il Web della comunicazione interattiva.

* **Ordine** in cui vengono visualizzati i vari paragrafi di testo nella comunicazione interattiva.

* **Dati condizionali** che vengono popolati in base a condizioni predefinite. Ad esempio, la data in cui viene generata la comunicazione interattiva.

* **Immagini archiviate in un repository**, ad esempio loghi e immagini di firma. Immagini come i logo aziendali appaiono nella maggior parte o in tutta la comunicazione interattiva.

* **Grafici e tabelle** necessari per semplificare la rappresentazione di dati complessi in una comunicazione interattiva

### Anatomia della comunicazione interattiva

Dopo aver finalizzato i contenuti e gli elementi utilizzati per creare la comunicazione interattiva, puoi creare un’anatomia della comunicazione interattiva. L&#39;anatomia deve avere i dettagli elencati nella sezione Considerazioni sulla pianificazione. Ad esempio, un&#39;anatomia della fattura mensile che un operatore di telecomunicazioni invia ai propri clienti.

L&#39;anatomia include dati con le seguenti modalità di input:

* Testo statico
* Modello dati modulo
* Dati condizionali
* Immagini


## Passaggio 2: creare il modello dati del modulo

Un modello per dati modulo consente di collegare una comunicazione interattiva per utilizzare origini dati diverse. Ad esempio, profilo utente AEM, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. Un modello dati modulo è uno schema di rappresentazione dati unificato di entità business e servizi disponibili nelle origini dati connesse. È possibile utilizzare il modello dati del modulo con una comunicazione interattiva per recuperare i dati dalle origini dati connesse. Per ulteriori informazioni sul modello dati modulo, vedere [Integrazione dati AEM Forms](/help/forms/data-integration.md).

## Passaggio 3: creare frammenti

I frammenti di documento sono componenti riutilizzabili di una corrispondenza utilizzati per comporre una comunicazione interattiva. I frammenti di documento sono di tipo Testo, Elenco e Condizione.


## Passaggio 4: creare modelli

L&#39;editor di comunicazioni interattive fornisce più modelli OOTB. Puoi modificare questi modelli in base ai requisiti della tua organizzazione o creare un modello da zero.


## Passaggio 5: creare una comunicazione interattiva

Dopo aver creato tutti i blocchi predefiniti, ad esempio il modello di dati del modulo, i frammenti di documento e i modelli per la versione web, puoi iniziare a creare una comunicazione interattiva. Per iniziare a creare una comunicazione interattiva:

1. Accedi all’ambiente AEM Forms as a Cloud Service.
1. Passa a Forms > Forms e documenti
1. Fai clic su **Crea** e seleziona **Documento di comunicazione**. Viene visualizzata una schermata di configurazione per impostare le seguenti opzioni:

   | Campo | Descrizione | Obbligatorio |
   |-------|-------------|----------|
   | Nome | Identificatore univoco della comunicazione | Sì |
   | Titolo | Nome visualizzato della comunicazione | Sì |
   | Descrizione | Breve descrizione dello scopo della comunicazione | No |
   | Modello | Seleziona un modello preconfigurato o inizia da zero | Sì |
   | Tag | Aggiungere tag di metadati per migliorare l’organizzazione | No |

1. Passa alla scheda Predefiniti e configura le seguenti opzioni:

   | Campo | Descrizione |
   |-------|-------------|
   | Elenco predefiniti | Selezionare un predefinito preconfigurato per le dimensioni del documento. Le opzioni più comuni includono A4, Letter e altro ancora. |
   | Larghezza predefinita | Visualizza la larghezza del predefinito per l&#39;elenco di predefiniti selezionato. |
   | Altezza predefinita | Visualizza l&#39;altezza del predefinito per l&#39;elenco di predefiniti selezionato. |
   | Unità predefinita | Selezionare l&#39;unità di misura per le dimensioni del documento, ad esempio millimetri, pollici. |
   | Orientamento predefinito | Scegliere l&#39;orientamento del documento, Verticale o Orizzontale. |

1. Fai clic su **Crea**. La comunicazione viene aperta nell’editor.
1. Trascina e rilascia componenti e frammenti per progettare la comunicazione interattiva.

   * Utilizza **Pagina master** per il contenuto comune tra le pagine. Le pagine master sono progettate per formattare le pagine e facilitano la coerenza della progettazione in quanto possono fornire uno sfondo e un formato di layout per più pagine in una progettazione di documenti.

   * Utilizza **Pagine** per creare il layout del contenuto e del layout del documento. Ogni pagina deriva le dimensioni e l&#39;orientamento da una pagina master e, per impostazione predefinita, ogni pagina è associata alla pagina master predefinita creata da Designer.


1. Utilizza la notazione `@` per completare automaticamente i campi dati in base al modello dati connesso.
1. Utilizzare l&#39;opzione `PDF Preview` per visualizzare in anteprima il documento insieme ai dati. È necessario specificare il file di dati in formato JSON.
