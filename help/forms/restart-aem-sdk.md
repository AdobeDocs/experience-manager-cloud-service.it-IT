---
title: Come si riavvia l’SDK per AEM?
description: Best practice per riavviare l’SDK per AEM
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 7%

---

# Riavvio dell’SDK dell’AEM

Se riavvii l’SDK dell’AEM interrompendo i processi Java™, potrebbero verificarsi incoerenze nell’ambiente di sviluppo dell’AEM, come segue:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Riavvia-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Soluzione

Per riavviare l&#39;SDK per AEM, passare alla finestra di comando attiva e premere il comando `Ctrl + C` per riavviare l&#39;SDK.

Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java™, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Consulta anche

* [Configurare l’ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md)
* [Abilitare i componenti core per moduli adattivi](/help/forms/enable-adaptive-forms-core-components.md)
