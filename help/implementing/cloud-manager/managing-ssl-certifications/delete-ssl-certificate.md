---
title: Eliminazione di un certificato SSL - Gestione di certificati SSL
description: Eliminazione di un certificato SSL - Gestione di certificati SSL
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---

# Eliminazione di un certificato SSL {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>La rimozione dei certificati da Cloud Manager è un’azione permanente che non può essere annullata. Si consiglia di salvare localmente tutti i file SSL necessari prima di eliminarli nell’interfaccia utente di Cloud Manager.

Per eliminare un certificato SSL in Cloud Manager, un utente deve trovarsi nel ruolo Proprietario business o Gestore distribuzione. Cloud Manager non ti consente di eliminare un certificato SSL associato a uno o più domini.  Tutti i domini associati devono essere eliminati prima di eliminare il certificato SSL. Fai riferimento a [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) per saperne di più.

Per eliminare un certificato SSL, effettua le seguenti operazioni:

1. Passa a **Certificati SSL** dalla schermata **Ambienti** pagina.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. Identifica la riga in cui è elencato il nome del certificato SSL che desideri eliminare.
1. Seleziona la **...** dall&#39;estremità destra della riga.
1. Seleziona **Elimina**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. Conferma l’invio da **Elimina certificato SSL** finestra di dialogo.
