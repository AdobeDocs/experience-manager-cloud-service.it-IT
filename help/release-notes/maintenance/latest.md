---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: fd0b8ca281f35a92876f3c31baa4e17884f23948
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 41%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 12441 {#release-12441}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 12441, rilasciata pubblicamente il 27 giugno 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 12255.

2023.7.0 Feature Activation fornirà il set completo di funzioni per questa versione di manutenzione. Consulta la [Roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per ulteriori informazioni.

### Miglioramenti {#enhancements-12441}

- SITES-8769: Migliorare le chiamate StyleImpl in ResponsiveGrid

### Problemi risolti {#fixed-issues-12441}

- Vari aggiornamenti relativi all’accessibilità
- SITES-12688: Editor pagina: operatore logico OR che non funziona correttamente nella ricerca di Asset Finder
- SITES-4951: Editor pagina: la ricerca dei tag nell’editor pagina non trova i tag secondari
- SITES-12465: Frammenti esperienza: i tasti freccia non funzionano nella finestra di dialogo del componente Frammento esperienza
- SITES-12893: Frammenti di esperienza: applicare la convalida circolare dei riferimenti ai frammenti di esperienza
- SITES-12715: Frammenti di esperienza: le configurazioni del servizio cloud applicate alla cartella Frammenti di esperienza non persistono
- SITES-13097: Frammenti esperienza: impossibile aggiungere frammenti esperienza a un progetto di traduzione
- SITES-13165: GraphQL: Ripristina il comportamento predefinito per il filtraggio di valori nulli
- SITES-12577: Verifica collegamenti: il trasformatore non riscrive i collegamenti in modo intermittente
- SITES-13559: MSM: eccezione &quot;Non modificabile&quot; generata durante il rollout del componente
- SITES-11757: MSM: l’ereditarietà della configurazione di rollout dall’elemento padre non viene ripristinata per le pagine figlie
- SITES-14073: Sites Admin: il rapporto CSV non riesce con 500 quando non si seleziona alcuna proprietà da esportare

### Problemi noti {#known-issues-12441}

Nessuno.

### Tecnologie incorporate {#embedded-tech-12441}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak API 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.0 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
