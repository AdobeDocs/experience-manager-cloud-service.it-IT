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

## Tipi di programma {#program-types}

Un utente può creare un programma **Sandbox** o **Regular**.

Di norma, viene creata una *sandbox* per consentire la formazione, l&#39;esecuzione di dimostrazioni, l&#39;abilitazione, i POC o la documentazione. Non è destinato a trasportare traffico live e avrà delle restrizioni che un programma regolare non vuole. Includerà Siti e Risorse e verrà distribuito automaticamente con un ramo Git che include codice di esempio, un ambiente Dev e una pipeline non di produzione.

Viene creato un *Programma regolare* per attivare il traffico live al momento opportuno in futuro.