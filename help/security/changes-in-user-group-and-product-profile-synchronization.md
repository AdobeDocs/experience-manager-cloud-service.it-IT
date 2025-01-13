---
title: Modifiche nella sincronizzazione di gruppi di utenti e profili di prodotto
description: Scopri le modifiche apportate alla sincronizzazione dei gruppi di utenti e dei profili di prodotto in AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 605a8032430b1be4aacebfcf73cfc16ba7691349
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Modifiche nella sincronizzazione di gruppi di utenti e profili di prodotto {#changes-in-user-group-and-product-profile-synchronization}

Ogni volta che un utente accede ad AEM as a Cloud Service o viene utilizzato un token di accesso, i gruppi di utenti Adobe Admin Console, i profili di prodotto e i servizi dei profili di prodotto vengono sincronizzati nell’archivio AEM come gruppi.

Il 27 gennaio, per ridurre il disordine nell’interfaccia utente e ottimizzare le prestazioni, saranno introdotte alcune modifiche nel comportamento di sincronizzazione, con la conseguente comparsa di un numero minore di gruppi nell’AEM. Verranno rimosse due categorie di gruppi AEM:

1. Gruppi AEM con suffisso `GROUP_NAME_SUFFIX`. Questi gruppi non vengono visualizzati in Adobe Developer Console, ma vengono visualizzati nella schermata Gestione gruppi AEM, come illustrato di seguito. Nel caso improbabile che l’applicazione AEM faccia riferimento a tali gruppi, assicurati invece di fare riferimento ai gruppi di utenti Adobe Admin Console senza tale suffisso.

   ![Gruppi rimossi 1](/help/security/assets/removed-groups-1.png)

1. Gruppi AEM associati a profili di prodotto di Adobe Admin Console non correlati all’ambiente specifico. Ciò può includere profili di prodotto che sono:

   * relativi ad altri prodotti di Adobe
   * relative ad altri programmi dell&#39;AEM
   * correlati ad altri ambienti AEM nello stesso programma AEM
   * relativo a Cloud Manager (ad esempio, `Business Owner - Cloud Service`)

   Nell&#39;immagine seguente, ad esempio, sono presenti molte righe con il pattern `AEM Administrators-<suffix>` o `AEM Users-<suffix>` in cui il suffisso non è correlato all&#39;ambiente corrente.

   ![Gruppi rimossi 2](/help/security/assets/removed-groups-2.png)

Per verificare quale suffisso è correlato all&#39;ambiente corrente, selezionare Gestisci **accesso - Profili autore** (o **Profili Publish**) nel menu Azioni dell&#39;ambiente in Cloud Manager.

![Controlla suffissi](/help/security/assets/suffix-check.png)

Verrà visualizzato il Adobe Admin Console, come illustrato nella schermata seguente. Tieni presente che `<suffix>` può essere un set casuale di caratteri o piuttosto il livello e gli ID di programma e ambiente (ad esempio, `author - Program 12345 - Environment 45678`).

![Suffissi nell&#39;Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

Nel caso improbabile che l’applicazione AEM faccia riferimento a un gruppo che non apparirà più nell’AEM, assicurati invece di utilizzare i) un profilo di prodotto della giusta istanza AEM o ii) un gruppo di utenti Adobe Admin Console.

