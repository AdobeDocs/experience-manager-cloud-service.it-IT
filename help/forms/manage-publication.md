---
title: Come si pubblicano o annullano la pubblicazione dei moduli nelle istanze di anteprima o pubblicazione?
description: Scopri come pubblicare o annullare la pubblicazione di moduli dall’ambiente di authoring AEM per visualizzare in anteprima o pubblicare le istanze. Sia che si eseguano test dei moduli in un ambiente di staging o che si distribuiscano in tempo reale per gli utenti finali, AEM fornisce strumenti semplificati per gestire questo processo in modo efficiente.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, manage publication, , AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: 242dcbc5bb541dfac601454fb75dec3bdff1ea64
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---


# &#x200B;Gestisci pubblicazione in Experience Manager Forms

In qualità di amministratore di Adobe Experience Manager Forms, puoi pubblicare i moduli dall’istanza di authoring a Experience Manager Forms. È possibile pianificare la pubblicazione di un modulo o di una cartella in una data o in un&#39;ora successiva. Dopo la pubblicazione, gli utenti possono accedere e compilare i moduli.

Puoi pubblicare o annullare la pubblicazione del modulo utilizzando le opzioni Publish o Gestisci pubblicazione disponibili nell’interfaccia di Experience Manager Forms. Se si apportano modifiche successive ai moduli o alla cartella originali in Experience Manager Forms, tali modifiche non verranno applicate nell&#39;istanza di pubblicazione fino a quando non si ripubblica da Experience Manager Forms. In questo modo le modifiche in corso di lavorazione non sono disponibili nell’istanza di pubblicazione. Nell’istanza di pubblicazione sono disponibili solo le modifiche pubblicate da un amministratore.

## Opzione Publish forms using Publish

L’opzione Pubblica consente di pubblicare immediatamente un modulo. Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo da pubblicare. Fai clic su Publish nella barra degli strumenti, controlla tutte le risorse di riferimento che verranno pubblicate con il modulo e fai clic su Publish.

Schermata di un computer

Descrizione generata automaticamente

## Publish o annullare la pubblicazione di moduli tramite Gestisci pubblicazione


Gestisci pubblicazione consente di pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, di aggiungere contenuto all’elenco di pubblicazione dalla cartella Moduli e documenti, di selezionare i riferimenti da pubblicare e pianificare la pubblicazione a una data o un’ora successiva.


Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo da pubblicare. Fai clic su Gestisci pubblicazione nella barra degli strumenti.


Schermata di un computer

Descrizione generata automaticamente



Nell’interfaccia Gestisci pubblicazione sono disponibili le seguenti opzioni:

* Azioni

   * Publish: Publish forms per la destinazione selezionata
   * Annulla pubblicazione: annulla la pubblicazione dei moduli dalla destinazione

* Destinazione

   * Publish: istanza Publish da Publish forms a Experience Manager Forms (AEM).
   * Anteprima: istanza di anteprima da Publish Forms a Experience Manager Forms (AEM).

* Pianificazione

   * Ora: Publish Forms immediatamente
   * In seguito: Publish Forms basato sulla data o sull’ora di attivazione



Per continuare, fare clic su **Avanti**. Nella scheda Ambito utilizza le opzioni Aggiungi contenuto per aggiungere altro contenuto da pubblicare. È ad esempio possibile aggiungere altri file Forms o Document of Record.

### Aggiungi contenuto

La pubblicazione in Experience Manager Forms consente di aggiungere ulteriore contenuto (moduli, risorse e cartelle) all’elenco di pubblicazione. È possibile aggiungere più moduli, risorse o cartelle all&#39;elenco dalla cartella formsanddocuments. Tuttavia, non è possibile aggiungere risorse da più cartelle alla volta.

Schermata di un computer

Descrizione generata automaticamente

Fai clic sul pulsante **Aggiungi contenuto** per aggiungere altro contenuto. Puoi aggiungere più risorse da una cartella o più cartelle alla volta. Tuttavia, non è possibile aggiungere risorse da più cartelle alla volta.

Per configurare i riferimenti da pubblicare o meno per un modulo o altre risorse, seleziona il modulo o la risorsa e fai clic su Riferimenti pubblicati.

Schermata di un computer

Descrizione generata automaticamente

Nella finestra di dialogo Riferimenti pubblicati, deseleziona le risorse che intendi non pubblicare e fai clic su Fine.


Schermata di un computer

Descrizione generata automaticamente


## Publish o annullare la pubblicazione di un modulo in un secondo momento


Oltre a consentire di pubblicare o annullare la pubblicazione dei moduli in una data e in un’ora successive, l’opzione Pubblica o Annulla pubblicazione successiva consente anche di configurare un flusso di lavoro. I moduli vengono pubblicati o non pubblicati dopo il completamento del workflow. Per pianificare la pubblicazione o l&#39;annullamento della pubblicazione di un modulo:

1. Dalla console Experience Manager Forms, passa alla cartella principale e seleziona il modulo da pianificare per la pubblicazione.
1. Fai clic su Gestisci pubblicazione nella barra degli strumenti.
1. Fai clic su Publish o su Annulla pubblicazione da azione, quindi seleziona la Destinazione in cui desideri pubblicare o annullare la pubblicazione del contenuto.

   * Anteprima: utilizza l’opzione Anteprima per pubblicare o annullare la pubblicazione in un ambiente di anteprima Experience Manager Forms. Gli ambienti di anteprima Experience Manager Forms vengono utilizzati per testare i moduli di sviluppo.
   * Publish: utilizza l’opzione Experience Manager Forms Publish per inviare il modulo all’ambiente di pubblicazione Experience Manager Forms quando è pronto per l’uso in un ambiente di produzione.


1. Seleziona Più tardi in Pianificazione.

1. Selezionare una data di attivazione e specificare la data e l&#39;ora. Fai clic su Avanti.

   Schermata di un computer

   Descrizione generata automaticamente

1. Nella scheda Ambito, aggiungi contenuto (se necessario). Fai clic su Avanti.

   Schermata di un computer

   Descrizione generata automaticamente

1, (Facoltativo) Nella scheda Flussi di lavoro, specifica un titolo Flusso di lavoro. Fai clic su Publish Later (Più tardi).

Schermata di un computer

Descrizione generata automaticamente

## Determinazione dello stato di pubblicazione

Esistono diversi modi per determinare lo stato di pubblicazione:

* Accedi all’istanza di destinazione per verificare i moduli pubblicati e altre risorse (a seconda della data o dell’ora pianificata).

* Utilizza la vista timeline per determinare lo stato della pubblicazione.

* Utilizza il menu Informazioni pagina nell’editor di Forms adattivo.