---
title: Aggiunta di utenti e ruoli - Elementi richiesti
description: Aggiunta di utenti e ruoli - Elementi richiesti
translation-type: tm+mt
source-git-commit: 1d2d39ba3dd84b79420da94c985b00aa1bb5b806

---


# Aggiunta di utenti e ruoli - Elementi richiesti {#add-users-roles}


Molte funzionalità di [!UICONTROL Cloud Manager] richiedono autorizzazioni specifiche per funzionare. Ad esempio, solo alcuni utenti possono impostare i KPI (Key Performance Indicators) per un programma. Tali autorizzazioni sono logicamente raggruppate in ruoli.

[!UICONTROL Cloud Manager] definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Proprietario
* Program Manager
* Gestione distribuzione
* Sviluppatore

>[!CAUTION]
>
>Per utilizzare [!UICONTROL Cloud Manager], è necessario disporre di un Adobe ID e del contesto prodotto dei servizi gestiti Adobe.

## Definizioni dei ruoli {#role-definitions}

>[!NOTE]
>
>La persona Sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli di Cloud Manager] | Descrizione |
|--- |--- |
| Proprietario | Responsabile della definizione dei KPI, dell&#39;approvazione delle implementazioni di produzione e della risoluzione di importanti errori a 3 livelli. |
| Program Manager | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, verificare lo stato e visualizzare i KPI. Può approvare importanti fallimenti a 3 livelli. |
| Gestione distribuzione | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di fase/produzione. È possibile modificare le tubazioni CI/CD. Può approvare importanti fallimenti a 3 livelli. Può accedere al repository Git. |
| Sviluppatore | Sviluppa e verifica il codice applicazione personalizzato. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Content Author | Generalmente non interagisce con [!UICONTROL Cloud Manager]. Può utilizzare il commutatore di programmi [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]) per accedere ad AEM. |