---
title: Modifiche alla sincronizzazione del gruppo utenti e del profilo prodotto
description: Informazioni sulle modifiche alla sincronizzazione del gruppo utenti e del profilo prodotto in arrivo in AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: cddfcddc0ca3652270bdb735e580386ac9ff1fc7
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 65%

---

# Modifiche alla sincronizzazione del gruppo utenti e del profilo prodotto {#changes-in-user-group-and-product-profile-synchronization}

Ogni volta che un utente accede ad AEM as a Cloud Service o viene utilizzato un token di accesso, i gruppi di utenti, i profili di prodotto e i servizi del profilo di prodotto di Adobe Admin Console vengono sincronizzati nell’archivio AEM come gruppi.

Con le versioni AEM superiori a 18751 (una versione di manutenzione inizierà a essere implementata negli ambienti di produzione il 27 gennaio), al fine di ridurre il disordine nell’interfaccia utente e ottimizzare le prestazioni, ci saranno alcune modifiche al comportamento di sincronizzazione, con conseguente minor numero di gruppi visualizzati nell’AEM. Verranno rimosse due categorie di gruppi AEM:

1. Gruppi AEM con suffisso `GROUP_NAME_SUFFIX`. Questi gruppi non vengono visualizzati in Adobe Developer Console, ma nella schermata Gestione dei gruppi AEM, come illustrato di seguito. Nel caso improbabile che l’applicazione AEM faccia riferimento a tali gruppi, assicurati invece di fare riferimento ai gruppi di utenti Adobe Admin Console senza tale suffisso.

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

Nel caso improbabile che l’applicazione AEM faccia riferimento a un gruppo che non apparirà più nell’AEM, assicurati invece di utilizzare i) un profilo di prodotto della giusta istanza AEM o ii) un gruppo di utenti Adobe Admin Console.

