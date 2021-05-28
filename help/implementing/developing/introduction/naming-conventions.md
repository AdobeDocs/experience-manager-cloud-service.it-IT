---
title: Convenzioni di denominazione
description: I nodi nell’archivio sono soggetti a denominazioni convenzionali del Java Content Repository
exl-id: 3c5c39dd-b209-488b-a93e-e840786fe224
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 9%

---

# Convenzioni di denominazione{#naming-conventions}

I nodi nell&#39;archivio sono soggetti a denominazioni convenzionali del Java Content Repository. Tuttavia AEM impone ulteriori convenzioni per il nome dei nodi di pagina.

## Convenzioni di denominazione per le pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione sono implementate a vari livelli:

* JcrUtil: implementazione AEM delle [utility JCR](#jcr-utilities).
* PageManager: il [Page Manager](#page-manager) fornisce metodi per le operazioni a livello di pagina.
* Nell’interfaccia AEM {#ui-behavior}

### Utilità JCR {#jcr-utilities}

[](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/commons/jcr/JcrUtil.html) JcrUtilis l&#39;implementazione AEM delle utility JCR. Di particolare interesse per la convalida dei nomi sono le mappature dei caratteri che controlla e le seguenti convalide:

* `isValidName`
   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.
* `createValidName`
   * Questo crea un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Gestore pagina {#page-manager}

[](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) PageManager fornisce metodi per le operazioni a livello di pagina, in base a  [JCRUtil](#jcr-utilities).

### Comportamento dell&#39;interfaccia AEM {#ui-behavior}

Durante la gestione del contenuto, nell’interfaccia AEM:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:
   * viene fornito un titolo di pagina per la conversione nel nome del nodo
   * viene fornito un nome di nodo esplicito
