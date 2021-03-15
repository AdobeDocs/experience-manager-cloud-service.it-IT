---
title: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
description: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: ddee11fdfa8cadfcd63472fd3c94cd8af555c856
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Verifica dello stato di un certificato SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere compreso immediatamente dalla pagina del certificato SSL.

Puoi identificare lo stato di un certificato SSL dai seguenti schemi di colore:

* ****
VerdeIndica che il certificato è valido per almeno 60 giorni nel futuro.

* ****
OrangeIndica che il certificato scade tra meno di 60 giorni. È ora di verificare di avere un piano per rinnovare il certificato e sostituirlo tramite l’interfaccia utente di Cloud Manager al fine di evitare possibili accessi o interruzioni del sito. Cloud Manager invia notifiche regolari nell’interfaccia utente per avvisarti della scadenza imminente del certificato.

* ****
RossoIndica che, nonostante più notifiche, il certificato SSL è scaduto.

## Configurazioni CDN preesistenti per Inserire nell&#39;elenco Consentiti IP {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nella pagina dei dettagli **Elenco consentiti IP** e **Ambiente** .

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente, come illustrato nella figura riportata di seguito.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)