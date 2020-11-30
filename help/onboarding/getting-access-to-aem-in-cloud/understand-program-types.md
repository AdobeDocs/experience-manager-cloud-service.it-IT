---
title: Informazioni sui tipi di programma
description: Informazioni sui tipi di programma e di programma - Cloud Services
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# Informazioni su programmi e tipi di programmi {#understanding-programs}

In Cloud Manager l&#39;entità tenant è nella parte superiore, che può contenere più programmi.  Ogni programma può contenere un solo ambiente di produzione e più ambienti non di produzione.

Il diagramma seguente mostra la gerarchia delle entità in Cloud Manager.

![immagine](assets/program-types1.png)

## Tipi di programmi {#program-types}

Un utente può creare un **sandbox** o un programma **regolare** .

In genere, viene creata una *sandbox* per scopi di formazione, esecuzione di dimostrazioni, abilitazione, POC o documentazione. Non è destinato a trasportare traffico live e avrà delle restrizioni che un programma regolare non vuole. Includerà Siti e Risorse e verrà distribuito automaticamente con un ramo Git che include codice di esempio, un ambiente Dev e una pipeline non di produzione.

Viene creato un programma ** regolare per consentire il traffico live al momento opportuno in futuro.