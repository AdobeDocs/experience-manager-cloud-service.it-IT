---
title: Finestra HTTP di Adobe AEM Target
description: Finestra HTTP di Adobe AEM Target
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 89%

---


# Introduzione {#introduction}

Questa pagina descrive i parametri configurabili presenti nella finestra HTTP di Adobe AEM Target.

## Parametri {#parameters}

![Finestra HTTP di Target](assets/httpwindow.png "Finestra HTTP di Target")

La finestra contiene i seguenti parametri configurabili:

| Parametro | Descrizione |
|---|---|
| URL API di Adobe Target | URL dell’API Adobe Target. |
| Abilitare URL assoluto | Determina se si utilizza la parte host dell’URL o l’URL completo. Attiva la casella di controllo se desideri utilizzare l’URL completo (non abbreviato). Per impostazione predefinita, la casella di controllo è disabilitata. |
| Timeout della connessione | Timeout (in millisecondi) fino a quando non viene stabilita una connessione. Il valore predefinito è pari a 60000 millisecondi. Un valore pari a 0 viene interpretato come un timeout infinito. |
| Timeout socket | Timeout (in millisecondi) in attesa dei dati o per un periodo massimo di inattività tra due pacchetti di dati consecutivi. Il valore predefinito è pari a 30000 millisecondi. |
| Gli URL dei consigli di Adobe Target sostituiscono Regex Token | Controlla il token nell’URL dell’endpoint Adobe Target che deve essere sostituito per puntare all’URL API dei consigli di Target. |
| Sostituzione URL consigli di Adobe Target con Token | Sostituzione del regex descritto nel parametro precedente, in modo che l’URL risultante punti all’API di consigli di Target. |
