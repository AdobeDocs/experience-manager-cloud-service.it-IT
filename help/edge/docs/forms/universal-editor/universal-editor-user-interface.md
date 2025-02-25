---
title: Informazioni su Universal Editor - Esercitazione per sviluppatori
description: Questa esercitazione ti aiuta a iniziare a usare l’interfaccia di Universal Editor. Consente di comprendere l'interfaccia utente per la creazione di Edge Delivery Services Form personalizzati in Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 0d28009332feccb4552e2cc42d7b1a8da43d579c
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Esplorazione dell&#39;interfaccia di Universal Editor (WYSIWYG)

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) offre un&#39;interfaccia What You See Is What You Get (WYSIWYG) semplice, visiva e intuitiva per Adobe Edge Delivery Services (EDS) Forms. Offre un’interfaccia moderna con funzionalità di trascinamento della selezione per un’authoring efficiente dei moduli.

![Interfaccia utente editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Interfaccia Universal Editor

Quando l’autore del modulo modifica il modulo utilizzando l’Editor universale, la console apre un’interfaccia WYSIWYG interattiva che consente all’utente di iniziare a modificare il modulo.

>[!NOTE]
>
> Per informazioni su come creare moduli utilizzando l&#39;editor universale, vedere l&#39;articolo [Guida introduttiva di Edge Delivery Services per AEM Forms utilizzando l&#39;editor universale (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interfaccia utente editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

L&#39;interfaccia di Universal Editor è divisa in quattro parti:

* **[A: Intestazione Experience Cloud](#experience-cloud-header)**
* **[B: Barra degli strumenti dell&#39;editor universale](#universal-editor-toolbar)**
* **[C: Pannello Proprietà](#properties-panel)**
* **[D: Editor](#editor)**

### Intestazione Experience Cloud

L’intestazione Experience Cloud si trova nella parte superiore della console. Fornisce informazioni sulla posizione corrente all’interno di Experience Cloud. Consente inoltre di passare ad altre applicazioni Experience Cloud.

![Intestazione Experience Cloud Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


Comprendiamo ciascuno dei suoi componenti.

* **Adobe Experience Cloud**

  Puoi fare clic sul collegamento **Adobe Experience Cloud** sul lato sinistro della schermata per passare alla directory principale della soluzione Experience Manager e accedere a strumenti come Experience Manager Sites, Experience Manager Assets e Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **Nome organizzazione**

  Il **nome organizzazione** visualizza il nome dell&#39;organizzazione IMS a cui si è attualmente connessi. Se ha accesso ad altre organizzazioni, puoi passare a un’altra organizzazione IMS selezionando dall’elenco a discesa. Ad esempio, il nome dell’organizzazione IMS attualmente selezionata è `AEM Forms Internal01`.

  ![Organizzazione](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **Aiuto**

  L’icona Aiuto consente di accedere rapidamente alle risorse di apprendimento e supporto. L&#39;autore del modulo può anche aggiungere il feedback nella sezione **Guida**.
  ![Guida](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **Notifiche**

  Nella sezione **Notifica** sono visualizzate le notifiche incomplete attualmente assegnate, le richieste e le attività correnti nell&#39;organizzazione IMS.

  ![Notifica](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **Soluzioni**

  Puoi passare ad altre soluzioni Experience Cloud utilizzando il collegamento **Soluzioni**.
  ![Soluzioni](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **Autore**
L’icona rappresenta i dettagli dell’autore del modulo e il nome dell’organizzazione IMS a cui l’autore ha attualmente effettuato l’accesso.
  ![Autore](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### Barra degli strumenti Editor universale

La barra degli strumenti consente di passare ad altri moduli e di modificarli. Consente inoltre di pubblicare o annullare la pubblicazione del modulo, di modificarne le proprietà e di accedere all’editor di regole.
![Barra degli strumenti Editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Comprendiamo ciascuno dei suoi componenti.

* **Pulsante Home**
Il pulsante Home consente di passare alla pagina iniziale di Universal Editor. È inoltre possibile immettere direttamente l&#39;URL del modulo che si desidera modificare utilizzando l&#39;editor universale.
  ![Pagina principale editor universale](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **Barra località**
La **barra località** visualizza l&#39;indirizzo del modulo che l&#39;autore sta modificando. Puoi anche immettere un altro URL modulo facendo clic sulla barra della posizione. Il tasto di scelta rapida per aprire la barra del percorso è il tasto `l`.
  ![Barra località](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **Editor regole**

  **Editor regole** offre un&#39;interfaccia visiva intuitiva per la creazione e la gestione delle regole. È possibile aggiungere il comportamento di un modulo dinamico utilizzando l’Editor di regole.

  ![Editor regole](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * In Universal Editor, l’estensione Rule Editor non è attivata per impostazione predefinita. Per abilitare l&#39;estensione Editor regole, scrivi a noi all&#39;indirizzo [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) dal tuo ID e-mail ufficiale.
  > * Per informazioni su come creare regole, fare riferimento all&#39;articolo [Introduzione all&#39;editor di regole in WYSIWYG Authoring](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

* **Modifica proprietà modulo**
È possibile modificare le proprietà del modulo, ad esempio il modello dati del modulo e la data di pubblicazione, facendo clic sull&#39;opzione **Modifica proprietà modulo**.
  ![Modifica proprietà modulo](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **Impostazioni intestazione autenticazione**
Le **impostazioni di intestazione autenticazione** consentono all&#39;autore di impostare un&#39;intestazione di autenticazione personalizzata per lo sviluppo locale.
  ![intestazione autenticazione](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **Modalità reattiva**
  L&#39;opzione **Modalità reattiva** consente di definire la modalità di rendering del modulo in Universal Editor. Per impostazione predefinita, l’editor si apre in un layout desktop, in cui l’altezza e la larghezza vengono determinate automaticamente dal browser. In alternativa, è possibile scegliere di emulare un dispositivo mobile e controllare la modalità di visualizzazione del modulo sui dispositivi mobili.

  ![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **Modalità anteprima**
In modalità anteprima, il modulo viene visualizzato nell’editor esattamente come viene pubblicato. In questo modo l&#39;autore può navigare nel modulo facendo clic su collegamenti e pulsanti. Una volta apportate le modifiche desiderate, l’autore può pubblicare il modulo per gli utenti live. Il tasto di scelta rapida per passare dalla modalità di modifica alla modalità di anteprima è `p`.
  ![Anteprima](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **Apri pagina**
L&#39;opzione **Apri pagina** apre il modulo in una nuova scheda per l&#39;anteprima. Il tasto di scelta rapida per aprire il modulo in modalità anteprima in una nuova scheda è `o`.
  ![Apri pagina](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **Pubblica**

  Puoi rendere il modulo disponibile agli utenti live utilizzando il pulsante **Pubblica**.
  ![Pubblica](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **Puntini di sospensione**
Quando l&#39;autore fa clic sull&#39;opzione (...), viene visualizzata l&#39;opzione **Annulla pubblicazione**. È possibile annullare la pubblicazione di un modulo utilizzando l&#39;opzione **Annulla pubblicazione**.
  ![Ellissi](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### Pannello Proprietà

Il pannello **Proprietà** si trova sul lato destro dell&#39;editor. Vengono visualizzati i dettagli del componente selezionato nella gerarchia del modulo. Si tratta della struttura di default quando non è selezionato alcun componente.
![pannello ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


Comprendiamo ciascuno dei suoi componenti.


* **Modalità proprietà**
In **Proprietà** l&#39;opzione mostra le proprietà del componente selezionato nell&#39;editor. Ad esempio, l&#39;immagine visualizza le proprietà del componente di input del numero selezionato. Puoi modificare le proprietà del componente utilizzando questa opzione. Il tasto di scelta rapida per aprire le proprietà del componente è `d`.

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **Struttura contenuto**
L&#39;opzione **Struttura contenuto** visualizza la gerarchia del modulo. Quando l’autore fa clic su un elemento nella struttura del contenuto, l’editor lo seleziona e scorre fino a quel componente. Il tasto di scelta rapida per passare dalla visualizzazione struttura contenuto alla visualizzazione struttura è il tasto `f`.

  ![Struttura contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **Generare varianti**
  **Genera varianti** utilizza l&#39;intelligenza artificiale per produrre versioni diverse dei moduli in base a prompt specifici. Questi prompt possono essere forniti da Adobe oppure creati e gestiti dall’autore del modulo.

  ![variante](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > Per istruzioni sull&#39;utilizzo di Genera varianti per i moduli, consulta l&#39;articolo [Genera varianti](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

* **Sperimentazione**:

  **Sperimentazione** si riferisce alle tecniche utilizzate per testare diverse varianti di moduli e layout per ottimizzare l&#39;esperienza utente e le prestazioni.
  ![sperimentazione](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalization**
L&#39;opzione **Personalization** configura le impostazioni per stabilire una connessione tra i moduli e Adobe Experience Platform (AEP) che fanno parte dell&#39;ecosistema Adobe o delle applicazioni esterne.
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **Test A/B**:
  **Test A/B** si riferisce alle tecniche utilizzate per testare diverse varianti di moduli e layout per ottimizzare l&#39;esperienza utente e le prestazioni.
  ![Test A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **Gestione attività**:
La funzionalità **Gestione attività** consente di semplificare i flussi di lavoro e migliorare la collaborazione consentendo ai team di gestire, tenere traccia ed eseguire attività correlate alla personalizzazione e all&#39;ottimizzazione dei moduli
  ![gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

.
* **Bozze di contenuto**

  L&#39;opzione **Bozze di contenuto** consente di creare bozze per gli elementi Rich Text. Le bozze possono essere create utilizzando il testo del modulo esistente o da zero. È possibile modificare o eliminare le bozze in base alle esigenze. Per impostazione predefinita, sono visibili solo tre bozze, ma facendo clic su **Mostra tutto** viene visualizzato il resto.

  ![gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **Source dati**

  L&#39;opzione **Data Source** consente di configurare le origini dati e di selezionarle durante la creazione di un modello dati modulo (FDM). Rende disponibili per l’utilizzo nel modello dati modulo tutti gli oggetti modello dati, le proprietà e i servizi delle origini dati selezionate.
  ![Source dati](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **Aggiungi**

  L&#39;opzione **Aggiungi** apre un elenco a discesa di componenti che è possibile aggiungere al contenitore selezionato. Ad esempio, in una sezione Modulo adattivo, l’elenco mostra i componenti disponibili che possono essere aggiunti a un modulo. Il tasto di scelta rapida per aprire l&#39;elenco dei componenti è `a`.
  ![Icona Aggiungi](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **Duplicato**

  L&#39;opzione **Duplica** crea una copia del componente, che è selezionato nella struttura del contenuto o nell&#39;editor.
  ![Icona duplicata](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **Elimina**
L&#39;opzione **Elimina** elimina un componente selezionato nella struttura del contenuto o nell&#39;editor.

  ![Elimina](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### Editor

L’editor consente di modificare il modulo e il modulo specificato nella barra della posizione viene renderizzato nell’area di modifica. Se l’editor è in modalità anteprima, puoi navigare nel modulo utilizzando i pulsanti e i collegamenti disponibili.
![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## Consulta anche

{{universal-editor-see-also}}
