---
title: Convenzioni di denominazione
description: I nodi nell’archivio sono soggetti alle convenzioni di denominazione dell’archivio dei contenuti Java
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# Convenzioni di denominazione{#naming-conventions}

I nodi nell’archivio sono soggetti alle convenzioni di denominazione dell’archivio dei contenuti Java. Tuttavia, l’AEM impone ulteriori convenzioni per il nome dei nodi della pagina.

## Convenzioni di denominazione delle pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione vengono implementate a vari livelli:

* JcrUtil: implementazione AEM delle [utilità JCR](#jcr-utilities).
* PageManager: [Page Manager](#page-manager) fornisce metodi per le operazioni a livello di pagina.
* Nell&#39;interfaccia utente AEM {#ui-behavior}

### Utilità JCR {#jcr-utilities}

[JcrUtil](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/jcr/JcrUtil.html) è l&#39;implementazione AEM delle utilità JCR. Di particolare interesse per la convalida dei nomi sono le mappature di caratteri che controlla e le convalide seguenti:

* `isValidName`
   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.
* `createValidName`
   * In questo modo viene creata un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Gestione pagine {#page-manager}

[PageManager](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) fornisce metodi per le operazioni a livello di pagina, basati su [JCRUtil](#jcr-utilities).

### Comportamento dell’interfaccia AEM {#ui-behavior}

Durante la gestione dei contenuti, l’interfaccia utente dell’AEM:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:
   * viene fornito il titolo della pagina da convertire nel nome del nodo
   * viene fornito un nome di nodo esplicito
