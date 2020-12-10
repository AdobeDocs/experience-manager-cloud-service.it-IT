---
title: Eliminazione di un certificato SSL - Gestione dei certificati SSL
description: Eliminazione di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Eliminazione di un certificato SSL {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>La rimozione dei certificati da Cloud Manager è un&#39;azione permanente che non può essere annullata. La procedura consigliata consiste nel salvare localmente tutti i file SSL necessari prima di eliminarli nell&#39;interfaccia utente di Cloud Manager.

Per eliminare un certificato SSL in Cloud Manager, un utente deve essere incluso nel ruolo Proprietario business o Gestione distribuzione. Cloud Manager non consente di eliminare un certificato SSL a cui sono associati uno o più domini.  Tutti i domini associati devono essere eliminati prima di eliminare il certificato SSL. Per ulteriori informazioni, fare riferimento a [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md).

Per eliminare un certificato SSL, effettuate le seguenti operazioni:

1. Passare alla schermata **Certificati SSL** dalla pagina **Ambienti**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. Identificate la riga in cui è elencato il nome del certificato SSL che desiderate eliminare.
1. Selezionare la **...** menu dall&#39;estremità destra della riga.
1. Selezionare **Elimina**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. Confermate l&#39;invio dalla finestra di dialogo **Elimina certificato SSL**.
