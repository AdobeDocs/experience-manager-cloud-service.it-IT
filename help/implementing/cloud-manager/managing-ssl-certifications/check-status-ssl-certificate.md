---
title: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
description: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Controllo dello stato di un certificato SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere compreso immediatamente dalla pagina del certificato SSL.

Puoi identificare lo stato di un certificato SSL dai seguenti schemi di colore:

* **Verde**
Indica che il certificato è valido per almeno 60 giorni nel futuro.

* **Arancio**
Indica che il certificato scade in meno di 60 giorni. È ora di verificare di avere un piano per rinnovare il certificato e sostituirlo tramite l’interfaccia utente di Cloud Manager al fine di evitare possibili accessi o interruzioni del sito. Cloud Manager invia notifiche regolari nell’interfaccia utente per avvisarti della scadenza imminente del certificato.

* **Rosso**
Indica che, nonostante più notifiche, il certificato SSL è scaduto.

## Configurazioni CDN preesistenti {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nel **ELENCO CONSENTITI IP** e **Ambiente** pagina dei dettagli. Il messaggio visualizzato nell’interfaccia utente scompare dopo la migrazione completa da parte del cliente di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente e potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente. Fai riferimento a [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) per ulteriori dettagli.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
