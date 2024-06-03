---
title: Come risolvere gli errori di creazione dei moduli?
description: Risoluzione dei problemi relativi agli errori di creazione dei moduli nell’ambiente as a Cloud Service di AEM Forms.
feature: Adaptive Forms, Troubleshooting
role: User
source-git-commit: 23491130b44147753c5b98f316be5a9e5937afea
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Problema durante la pubblicazione dei moduli{#form-creation-fails}

Dopo che gli utenti si aggiornano alla versione as a Cloud Service di AEM Forms `2024.5.16461`:

**Alcuni utenti** potrebbe verificarsi un problema durante la creazione dei moduli. di conseguenza, quando un utente crea un modulo, nella finestra di dialogo di creazione viene visualizzato il messaggio di errore seguente:

`A server error occurred. Try again after sometime.`

## Causa {#cause-form-creation-fails}

Il problema si verifica perché l’autore pubblica il modulo senza **prima pubblicazione del modello** utilizzato in esso. Ciò comporta l&#39;aggiunta del `jcr:uuid` e altre proprietà protette e generate dal sistema `<template-path>/initial/jcr:content` causando errori nella successiva creazione del modulo.

## Soluzione alternativa {#resolution-form-creation-fails}

Per risolvere il problema, effettuare le seguenti operazioni:

1. Verificare che il modello utilizzato nel modulo non disponga di `jcr:uuid` e altre proprietà protette generate dal sistema nel percorso `<template-path>/initial/jcr:content node`.
1. Pubblica il modello esplicitamente utilizzando la console modelli.
1. Ora, quando il modello viene pubblicato, provare a creare nuovi moduli utilizzando il modello.
1. Se il modello utilizzato viene aggiornato nelle versioni future, pubblicalo nuovamente (come indicato nel passaggio 2) per evitare problemi di errore durante la creazione del modulo.


<!--

# Issue {#form-creation-fails}

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->










