---
title: AEM as a Cloud Service su Unified Shell
description: AEM as a Cloud Service su Unified Shell
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: aeb8244b4da17a0675b86a69727807abf45ca84a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 68%

---

# AEM as a Cloud Service su Unified Shell {#aem-as-a-cloud-service-on-unified-shell}

## Panoramica {#overview}

AEM as a Cloud Service (Author Service) è integrato con Unified Shell per migliorare l’esperienza utente e unificarla a tutte le altre applicazioni di Experience Cloud. L’impatto di questa integrazione può essere visto nell’intestazione superiore dell’applicazione, come illustrato di seguito.

![immagine](/help/overview/assets/unifiedshell_header.png)

Offre i seguenti vantaggi:

* Single sign-on in tutte le applicazioni Experience Cloud
* Semplicità di passaggio a un’altra organizzazione o applicazione
* Documentazione del prodotto migliorata
* Pulsante di feedback semplificato all’interno del prodotto per segnalare i problemi o condividere idee con Adobe
* Accesso agli annunci e alle notifiche globali dei prodotti oltre a notifiche specifiche per AEM as a Cloud Service

## Disattivazione di Unified Shell {#disabling-unified-shell}

La funzionalità Unified Shell è attivata in AEM as a Cloud Service per impostazione predefinita. Tuttavia, nel caso in cui l’intestazione superiore sia stata personalizzata, si consiglia di disabilitare Unified Shell per evitare problemi nelle personalizzazioni. Per disattivare Unified Shell, effettua le seguiti operazioni:

>[!NOTE]
>La shell unificata può essere disabilitata solo da un account con privilegi amministrativi.

1. Passa a **Strumenti > Cloud Services**.

   All’utente amministratore verrà presentata la scheda di configurazione Unified Shell, come illustrato di seguito:

   ![immagine](/help/overview/assets/unifiedshell2.png)

1. Fai clic su **Configurazione Unified Shell**. Quindi, deseleziona la casella di controllo illustrata di seguito per disabilitare Unified Shell:

   ![immagine](/help/overview/assets/unifiedshell3.png)

## Passare al tema scuro {#changing-to-dark-theme}

Per passare al tema scuro, fai clic sull’icona del tuo profilo. Viene visualizzata una finestra a comparsa. Puoi utilizzare l’interruttore per passare al tema scuro di Unified Shell.

>[!INFO]
>
>Il tema scuro viene applicato solo all’area Unified Shell (la barra superiore).

![immagine](/help/overview/assets/unifiedshell4.png)

## Identificazione dell’ambiente as a Cloud Service AEM {#identify-aemaacs-environment}

AEM as a Cloud Service fornisce tre tipi di ambienti: Produzione, stage e sviluppo. Fai riferimento a [Tipi di ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en) per ulteriori dettagli. Con questa integrazione con Unified Shell, il tipo di ambiente a cui l’utente ha effettuato l’accesso al servizio Author viene visualizzato nell’intestazione superiore tramite un’etichetta come mostrato di seguito.

![immagine](/help/overview/assets/unifiedshell_header_label.png)

## Accesso alla casella in entrata AEM {#accessing-the-aem-inbox}

È possibile accedere alla Casella in entrata AEM facendo clic sull’icona del campanello in Unified Shell.

>[!INFO]
>
> Il numero indicato sull’icona del campanello include le notifiche non lette in tutte le soluzioni per l’organizzazione IMS e le attività elencate nella casella in entrata AEM.

![immagine](/help/overview/assets/unifiedshell5.png)

Fai clic sul pulsante Casella in entrata nel pannello a comparsa per passare alla casella in entrata AEM:

![immagine](/help/overview/assets/unifiedshell6.png)
