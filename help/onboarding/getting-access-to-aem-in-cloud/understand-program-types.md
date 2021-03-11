---
title: Informazioni sui tipi di programma e di programma
description: Informazioni sui tipi di programma e di programma - Cloud Services
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# Informazioni su programmi e tipi di programmi {#understanding-programs}

In Cloud Manager, l’entità tenant è nella parte superiore che può contenere più programmi. Ogni programma può contenere non più di un ambiente di produzione e più ambienti non di produzione.

Il diagramma seguente mostra la gerarchia delle entità in Cloud Manager.

![immagine](assets/program-types1.png)

## Tipi di programmi {#program-types}

Un utente può creare un programma **Sandbox** o **Produzione**.

* Viene creato un *programma di produzione* per abilitare il traffico live al momento appropriato in futuro.
Per ulteriori informazioni, consulta [Introduzione ai programmi di produzione](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md) .


* Un *programma sandbox* viene generalmente creato per scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione. Non è destinato a trasportare traffico live e avrà restrizioni che un programma di produzione non intende. Includerà Sites e Assets e verrà fornito automaticamente con un ramo Git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
Per ulteriori informazioni, consulta [Introduzione ai programmi sandbox](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) .

