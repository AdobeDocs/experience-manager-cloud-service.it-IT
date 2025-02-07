---
title: Modifiche alla sincronizzazione di gruppi di utenti e profili di prodotto
description: Informazioni sulle modifiche alla sincronizzazione del gruppo utenti e del profilo prodotto in arrivo in AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: ht
source-wordcount: '385'
ht-degree: 100%

---

# Modifiche alla sincronizzazione di gruppi di utenti e profili di prodotto {#changes-in-user-group-and-product-profile-synchronization}

Ogni volta che un utente accede ad AEM as a Cloud Service o viene utilizzato un token di accesso, i gruppi di utenti, i profili di prodotto e i servizi del profilo di prodotto di Adobe Admin Console vengono sincronizzati nell’archivio AEM come gruppi.

A partire dalla versione di manutenzione di AEM 19149, il comportamento di sincronizzazione del gruppo viene modificato per ridurre il disordine nell’interfaccia utente e ottimizzare le prestazioni. In particolare, l’iscrizione al gruppo di utenti delle due seguenti categorie di gruppi AEM non sarà più sincronizzata:

1. Gruppi AEM con suffisso `GROUP_NAME_SUFFIX`. Questi gruppi non vengono visualizzati in Adobe Developer Console, ma nella schermata Gestione dei gruppi AEM, come illustrato di seguito. Nel caso improbabile che l’applicazione AEM faccia riferimento a tali gruppi, assicurarsi di utilizzare invece i gruppi di utenti di Adobe Admin Console senza quel suffisso.

   ![Gruppi rimossi 1](/help/security/assets/removed-groups-1.png)

1. Gruppi AEM associati a profili di prodotto di Adobe Admin Console non correlati all’ambiente specifico. Ciò può includere profili di prodotto che sono:

   * relativi ad altri prodotti Adobe
   * relativi ad altri programmi AEM
   * relativi ad altri ambienti AEM nello stesso programma AEM
   * relativi a Cloud Manager (ad esempio `Business Owner - Cloud Service`)

   Nell’immagine seguente, ad esempio, sono presenti molte righe con il pattern `AEM Administrators-<suffix>` o `AEM Users-<suffix>` in cui il suffisso non è correlato all’ambiente corrente.

   ![Gruppi rimossi 2](/help/security/assets/removed-groups-2.png)

Per verificare quale suffisso è correlato all’ambiente corrente, selezionare Gestione **accesso - Profili di authoring** (o **Profili di pubblicazione**) nel menu Azioni dell’ambiente in Cloud Manager.

![Verificare i suffissi](/help/security/assets/suffix-check.png)

In questo modo si accede ad Adobe Admin Console, come illustrato nella schermata seguente. `<suffix>` potrebbe essere un set casuale di caratteri o piuttosto il livello e gli ID di programma e dell’ambiente (ad esempio, `author - Program 12345 - Environment 45678`).

![Suffissi in Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

Nel caso improbabile che l’applicazione AEM faccia riferimento a un gruppo che non apparirà più in AEM, assicurarsi invece di utilizzare i) un profilo di prodotto della giusta istanza AEM o ii) un gruppo di utenti Adobe Admin Console.

Le iscrizioni ai gruppi dell’utente vengono sincronizzate al momento dell’accesso all’ambiente e rimosse dai gruppi non correlati all’ambiente corrente. I gruppi stessi rimangono e includono gli utenti che non hanno effettuato l’accesso da quando la funzione è stata abilitata.
