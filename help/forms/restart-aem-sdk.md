---
title: Come si riavvia l’SDK per AEM?
description: Best practice per riavviare l’SDK per AEM
role: Admin, Developer, User
feature: Adaptive Forms
source-git-commit: a0e2c0e3020d48b171645818b8e02dc33b50c2d5
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 2%

---


# Riavvio dell’SDK dell’AEM

Se riavvii l’SDK dell’AEM interrompendo i processi Java™, potrebbero verificarsi incoerenze nell’ambiente di sviluppo dell’AEM, come segue:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Soluzione

Per riavviare l&#39;SDK dell&#39;AEM, passare alla finestra di comando attiva e premere `Ctrl + C` per riavviare l&#39;SDK.

Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java™, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Consulta anche

* [Configurare l’ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md)
* [Abilita componenti core Forms adattivi](/help/forms/enable-adaptive-forms-core-components.md)
