---
title: Gestione multisito di Ripoless
description: Scopri i consigli sulle best practice per configurare un progetto con siti multilingue sfruttando un’unica base di codice in modo repoless.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Gestione multisito di Ripoless {#repoless-msm}

In questo documento si presuppone che sia già stato creato un sito di base per il progetto denominato `my-aem-site` e che si desideri localizzarlo utilizzando la funzionalità MSM di AEM.

Se hai già configurato il progetto per il caso d&#39;uso Repoless, la configurazione cloud viene assegnata al livello della pagina root, `/content/my-aem-site`. Per i siti multilingue, l&#39;assegnazione della configurazione deve essere modificata nella directory principale della lingua, ad esempio `/content/my-aem-site/language-master/de`.

