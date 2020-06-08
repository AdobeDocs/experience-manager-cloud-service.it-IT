---
title: Aggiunta di utenti e ruoli - Elementi richiesti
description: Aggiunta di utenti e ruoli - Elementi richiesti
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 8%

---


# Aggiungere utenti e ruoli {#add-users-roles}


Molte funzionalità di [!UICONTROL Cloud Manager] richiedono autorizzazioni specifiche per funzionare. Ad esempio, solo alcuni utenti possono impostare i KPI (Key Performance Indicators) per un programma. Tali autorizzazioni sono logicamente raggruppate in ruoli.

[!UICONTROL Cloud Manager] definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Business Owner (Proprietario)
* Program Manager (Responsabile programma)
* Deployment Manager (Responsabile implementazione)
* Developer (Sviluppatore)

>[!CAUTION]
>
>Per utilizzare [!UICONTROL Cloud Manager], è necessario disporre di un Adobe ID e del contesto di prodotto dei servizi gestiti Adobe.

## Definizioni dei ruoli {#role-definitions}

>[!NOTE]
>
>La persona Sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli di Cloud Manager] | Descrizione |
|--- |--- |
| Business Owner (Proprietario) | Responsabile della definizione dei KPI, dell&#39;approvazione delle implementazioni di produzione e della risoluzione di importanti errori a 3 livelli. |
| Program Manager (Responsabile programma) | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, verificare lo stato e visualizzare i KPI. Può approvare importanti fallimenti a 3 livelli. |
| Deployment Manager (Responsabile implementazione) | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di fase/produzione. È possibile modificare le tubazioni CI/CD. Può approvare importanti fallimenti a 3 livelli. Può accedere al repository Git. |
| Developer (Sviluppatore) | Sviluppa e verifica il codice applicazione personalizzato. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Content Author | Generalmente non interagisce con [!UICONTROL Cloud Manager]. Può utilizzare il commutatore di programmi [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]) per accedere ad AEM. |