---
title: Aggiunta degli elenchi IP consentiti
description: Scopri come aggiungere un elenco IP consentiti personalizzato con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---


# Aggiunta di un elenco IP consentiti {#add-ip-allow-list}

Scopri come aggiungere un elenco IP consentiti personalizzato con Cloud Manager.

Per aggiungere un elenco IP consentiti, l’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può seguire la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla schermata **Ambienti**, accedi alla pagina **Elenchi IP consentiti**.

   ![Opzione elenchi IP consentiti nel pannello laterale](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Per aprire la finestra di dialogo **Aggiungi elenco IP consentiti**, fai clic su **Aggiungi elenco IP consentiti**.

   ![Finestra di dialogo Aggiungi elenco IP consentiti](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Inserisci il nome che desideri utilizzare per fare riferimento all’elenco Consentiti nel campo **Nome elenco IP consentiti**.

   * Questo campo è esclusivamente informativo e deve essere descrittivo per aiutarti a identificare l’elenco.

1. Nel campo **Indirizzo IP/CIDR**, immetti un IP o un blocco IP CIDR.

   * È possibile separare più blocchi con una virgola o una tabulazione.

1. Per confermare quanto inserito, fai clic su **Salva**.

Al momento del salvataggio, l’elenco IP consentiti appena creato viene visualizzato come riga nella tabella della pagina **Elenchi IP consentiti**.
