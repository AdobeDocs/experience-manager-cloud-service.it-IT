---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.7.0'
description: Note sulla versione 2020.7.0 di Experience Manager
translation-type: tm+mt
source-git-commit: 74abf1c4cc6ae449a81e3e40d073bfcb23b056e8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 29%

---


# Note sulla versione di AEM as a Cloud Service 2020.7.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.7.0.

## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.7.0.

### Data di rilascio {#release-date}

La data di rilascio per [!UICONTROL Cloud Manager] versione 2020.7.0 è il 9 luglio 2020.

### Novità {#what-is-new-cloud-manager}

* La pagina degli ambienti è stata riprogettata.

* Gli ambienti con sospensione ora mostrano uno stato discreto in Cloud Manager quando sono attivati.

* Il contenitore di build di Cloud Manager ora supporta sia Java 8 che Java 11.

### Correzioni di bug {#bug-fixes-cm}

* Il collegamento da Cloud Manager a Developer Console non era correttamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento alla console per sviluppatori direttamente da Cloud Manager non consentiva di disattivare/attivare l&#39;ambiente di un programma sandbox.

* Le opzioni **Annulla** e **Salva** nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potrebbero causare la mancata generazione corretta del file di registro.

* Quando si crea un nuovo programma, il nome suggerito a volte restituisce un duplicato di un nome di programma esistente.

* Non è stato possibile scaricare in modo coerente alcuni log delle fasi della pipeline di grandi dimensioni tramite l&#39;interfaccia utente.

* La convalida dei nomi dell&#39;ambiente presentava un errore &quot;off-by-one&quot;.

* In alcuni casi, la pagina Ambienti visualizzava segmenti di pubblicazione e dispatcher se non ne erano presenti.