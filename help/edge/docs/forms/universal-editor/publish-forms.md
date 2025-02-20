---
title: Pubblica AEM Forms per Edge Delivery Services.
description: Pubblicare i Edge Delivery Services Form in modo rapido e semplice.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Pubblicare il modulo adattivo in Edge Delivery Services

Quando il modulo è finalizzato e pronto per l’uso, è possibile pubblicarlo per renderlo accessibile ai clienti per la raccolta e l’invio dei dati. La pubblicazione garantisce che il modulo sia disponibile su Edge Delivery, consentendo agli utenti di interagire direttamente con esso. Questo processo consente ai clienti di compilare e inviare il modulo in tempo reale, garantendo un&#39;acquisizione efficiente dei dati e una elaborazione semplificata.

## Prerequisiti

* Modulo creato utilizzando il modello **Edge Delivery Services (EDS)**. [Ulteriori informazioni](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) sulla creazione di un modulo basato su EDS.

## Pubblicare il modulo

Puoi pubblicare qualsiasi **modulo adattivo basato su EDS** in Edge Delivery seguendo questi passaggi:

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. Apri il modulo adattivo nell&#39;editor e fai clic sull&#39;icona **Pubblica** nella barra superiore.
   ![Fai clic su Pubblica](/help/forms/assets/publish-icon-eds-form.png)

1. Quando fai clic su **Pubblica**, viene visualizzata una schermata o un pop-up che mostra le risorse di pubblicazione, incluso il titolo del modulo. In questo esempio viene utilizzato il modello **Wknd_Form**.
   ![Al clic del mouse](/help/forms/assets/on-click-publish.png)

1. Fai di nuovo clic su **Pubblica** per visualizzare un pop-up di conferma, che indica che il modulo è ora pubblicato.
   ![Pubblicazione completata](/help/forms/assets/publish-success.png)

1. Per verificare lo stato di pubblicazione del modulo, fai di nuovo clic su **Pubblica**.
   ![Stato pubblicazione](/help/forms/assets/publish-status.png)

1. Per **annullare la pubblicazione** di un modulo, apri il modulo nell&#39;editor, fai clic sul menu a tre punti in alto a destra e fai clic su **Annulla pubblicazione**.
   ![Annulla pubblicazione](/help/forms/assets/unpublish--form.png)

## Abilitare l’invio di moduli su Edge Delivery configurando un filtro Referrer per AEM Publisher

Per garantire l&#39;invio sicuro dei moduli, è necessario configurare un **filtro referrer** in AEM Publisher. Questo filtro garantisce che solo le richieste autorizzate da Edge Delivery possano eseguire operazioni di scrittura (POST, PUT, DELETE, COPY, MOVE), impedendo modifiche non autorizzate. Di seguito sono riportati i passaggi necessari per configurare un filtro Referrer per AEM Publisher:

### Aggiornare l’URL dell’istanza di AEM in Edge Delivery

Modifica `submitBaseUrl` nel file **constant.js** all&#39;interno del blocco del modulo per specificare l&#39;URL dell&#39;istanza di AEM:

**Configurazione cloud:**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
**Per lo sviluppo locale:**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### Modificare la configurazione CORS

Regola le **impostazioni CORS** per consentire le richieste di invio di moduli dai domini Edge Delivery. Per ulteriori informazioni, consultare la [Guida alla configurazione CORS](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).

**Configurazione CORS di esempio:**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
Per lo sviluppo locale, consulta la [documentazione](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter) per abilitare CORS dall&#39;**URL host interfaccia utente di sviluppo**.

### Configurare il filtro Referrer

Configura il **filtro Referrer** in AEM Cloud Service tramite Cloud Manager. [Ulteriori informazioni](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) sulla configurazione del filtro referente in un&#39;istanza di AEM Cloud Service tramite Cloud Manager.

**Configurazione JSON per il filtro Referrer:**

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
    "https://.*\\.hlx\\.page:443",
    "https://.*\\.hlx\\.live:443"
  ],
  "filter.methods": [
    "POST",
    "PUT",
    "DELETE",
    "COPY",
    "MOVE"
  ],
  "exclude.agents.regexp": [
    ""
  ]
}
```

Questa configurazione specifica quali metodi HTTP vengono filtrati, quali referenti sono consentiti e quali agenti utente sono esclusi dal filtro. Implementando queste configurazioni, **gli invii di moduli tramite Edge Delivery** saranno protetti e limitati solo alle origini autorizzate.

### Accedere al modulo adattivo pubblicato

Il modulo adattivo è ora accessibile tramite **Edge Delivery** utilizzando il seguente formato URL:

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

Ad esempio, l&#39;URL per **Wknd-Form** è:

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## Consulta anche

{{universal-editor-see-also}}

