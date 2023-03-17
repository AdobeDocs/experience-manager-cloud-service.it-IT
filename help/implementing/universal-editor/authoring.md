---
title: Creazione di contenuti con l’editor universale
description: Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 2%

---


# Creazione di contenuti con l’editor universale {#authoring}

Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.

## Introduzione {#introduction}

L’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.

A questo scopo, offre agli autori dei contenuti un’interfaccia utente intuitiva che richiede una formazione minima per poter iniziare a modificare i contenuti.

>[!TIP]
>
>Per un’introduzione più dettagliata all’editor universale, consulta il documento [Introduzione all’editor universale.](introduction.md)

>[!NOTE]
>
>L’editor universale è ancora in fase di sviluppo e al momento può creare solo testo.

## Preparare l’app {#prepare-app}

Per creare contenuti per un’app utilizzando l’editor universale, l’app deve essere strumentalizzata da uno sviluppatore per supportare l’editor.

>[!TIP]
>
>Vedi il documento [Guida introduttiva all’Editor universale in AEM](getting-started.md) per un esempio su come configurare un’app AEM per l’utilizzo con l’editor universale.

## Accedi {#sign-in}

Una volta che l’app è stata attrezzata per funzionare con l’Editor universale, dovrai accedere all’Editor universale. Sarà necessario un Adobe ID per accedere e [hanno accesso all’editor universale.](getting-started.md#request-access)

Dopo aver effettuato l’accesso, immetti l’URL della pagina da modificare nel [barra degli indirizzi.](#address-bar) per iniziare [modifica del contenuto.](#edit-content)

## Comprendere l’interfaccia utente {#ui}

L’interfaccia utente è divisa in quattro aree principali.

* [Intestazione dell’Experience Cloud](#experience-cloud-header)
* [Intestazione dell’editor universale](#universal-editor-header)
* [La barra](#rail)
* [L&#39;editor](#editor)

![Interfaccia utente dell’editor universale](assets/ui.png)

### Intestazione Experience Cloud {#experience-cloud-header}

L’intestazione dell’Experience Cloud è sempre presente nella parte superiore dello schermo. È un ancoraggio che indica dove ti trovi all’interno di Experience Cloud e ti aiuta a passare ad altre app di Experience Cloud.

![Intestazione dell’Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Seleziona il collegamento Adobe Experience Cloud a sinistra dell’intestazione per accedere alla directory principale della soluzione Experience Manager e accedere a strumenti come [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager,](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) e [Distribuzione di software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

![Pulsante Navigazione globale](assets/global-navigation.png)

#### Organizzazione {#organization}

Viene visualizzata l’organizzazione a cui hai effettuato l’accesso. Tocca o fai clic per passare a un’altra organizzazione se il tuo Adobe ID è associato a più gruppi.

![Indicatore dell&#39;organizzazione](assets/organization.png)

#### Soluzioni {#solutions}

Tocca o fai clic sul commutatore delle soluzioni per passare rapidamente ad altre soluzioni di Experience Cloud.

![Switcher di soluzioni](assets/solutions.png)

#### Aiuto {#help}

L’icona Aiuto fornisce un accesso rapido alle risorse di apprendimento e supporto.

![Aiuto](assets/help.png)

#### Notifiche {#notifications}

Questa icona viene contrassegnata con il numero di elementi incompleti attualmente assegnati [notifiche.](/help/implementing/cloud-manager/notifications.md)

![Notifiche](assets/notifications.png)

#### Proprietà utente {#user-properties}

Tocca o fai clic sull’icona che rappresenta l’utente per accedere alle impostazioni utente. Se non hai configurato un&#39;immagine utente, verrà assegnata un&#39;icona in modo casuale.

![Proprietà utente](assets/user-properties.png)

### Intestazione dell’editor universale {#universal-editor-header}

L’intestazione dell’Editor universale è sempre presente nella parte superiore dello schermo immediatamente sotto [l’intestazione dell’Experience Cloud.](#experience-cloud-header) Consente di passare rapidamente a un’altra pagina da modificare e di pubblicare la pagina corrente.

![Intestazione dell’editor universale](assets/universal-editor-header.png)

#### Menu Hamburger {#hamburger-menu}

Il menu hamburger non è ancora implementato.

![Menu Hambuger](assets/hamburger-menu.png)

#### Barra degli indirizzi {#address-bar}

La barra degli indirizzi mostra il percorso della pagina che si sta modificando. Tocca o fai clic per inserire l’indirizzo di un’altra pagina da modificare.

![Barra degli indirizzi](assets/address-bar.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `L` per aprire la barra degli indirizzi.

>[!NOTE]
>
>Qualsiasi pagina da modificare con l’Editor universale deve essere [è stato progettato per supportare l’editor universale.](getting-started.md)

#### Indicatore di collaborazione {#collaboration}

Se nell’editor universale sono presenti altri autori con la stessa pagina caricata, verranno mostrate le immagini di tali autori. Passa il puntatore del mouse su un&#39;immagine per visualizzare il nome utente completo

![Indicatore di collaborazione](assets/collaboration.png)

#### Apri anteprima app {#open-app-preview}

Tocca o fai clic sull’icona di anteprima dell’app aperta per aprire la pagina che stai modificando nel proprio browser, senza utilizzare l’editor per visualizzare in anteprima le modifiche.

![Apri anteprima app](assets/open-app-preview.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `O` per aprire l’anteprima dell’app.

#### Pubblicazione {#publish}

Tocca o fai clic sul pulsante di pubblicazione per pubblicare le modifiche al contenuto in tempo reale da utilizzare per i lettori.

![Pulsante Pubblica](assets/publish.png)

### La barra {#rail}

La barra laterale sinistra dell’editor è sempre presente. Consente di passare facilmente dall&#39;anteprima alla modalità di modifica e viceversa.

![La barra](assets/rail.png)

#### Modalità Anteprima {#preview-mode}

In modalità anteprima, la pagina viene riprodotta nell’editor come verrebbe visualizzata sul servizio pubblicato. Questo consente all’autore del contenuto di navigare nel contenuto facendo clic sui collegamenti, ecc.

![Modalità Anteprima](assets/preview-mode.png)

>[!TIP]
>
>Usa il tasto di scelta rapida `P` per passare alla modalità anteprima.

#### Modalità Modifica {#edit-mode}

In modalità di modifica, la pagina viene sottoposta a rendering nell’editor, ma l’autore del contenuto può fare clic per selezionare il contenuto da modificare. Questa è la modalità predefinita dell’editor quando viene caricata una pagina.

Modalità ![Modifica](assets/edit-mode.png)

### Editor {#editor}

L’editor occupa la maggior parte della finestra ed è il punto in cui si trova la pagina specificata in [la barra degli indirizzi](#address-bar) viene eseguito il rendering.

A seconda se l’editor è in [modalità di modifica](#edit-mode) o [modalità anteprima,](#edit-mode) il contenuto sarà rispettivamente modificabile o navigabile.

![Editor](assets/editor.png)

## Modifica del contenuto {#editing-content}

L&#39;editing dei contenuti è semplice e intuitivo. In [modalità di modifica,](#edit-mode) quando passi il mouse sul contenuto nell’editor, il contenuto modificabile viene evidenziato con una casella blu.

![Il contenuto modificabile viene evidenziato da una casella blu](assets/editable-content.png)

Tocca o fai clic sul contenuto della casella blu per avviare un editor in-place per apportare le modifiche. Premere enter o return per salvare le modifiche.

![Modifica del contenuto](assets/editing-content.png)

In modalità di modifica, toccando o facendo clic sul contenuto si tenta di selezionarlo per la modifica. Per navigare nel contenuto tramite i seguenti collegamenti, passa a [modalità anteprima.](#preview-mode)

## Anteprima del contenuto {#previewing-content}

Quando hai finito di modificare il contenuto, spesso desideri navigarlo per vedere come si presenta nel contenuto di altre pagine. In [modalità anteprima](#preview-mode) potete fare clic sui collegamenti per navigare nel contenuto come farebbe un lettore. Il contenuto viene riprodotto nell’editor così come verrebbe pubblicato.

In modalità anteprima, il tocco o il clic sul contenuto reagisce come se si trattasse di un lettore del contenuto. Se desideri selezionare il contenuto per la modifica, passa a [modalità di modifica.](#edit-mode)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’Editor universale in AEM](getting-started.md) - Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md) - Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md) - Scopri gli attributi e i tipi di dati richiesti dall’Editor universale.
* [Autenticazione dell’editor universale](authentication.md) - Scopri come l’editor universale si autentica.
