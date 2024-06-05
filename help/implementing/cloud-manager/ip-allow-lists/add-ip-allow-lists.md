---
title: Aggiunta degli elenchi IP consentiti
description: Scopri come aggiungere un elenco IP consentiti personalizzato con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 75%

---


# Aggiunta di un elenco IP consentiti {#add-ip-allow-list}

Scopri come aggiungere un elenco IP consentiti personalizzato con Cloud Manager.

Per aggiungere un elenco IP consentiti, l’utente con ruolo di **Proprietario business** o **Responsabile della distribuzione** può seguire la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla sezione **Panoramica** , passare alla pagina **ELENCHI CONSENTITI IP** tramite la scheda di navigazione laterale.

   ![Opzione elenchi IP consentiti nel pannello laterale](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clic **Aggiungi Elenco consentiti IP**.

   ![Finestra di dialogo Aggiungi elenco IP consentiti](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. In **Aggiungi Elenco consentiti IP** immettere un nome che si desidera utilizzare per fare riferimento al inserisco nell&#39;elenco Consentiti di selezione nella finestra di dialogo **Nome Elenco consentiti IP** campo.

   * Questo nome è esclusivamente informativo e deve essere descrittivo, per aiutarti a identificare l’elenco.

1. Nel campo **Indirizzo IP/CIDR**, immetti un IP o un blocco IP CIDR.

   * È possibile separare più blocchi con una virgola o una tabulazione.

1. Fai clic su **Salva**.

Dopo averlo salvato, l’elenco IP consentiti appena creato viene visualizzato come riga nella tabella della pagina **Elenchi IP consentiti**.
