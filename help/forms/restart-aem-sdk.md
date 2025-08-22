---
title: Come riavviare AEM SDK?
description: Best practice per il riavvio di AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 2%

---

# Riavvio di AEM SDK

Se riavvii AEM SDK arrestando i processi Java™, potrebbero verificarsi incongruenze nell’ambiente di sviluppo AEM, come segue:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Riavvia-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Soluzione

Per riavviare AEM SDK, passare alla finestra dei comandi attiva e premere il comando `Ctrl + C` per riavviare SDK.

Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java™, può causare incongruenze nell’ambiente di sviluppo AEM.

## Consulta anche

* [Configurare l’ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md)

