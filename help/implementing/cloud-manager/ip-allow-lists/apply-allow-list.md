---
title: Elenchi consentiti di Applica e Unpply IP
description: Scopri come applicare e annullare l'applicazione degli elenchi di indirizzi IP consentiti agli ambienti Cloud Manager.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 328ae6d1866a7089fb291d4872d27dc5fa1d4caa
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 12%

---


# Applica e annulla l&#39;applicazione degli elenchi indirizzi IP consentiti {#apply-allow-list}

Quando si applicano elenchi indirizzi IP consentiti, tutti gli intervalli IP inclusi nella definizione dell&#39;elenco sono associati a un autore o a un servizio pubblicare all&#39;interno di un ambiente. La rimozione di un elenco costituisce il processo inverso.

{{add-cm-allowlist-frontend-pipeline}}

## Applica Elenchi indirizzi IP consentiti {#applying}

Un utente nel ruolo Proprietario **Aziende o** Responsabile distribuzione **** può seguire questi passaggi per applicare un elenco indirizzi IP consentiti.

**Per applicare gli elenchi consentiti IP:**

1. Accedi a Cloud Manager in [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Selezionare l&#39;organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Dalla pagina **Panoramica**, passa alla schermata **Ambienti**.
1. **Nella schermata Ambienti**, vai alla pagina dei dettagli dell&#39;ambiente specifico.
1. Passare alla **tabella Elenco** indirizzi IP consentiti.
1. Utilizzare i campi di input nella parte superiore della tabella in modo da poter selezionare l&#39;elenco indirizzi IP consentiti e il servizio Autore, Publish o Anteprima a cui applicarlo.
Per applicarlo, l&#39;elenco indirizzi IP consentiti deve già esistere in Cloud Manager. Consulta [Aggiungere elenchi di indirizzi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).
1. Fai clic sull&#39;icona ![**](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) Aggiungi Applica** e conferma l&#39;invio.

## Non applicare elenchi di indirizzi IP consentiti {#un-applying}

Un utente nel ruolo Proprietario **Aziende o** Responsabile distribuzione **può seguire questi passaggi per annullare l&#39;applicazione** di un elenco indirizzi IP consentiti.

**Per annullare l&#39;applicazione degli elenchi indirizzi IP consentiti:**

1. Accedi a Cloud Manager in [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Selezionare l&#39;organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. **Dalla pagina Panoramica**, passa alla **pagina Ambienti**.
1. Passa alla pagina dei dettagli dell&#39;ambiente specifico.
1. Dall&#39;scheda Generale scorrere fino alla **tabella Elenco** indirizzi IP consentiti.
1. Identificare la riga dell&#39;elenco indirizzi IP consentiti a cui si desidera annullare l&#39;applicazione.
1. Sul lato destro della riga identificata, fare clic su ![Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Fate clic su **Annulla applicazione**.
1. Nella finestra di dialogo Non applicare l&#39;elenco **** indirizzi IP consentiti, fare clic su **Annulla applicazione**.
