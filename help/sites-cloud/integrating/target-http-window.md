---
title: Finestra Adobe AEM Target HTTP
description: 'Finestra Adobe AEM Target HTTP '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# Introduzione {#introduction}

Questa pagina descrive i parametri configurabili presenti nella finestra Adobe AEM Target HTTP.

## Parametri {#parameters}

![Finestra HTTP](assets/httpwindow.png "WindowTarget di Target")

La finestra contiene i seguenti parametri configurabili:

| Parametro | Descrizione |
|---|---|
| URL API Adobe Target  | L&#39;URL dell&#39;API del Adobe Target . |
| Abilita URL assoluto | Determina se utilizzare la parte host dell&#39;URL o l&#39;URL completo. Selezionate la casella di controllo se desiderate utilizzare l’URL completo (senza abbreviazioni). Per impostazione predefinita, la casella di controllo è disattivata. |
| Timeout della connessione | Timeout (in millisecondi) fino a quando non viene stabilita una connessione. Il valore predefinito è 60000 millisecondi. Il valore 0 viene interpretato come un timeout infinito. |
| Timeout socket | Timeout (in millisecondi) per attendere i dati o un periodo massimo di inattività tra due pacchetti di dati consecutivi. Il valore predefinito è 30000 millisecondi. |
|  URL Raccomandazioni Adobe Target Sostituire il token Regex | Controlla il token nell&#39;URL dell&#39;endpoint del Adobe Target  che deve essere sostituito per puntare all&#39;URL API delle raccomandazioni di Target. |
|  URL di Recommendations del Adobe Target Sostituisci con token | Sostituzione per il regex descritto nel parametro precedente, in modo che l&#39;URL risultante faccia riferimento all&#39;API Target Recommendations. |
