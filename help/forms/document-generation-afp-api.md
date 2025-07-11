---
title: Come si utilizza l’API di sincronizzazione dell’output AFP?
description: Scopri come utilizzare l’API AFP Output Sync per recuperare e sincronizzare le rappresentazioni di output.
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, User
source-git-commit: 0b86f3bf71505b69ef995369045b7c682d7db8e3
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 10%

---

# Generare output AFP utilizzando l’API AEM Forms

<span class="preview">Si tratta di una funzione pre-release accessibile tramite il [canale pre-release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features). </span>

Advanced Function Presentation (AFP) è un formato di documento ad alte prestazioni progettato principalmente per scopi di stampa.\
Questa guida descrive tutti i passaggi e le configurazioni necessari per generare l’output AFP utilizzando AEM Forms.

<!--
## Prerequisites

To support AFP output generation, the following OSGi bundles must be present and in an **active** state:

* **AFP Core Bundle** – Available in the AFP repository
* **Forms Output Core** – Found in the Forms Output comments package
* **Bedrock Connector** – Provided by the Forms Output API
* **Cloud Ready Implementation** – Available through the Forms installer

>[!NOTE]
>
> * If any bundle is inactive, resolve dependency issues or reinstall manually.
> * To enable AFP generation, the `FT_FORMS-17887` toggle configurations must be set in AEM configuration manager.-->

## API di generazione AFP

Genera un file AFP (Advanced Function Presentation) utilizzando un modello XDP e i dati di input.

### Autorizzazione

È possibile utilizzare **BasicAuth** (credenziali amministratore) per gli ambienti locali o **BearerAuth** per le istanze di AEM Cloud.

### Richiesta

**Endpoint:**
`POST http://<server>:<port>/adobe/forms/document/generate/afp`

### Intestazioni

| Chiave | Valore |
| --------------- | ------------------------------------------------------ |
| `Content-Type` | `application/pdf` |
| `Authorization` | `(Bearer Access token)` |

### Corpo della richiesta

**Tipo di contenuto: multipart/form-data**

| Chiave | Tipo | Obbligatorio | Descrizione |
| ---------- | ---- | -------- | ------------------------------------------------------------------------- |
| `template` | File/Testo | Sì | File XDP utilizzato come modello per la generazione AFP (ad esempio, `demo.xdp`) |
| `data` | File/Testo | No | File di dati (XML o JSON) da unire al modello (ad esempio, `data.xml`) |
| `options` | Testo | No | Stringa JSON con opzioni per controllare l’output AFP (ad es. risoluzione, impostazioni locali) |

**Esempio `options` JSON (campo di testo):**

```json
{
  "pdfVersion": "1.7",
  "resolution": 300,
  "locale": "en-US",
  "embedFonts": true,
  "contentRoot": "/usr/tmp"
}
```

### Risposte

| Codice | Descrizione |
| ----- | ------------------------------------------------------------------------- |
| `200` | Operazione completata. Restituisce il flusso del documento AFP. |
| `400` | Richiesta non valida. Il payload della richiesta non è formattato correttamente o contiene campi obbligatori mancanti. |
| `500` | Errore interno del server. Riprova più tardi. |

### Comando Curl

```
curl --location 'http://<server>:<port>/adobe/forms/document/generate/afp' \
--header 'Authorization: Bearertoken <base64-encoded-credentials>' \
--form 'template=@"<path-to-template>.xdp"' \
--form 'data=@"<path-to-data-file>.xml"' \
--form 'options=<JSON-options-string>'
```

### Test dell’API

Puoi scaricare il file .yaml e caricarlo su Postman per verificare la funzionalità delle API.

![Immagine AFP Postman](/help/forms/assets/afp-postman.png)

Puoi salvare la risposta e aprire il file salvato nel lettore AFP per visualizzarlo.

![Lettore PDF](/help/forms/assets/afp-pdf.png)
