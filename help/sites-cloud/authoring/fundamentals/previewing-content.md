---
title: Anteprima del contenuto
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima il contenuto prima di iniziare la pubblicazione.
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Anteprima del contenuto {#previewing-content}

>[!NOTE]
>
>La funzione Anteprima fa parte della versione 2021.5.0 e verrà implementata gradualmente nelle prossime settimane.

AEM offre un servizio di anteprima dei siti progettato per consentire agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione ed sia disponibile al pubblico.

Consente di visualizzare in anteprima le esperienze di pagina che non sarebbero altrimenti visibili dall’ambiente di authoring, come le transizioni di pagina e altri contenuti solo lato pubblicazione.

## Pubblicazione del contenuto nell&#39;anteprima {#publishing-content-to-preview}

Puoi pubblicare il contenuto nel servizio di anteprima utilizzando l’interfaccia utente della pubblicazione gestita come segue:

1. Seleziona le pagine da inviare per l’anteprima nella console Sites e fai clic sul pulsante **Gestisci pubblicazione**
1. Nella procedura guidata seguente, seleziona **Anteprima** come destinazione

   ![pubblicazione gestita](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Fai clic su **Avanti**, quindi su **Pubblica** per confermare.

Per visualizzare il contenuto dell&#39;anteprima, aggiungi **preview** all&#39;URL di pubblicazione dell&#39;istanza di produzione. L’URL deve essere costruito come segue:

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

Per ulteriori informazioni su come ottenere gli URL per i tuoi ambienti, consulta [Gestisci gli ambienti](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) .

