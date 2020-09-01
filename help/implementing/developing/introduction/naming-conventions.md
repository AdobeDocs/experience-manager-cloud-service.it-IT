---
title: Convenzioni di denominazione
description: I nodi nell'archivio sono soggetti alle convenzioni di denominazione dell'archivio dei contenuti Java
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 8%

---


# Naming Conventions{#naming-conventions}

I nodi nell&#39;archivio sono soggetti a denominazioni convenzionali del Java Content Repository. Tuttavia AEM ulteriori convenzioni per il nome dei nodi di pagina.

## Convenzioni di denominazione per le pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione sono implementate a vari livelli:

* JcrUtil: l&#39;AEM implementazione delle utility [JCR](#jcr-utilities).
* PageManager: il gestore [](#page-manager) pagina fornisce metodi per le operazioni a livello di pagina.
* Nell’interfaccia AEM {#ui-behavior}

### Utilità JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) è l&#39;implementazione AEM delle utility JCR. Di particolare interesse per la convalida dei nomi sono le mappature dei caratteri che controlla e le seguenti convalide:

* `isValidName`
   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.
* `createValidName`
   * In questo modo viene creata un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Page Manager {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) fornisce metodi per le operazioni a livello di pagina, in base a [JCRUtil](#jcr-utilities).

### AEM comportamento dell&#39;interfaccia utente {#ui-behavior}

Quando gestite il contenuto, l&#39;interfaccia AEM:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:
   * un titolo di pagina è fornito per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito
