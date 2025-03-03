---
title: Informazioni su editor universale - Tutorial per sviluppatori
description: Questo tutorial ti consentirà rapidamente di utilizzare l’interfaccia dell’editor universale. Ti fornisce una guida alla comprensione dell’interfaccia utente per la creazione di moduli Edge Delivery Services personalizzati nell’editor universale.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 744f505c8e97b6ca6947b685ddb1eba41b370cfa
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 96%

---

# Esplorazione dell’interfaccia dell’editor universale (WYSIWYG)

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) offre un&#39;interfaccia What You See Is What You Get (WYSIWYG) semplice, visiva e intuitiva per Adobe Edge Delivery Services Forms. Fornisce un’interfaccia moderna con funzionalità di trascinamento per l’authoring efficiente dei moduli.

![Interfaccia utente dell’editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Informazioni sull’interfaccia dell’editor universale

Quando il modulo viene modificato dall’autore utilizzando l’editor universale, la console apre un’interfaccia WYSIWYG interattiva che consente di iniziare a modificare il modulo.

>[!NOTE]
>
> Per informazioni sull’authoring dei moduli con l’editor universale, consulta l’articolo [Guida introduttiva di Edge Delivery Services per AEM Forms utilizzando l’editor universale (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interfaccia utente dell’editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

L’interfaccia dell’editor universale è divisa in quattro parti:

* **[A: intestazione di Experience Cloud](#experience-cloud-header)**
* **[B: barra degli strumenti dell’editor universale](#universal-editor-toolbar)**
* **[C: pannello Proprietà](#properties-panel)**
* **[D: editor](#editor)**

### Intestazione di Experience Cloud

L’intestazione di Experience Cloud si trova nella parte superiore della console. Fornisce informazioni sulla posizione attuale all’interno di Experience Cloud. Consente inoltre di passare ad altre applicazioni di Experience Cloud.

![Intestazione editor universale Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


Comprendiamo ciascuno dei suoi componenti.

* **Adobe Experience Cloud**

  Puoi fare clic sul collegamento **Adobe Experience Cloud** sul lato sinistro della schermata per passare alla directory principale della soluzione Experience Manager e accedere a strumenti come Experience Manager Sites, Experience Manager Assets e Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **Nome organizzazione**

  Il **nome organizzazione** mostra il nome dell’organizzazione IMS a cui hai effettuato l’accesso. Se hai accesso, puoi passare a un’altra organizzazione IMS selezionandola dall’elenco a discesa. Ad esempio, il nome dell’organizzazione IMS attualmente selezionato è `AEM Forms Internal01`.

  ![Organizzazione](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **Guida**

  L’icona della guida fornisce un accesso rapido alle risorse di apprendimento e supporto. L’autore del modulo può anche aggiungere il feedback nella sezione **Guida**.
  ![Guida](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **Notifiche**

  La sezione **Notifica** mostra il numero di notifiche incomplete attualmente assegnate, le richieste e le attività correnti nell’organizzazione IMS.

  ![Notifica](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **Soluzioni**

  Puoi passare ad altre soluzioni di Experience Cloud utilizzando il collegamento **Soluzioni**.
  ![Soluzioni](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **Autore**
L’icona rappresenta i dettagli dell’autore del modulo e il nome dell’organizzazione IMS a cui l’autore ha effettuato l’accesso.
  ![Autore](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### Barra degli strumenti dell’editor universale

La barra degli strumenti consente di passare ad altri moduli e di modificarli. Consente inoltre di pubblicare o annullare la pubblicazione del modulo, di modificarne le proprietà e di accedere all’editor di regole.
![Barra degli strumenti dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Comprendiamo ciascuno dei suoi componenti.

* **Pulsante Home**
Il pulsante Home consente di passare alla pagina iniziale dell’editor universale. Puoi anche immettere direttamente l’URL del modulo che desideri modificare utilizzando l’editor universale.
  ![Pagina Home dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **Barra della posizione**
La **barra della posizione** mostra l’indirizzo del modulo che l’autore sta modificando. Puoi anche immettere l’URL di un altro modulo facendo clic sulla barra della posizione. Il tasto di scelta rapida per aprire la barra della posizione è il tasto `l`.
  ![Barra della posizione](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **Editor di regole**

  L’**editor di regole** offre un’interfaccia visiva intuitiva per la creazione e la gestione delle regole. È possibile aggiungere il comportamento di un modulo dinamico utilizzando l’editor di regole.

  ![Editor di regole](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * Nell’editor universale, l’estensione editor di regole non è attivata per impostazione predefinita. Per abilitare l’estensione editor di regole, scrivi all’indirizzo [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) dal tuo ID e-mail ufficiale.
  > * Per informazioni su come creare regole, consulta all’articolo [Introduzione all’editor di regole nell’authoring WYSIWYG](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

* **Modifica proprietà modulo**
Puoi modificare le proprietà del modulo, ad esempio il modello dati modulo e la data di pubblicazione, facendo clic sull’opzione **Modifica proprietà modulo**.
  ![Modifica proprietà modulo](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **Impostazioni intestazione dell’autenticazione**
**Impostazioni intestazione dell’autenticazione** consente all’autore di impostare un’intestazione dell’autenticazione personalizzata per lo sviluppo locale.
  ![intestazione autenticazione](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **Modalità reattiva**
  L’opzione **Modalità reattiva** consente di definire la modalità di rendering del modulo nell’editor universale. Per impostazione predefinita, l’editor si apre in un layout del desktop, dove l’altezza e la larghezza vengono definite automaticamente dal browser. In alternativa, è possibile scegliere di emulare un dispositivo mobile e controllare la modalità di visualizzazione del modulo sui dispositivi mobili.

  ![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **Modalità anteprima**
Nella modalità di anteprima, il modulo viene visualizzato nell’editor esattamente come viene pubblicato. In questo modo l’autore può spostarsi all’interno del modulo facendo clic su collegamenti e pulsanti. Una volta apportate le modifiche desiderate, l’autore può pubblicare il modulo per gli utenti live. Il tasto di scelta rapida per passare dalla modalità di modifica alla modalità di anteprima è `p`.
  ![Anteprima](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **Apri pagina**
L’opzione **Apri pagina** apre il modulo in una nuova scheda per la visualizzazione in anteprima. Il tasto di scelta rapida per aprire il modulo in modalità di anteprima in una nuova scheda è `o`.
  ![Apri pagina](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **Pubblica**

  Puoi rendere il modulo disponibile agli utenti live utilizzando il pulsante **Pubblica**.
  ![Pubblica](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **Puntini di sospensione**
Quando l’autore fa clic sull’opzione (...), viene visualizzata l’opzione **Annulla pubblicazione**. Puoi annullare la pubblicazione di un modulo utilizzando l’opzione **Annulla pubblicazione**.
  ![Puntini di sospensione](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### Pannello Proprietà

Il **pannello Proprietà** si trova sul lato destro dell’editor. Mostra i dettagli del componente selezionato nella gerarchia del modulo. Si tratta della struttura predefinita quando non è selezionato alcun componente.
![pannello ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


Comprendiamo ciascuno dei suoi componenti.


* **Modalità proprietà**
L’opzione **Proprietà** mostra le proprietà del componente selezionato nell’editor. Ad esempio, l’immagine mostra le proprietà del componente di input del numero selezionato. Puoi modificare le proprietà del componente utilizzando questa opzione. Il tasto di scelta rapida per aprire le proprietà del componente è `d`.

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **Struttura contenuto**
L&#39;opzione **Struttura contenuto** visualizza la gerarchia del modulo. Quando l’autore fa clic su un elemento nella struttura del contenuto, l’editor lo seleziona e scorre fino a quel componente. Il tasto di scelta rapida per passare tra le visualizzazioni della struttura contenuto è `f`.

  ![Struttura contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **Generare varianti**
  La funzione **Genera varianti** utilizza l’intelligenza artificiale per produrre versioni diverse dei moduli in base a prompt specifici. I prompt possono essere forniti da Adobe oppure creati e gestiti dall’autore del modulo.

  ![variante](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > Per istruzioni sull’utilizzo della funzione Genera varianti per i moduli, consulta l’articolo [Generare varianti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

* **Sperimentazione**:

  La funzione **Sperimentazione** si riferisce a tecniche utilizzate per testare diverse varianti di moduli e layout al fine di ottimizzare l’esperienza utente e le prestazioni.
  ![sperimentazione](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalizzazione**
L’opzione **Personalizzazione** permette di configurare le impostazioni per stabilire una connessione tra i moduli e le applicazioni Adobe Experience Platform (AEP) che fanno parte dell’ecosistema Adobe o altre applicazioni esterne.
  ![Personalizzazione](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **Test A/B**:
  **Test A/B** si riferisce alle tecniche utilizzate per testare diverse varianti di moduli e layout per ottimizzare l’esperienza utente e le prestazioni.
  ![Test A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **Gestione attività**:
la funzione **Gestione attività** consente di semplificare i flussi di lavoro e migliorare la collaborazione consentendo ai team di gestire, tenere traccia ed eseguire attività correlate alla personalizzazione e all’ottimizzazione dei moduli.
  ![gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

.
* **Bozze di contenuto**

  L’opzione **Bozze di contenuto** consente di creare bozze di elementi formattati. Le bozze possono essere create utilizzando il testo del modulo esistente o da zero. È possibile modificare o eliminare le bozze in base alle esigenze. Per impostazione predefinita, sono visibili solo tre bozze, ma facendo clic su **Mostra tutto** viene visualizzato il resto.

  ![gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **Origine dati**

  L’opzione **Origine dati** consente di configurare le origini dati e di selezionarle durante la creazione di un modello di dati modulo (FDM, Form Data Model). Tutti gli oggetti del modello di dati, le proprietà e i servizi dalle origini dati selezionate diventano disponibili e utilizzabili nel modello di dati modulo.
  ![Origine dati](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **Aggiungi**

  L’opzione **Aggiungi** apre un elenco a discesa contenente i componenti che è possibile aggiungere al contenitore selezionato. Ad esempio, nella sezione Modulo adattivo, sono elencati i componenti che possono essere aggiunti a un modulo. Il tasto di scelta rapida per aprire l’elenco dei componenti è `a`.
  ![Icona Aggiungi](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **Duplica**

  L’opzione **Duplica** crea una copia del componente selezionato nella struttura del contenuto o nell’editor.
  ![Icona Duplica](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **Elimina**
L’opzione **Elimina** elimina un componente selezionato nella struttura del contenuto o nell’editor.

  ![Elimina](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### Editor

L’editor consente di modificare il modulo; il modulo specificato nella barra della posizione viene riprodotto nell’area di modifica. Se l’editor è in modalità di anteprima, puoi navigare nel modulo utilizzando i pulsanti e i collegamenti disponibili.
![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## Consulta anche

{{universal-editor-see-also}}
