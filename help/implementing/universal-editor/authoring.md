---
title: Authoring dei contenuti con l’editor universale
description: Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 84%

---

# Authoring dei contenuti con l’editor universale {#authoring}

Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.

## Introduzione {#introduction}

Universal Editor consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione, in modo da poter fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A questo scopo, offre agli autori dei contenuti un’interfaccia utente intuitiva che richiede una formazione minima per poter entrare e iniziare a modificare i contenuti.

>[!TIP]
>
>Per un’introduzione più dettagliata all’editor universale, consulta il documento [Introduzione all’editor universale.](introduction.md)

>[!NOTE]
>
>L’editor universale è ancora in fase di sviluppo e al momento non può modificare tutti i tipi di contenuto.

## Preparare l’app {#prepare-app}

Per creare contenuti per un’app tramite l’editor universale, l’app deve essere dotata di strumenti che consentano a uno sviluppatore di supportare l’editor.

>[!TIP]
>
>Consulta il documento [Guida introduttiva all’editor universale in AEM](getting-started.md) per un esempio su come configurare un’app AEM per lavorare con l’editor universale.

## Accedi {#sign-in}

Una volta che l’app è stata preparata per funzionare con l’editor universale, dovrai accedere all’editor universale. Sarà necessario un Adobe ID per accedere e [avere accesso all’editor universale.](getting-started.md#request-access)

Dopo aver effettuato l’accesso, immetti l’URL della pagina da modificare in [barra degli indirizzi.](#address-bar) per iniziare [la modifica del contenuto.](#edit-content)

## Comprendere l’interfaccia utente {#ui}

L’interfaccia utente è divisa in quattro aree principali.

* [Intestazione di Experience Cloud](#experience-cloud-header)
* [Intestazione dell’editor universale](#universal-editor-header)
* [La barra laterale](#rail)
* [L’editor](#editor)

![Interfaccia utente dell’editor universale](assets/ui.png)

### Intestazione di Experience Cloud {#experience-cloud-header}

L’intestazione di Experience Cloud è sempre presente nella parte superiore dello schermo. È un ancoraggio che indica dove ti trovi all’interno di Experience Cloud e ti aiuta a passare ad altre app di Experience Cloud.

![Intestazione di Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Seleziona il collegamento Adobe Experience Cloud a sinistra dell’intestazione per passare alla directory principale della soluzione Experience Manager e accedere a strumenti come [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager,](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) e [Distribuzione di software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it)

![Pulsante di navigazione globale](assets/global-navigation.png)

#### Organizzazione {#organization}

Viene visualizzata l’organizzazione in cui hai effettuato l’accesso. Tocca o fai clic per passare a un’altra organizzazione se il tuo Adobe ID è associato a più di una.

![Indicatore dell’organizzazione](assets/organization.png)

#### Soluzioni {#solutions}

Tocca o fai clic sul selettore delle soluzioni per passare rapidamente ad altre soluzioni di Experience Cloud.

![Selettore di soluzioni](assets/solutions.png)

#### Aiuto {#help}

L’icona dell’aiuto fornisce un accesso rapido alle risorse di apprendimento e supporto.

![Aiuto](assets/help.png)

#### Notifiche {#notifications}

Questa icona è contrassegnata con il numero di incompleti attualmente assegnati [notifiche.](/help/implementing/cloud-manager/notifications.md)

![Notifiche](assets/notifications.png)

#### Proprietà utente {#user-properties}

Tocca o fai clic sull’icona che rappresenta l’utente per accedere alle impostazioni utente. Se non hai configurato un’immagine utente, viene assegnata un’icona in modo casuale.

![Proprietà utente](assets/user-properties.png)

### Intestazione dell’editor universale {#universal-editor-header}

L’intestazione dell’editor universale è sempre presente nella parte superiore dello schermo immediatamente sotto [l’intestazione di Experience Cloud.](#experience-cloud-header) Consente un accesso rapido per passare a un’altra pagina di modifica e di pubblicazione della pagina corrente.

![Intestazione dell’editor universale](assets/universal-editor-header.png)

#### Il menu hamburger {#hamburger-menu}

Il menu hamburger non è ancora implementato.

![Menu hambuger](assets/hamburger-menu.png)

#### Barra della posizione {#Location-bar}

La barra della posizione mostra l’indirizzo della pagina che stai modificando. Tocca o fai clic per inserire l’indirizzo di un’altra pagina da modificare.

![Barra della posizione](assets/address-bar.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `L` per aprire la barra degli indirizzi.

>[!NOTE]
>
>Qualsiasi pagina da modificare con l’editor universale deve essere [abilitata per supportare l’editor universale.](getting-started.md)

#### Apri anteprima app {#open-app-preview}

Tocca o fai clic sull’icona di anteprima dell’app aperta per aprire la pagina che stai modificando nel browser, senza ricorrere all’editor per visualizzare in anteprima le modifiche.

![Apri anteprima app](assets/open-app-preview.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `O` per aprire l’anteprima dell’app.

#### Pubblicazione {#publish}

Tocca o fai clic sul pulsante Pubblica per pubblicare le modifiche al contenuto live per consentirne l’utilizzo da parte dei lettori.

![Pulsante pubblica](assets/publish.png)

>[!TIP]
>
>Consulta il documento [Pubblicazione di contenuti con l’editor visivo universale](publishing.md) per ulteriori informazioni sulla pubblicazione con l’editore universale.

### La barra laterale {#rail}

La barra laterale sinistra dell’editor è sempre presente. Consente di passare facilmente dalla modalità anteprima a quella di modifica e viceversa.

![La barra](assets/rail.png)

#### Modalità Anteprima {#preview-mode}

In modalità anteprima, la pagina viene riprodotta nell’editor come verrebbe visualizzata sul servizio pubblicato. Questo consente all’autore del contenuto di navigare nel contenuto facendo clic sui collegamenti, ecc.

![Modalità anteprima](assets/preview-mode.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `P` per passare alla modalità anteprima.

#### Modalità modifica {#edit-mode}

In modalità modifica, la pagina viene visualizzata nell’editor, ma l’autore del contenuto può fare clic per selezionare il contenuto da modificare. Questa è la modalità predefinita dell’editor quando viene caricata una pagina.

![Modalità modifica](assets/edit-mode.png)

### L’editor {#editor}

L’editor occupa la maggior parte della finestra ed è l’area in cui viene eseguito il rendering della pagina specificata nella [barra degli indirizzi](#address-bar).

A seconda che l’editor sia in [modalità di modifica](#edit-mode) o [modalità anteprima,](#edit-mode)il contenuto sarà rispettivamente modificabile o navigabile.

![Editor](assets/editor.png)

## Modifica del contenuto {#editing-content}

La modifica del contenuto è semplice e intuitiva. In entrata [modalità di modifica,](#edit-mode) quando passi il mouse sul contenuto nell’editor, il contenuto modificabile viene evidenziato con una casella blu.

![Il contenuto modificabile viene evidenziato da una casella blu](assets/editable-content.png)

Tocca o fai clic sul contenuto nella casella blu per avviare un editor diretto per apportare le modifiche. Premi invio o indietro per salvare le modifiche.

![Modifica del contenuto](assets/editing-content.png)

In modalità modifica, toccando o facendo clic sul contenuto lo si seleziona per la modifica. Per navigare nel contenuto tramite i seguenti collegamenti, passa a [modalità anteprima.](#preview-mode)

## Anteprima del contenuto {#previewing-content}

Quando hai finito di modificare il contenuto, spesso desideri navigare in esso per vedere come si presenta nel contenuto di altre pagine. In [modalità anteprima](#preview-mode) puoi fare clic sui collegamenti per navigare nel contenuto come farebbe un lettore. Il contenuto viene riprodotto nell’editor così come verrebbe pubblicato.

In modalità anteprima, toccando o facendo clic sul contenuto questo appare così come si presenterebbe a un lettore. Se desideri selezionare il contenuto per modificarlo, passa a [modalità modifica.](#edit-mode)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come Universal Editor consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione, per offrire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Pubblicazione di contenuto con l’editor universale](publishing.md): scopri in che modo l’editor visivo universale pubblica il contenuto e come le app possono gestire il contenuto pubblicato.
* [Guida introduttiva all’editor universale in AEM](getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.
